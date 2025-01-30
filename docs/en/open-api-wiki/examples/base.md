# Base Contract

## .hpp

```cpp
#pragma once

#include <eosio/eosio.hpp>
#include <eosio/print.hpp>
#include <eosio/asset.hpp>
#include <eosio/transaction.hpp>
#include <eosio/action.hpp>

using namespace eosio;
using namespace std;
using std::string;
using std::vector;

namespace eosio {
	class [[eosio::contract("base.token")]] basetoken : public contract {
		public:
			using contract::contract;

		[[eosio::action]]
		void create( const name& issuer, const asset& maximum_supply);
		
		[[eosio::action]]
		void issue( const name& to, const asset& quantity, const string& memo );

		[[eosio::action]]
		void retire( const asset& quantity, const string& memo );

		[[eosio::action]]
		void transfer( const name from, const name to, const asset quantity, const string memo );

		[[eosio::action]]
		void open( const name& owner, const symbol& symbol, const name& ram_payer );

		[[eosio::action]]
		void close( const name& owner, const symbol& symbol );
		
		[[eosio::action]]
		void blacklist( name account, bool a );
		
		[[eosio::action]]
		void stake( const name from, const asset quantity );
		
		[[eosio::action]]
		void unstake( const name from, const asset quantity );
		
		static asset get_supply( const name& token_contract_account, const symbol_code& sym_code )
		{
			stats statstable( token_contract_account, sym_code.raw() );
			const auto& st = statstable.get( sym_code.raw() );
			return st.supply;
		}

		static asset get_balance( const name& token_contract_account, const name& owner, const symbol_code& sym_code )
		{
			accounts accountstable( token_contract_account, owner.value );
			const auto& ac = accountstable.get( sym_code.raw() );
			return ac.balance;
		}

		using create_action = eosio::action_wrapper<"create"_n, &basetoken::create>;
		using issue_action = eosio::action_wrapper<"issue"_n, &basetoken::issue>;
		using retire_action = eosio::action_wrapper<"retire"_n, &basetoken::retire>;
		using transfer_action = eosio::action_wrapper<"transfer"_n, &basetoken::transfer>;
		using open_action = eosio::action_wrapper<"open"_n, &basetoken::open>;
		using close_action = eosio::action_wrapper<"close"_n, &basetoken::close>;
		using blacklist_action = eosio::action_wrapper<"blacklist"_n, &basetoken::blacklist>;
		using stake_action = eosio::action_wrapper<"stake"_n, &basetoken::stake>;
		using unstake_action = eosio::action_wrapper<"unstake"_n, &basetoken::unstake>;
		
		private:
		
		void getblacklist( name account );
		void sub_balance( const name owner, const asset value );
		void add_balance( const name owner, const asset value, const name ram_payer );
		void get_staked_balance( const name from, asset quantity );
		void check_quantity( asset quantity );
		
		struct [[eosio::table]] account {
			asset	balance;
			uint64_t primary_key()const { return balance.symbol.code().raw(); }
		};

		struct [[eosio::table]] currency_stats {
			asset	supply;
			asset	max_supply;
			name	issuer;
			uint64_t primary_key()const { return supply.symbol.code().raw(); }
		};
		
		struct [[eosio::table]] currency_stake {
			name account;
			asset staked;
			uint64_t primary_key()const { return account.value; }
		};
		
		struct [[eosio::table]] blacklists {
			name account;
			uint64_t primary_key() const { return account.value; }
		};

		typedef eosio::multi_index< "accounts"_n, account > accounts;
		typedef eosio::multi_index< "stat"_n, currency_stats > stats;
		typedef eosio::multi_index< "stake"_n, currency_stake > stakeds;
		typedef eosio::multi_index< "blacklist"_n, blacklists > db_blacklist;
	};
}
```

## .cpp

```cpp
#include <eosio/eosio.hpp>
#include <eosio/asset.hpp>
#include <eosio/transaction.hpp>
#include <eosio/system.hpp>
#include <eosio/crypto.hpp>
#include <eosio/action.hpp>
#include <eosio/print.hpp>

using namespace eosio;
using namespace std;
using std::string;
using std::vector;

#include "basetoken.hpp"

namespace eosio {

void basetoken::create( const name&	issuer, const asset& maximum_supply )
{
	require_auth( get_self() );

	auto sym = maximum_supply.symbol;
	check( sym.is_valid(), "Invalid symbol name" );
	check( maximum_supply.is_valid(), "Invalid supply");
	check( maximum_supply.amount > 0, "Max-Supply must be more then 0");

	stats statstable( get_self(), sym.code().raw() );
	auto existing = statstable.find( sym.code().raw() );
	check( existing == statstable.end(), "This token already exist" );

	statstable.emplace( get_self(), [&]( auto& s ) {
		s.supply.symbol = maximum_supply.symbol;
		s.max_supply	= maximum_supply;
		s.issuer		= issuer;
	});
}

void basetoken::issue( const name& to, const asset& quantity, const string& memo )
{
	getblacklist( to );
	auto sym = quantity.symbol;
	check( sym.is_valid(), "Invalid symbol name" );
	check( memo.size() <= 256, "Memo has more than 256 bytes" );

	stats statstable( get_self(), sym.code().raw() );
	auto existing = statstable.find( sym.code().raw() );
	check( existing != statstable.end(), "This token dont exist." );
	const auto& st = *existing;
	check( to == st.issuer, "Token can only be issued TO issuer account" );
	require_recipient( to );
	require_auth( st.issuer );
	check( quantity.is_valid(), "Invalid quantity" );
	check( quantity.amount > 0, "Amount should be more then 0" );

	check( quantity.symbol == st.supply.symbol, "Symbol precision mismatch" );
	check( quantity.amount <= st.max_supply.amount - st.supply.amount, "Quantity exceeds available supply");

	statstable.modify( st, same_payer, [&]( auto& s ) {
		s.supply += quantity;
	});
	add_balance( st.issuer, quantity, st.issuer );
}

void basetoken::retire( const asset& quantity, const string& memo )
{
	auto sym = quantity.symbol;
	check( sym.is_valid(), "Invalid symbol name" );
	check( memo.size() <= 256, "Memo has more than 256 bytes" );

	stats statstable( get_self(), sym.code().raw() );
	auto existing = statstable.find( sym.code().raw() );
	check( existing != statstable.end(), "Token with symbol does not exist" );
	const auto& st = *existing;

	require_auth( st.issuer );
	check( quantity.is_valid(), "Invalid quantity" );
	check( quantity.amount > 0, "Amount should be more then 0" );

	check( quantity.symbol == st.supply.symbol, "Symbol precision mismatch" );

	statstable.modify( st, same_payer, [&]( auto& s ) {
		s.supply -= quantity;
	});
	sub_balance( st.issuer, quantity );
}

void basetoken::transfer( name from, name to, asset quantity, string memo )
{
	check( from != to, "Cannot transfer to self" );
	require_auth( from );
	getblacklist( from );
	getblacklist( to );
	check( is_account( to ), "TO ["+to.to_string()+"] account does not exist");
	auto sym = quantity.symbol.code();
	stats statstable( get_self(), sym.raw() );
	const auto& st = statstable.get( sym.raw() );

	require_recipient( from );
	require_recipient( to );
	
	check_quantity( quantity );
	check( quantity.symbol == st.supply.symbol, "Symbol precision mismatch" );
	check( memo.size() <= 256, "Memo has more than 256 bytes" );

	auto payer = has_auth( to ) ? to : from;
	
	get_staked_balance( from, quantity );
	
	sub_balance( from, quantity );
	add_balance( to, quantity, payer );
}

void basetoken::sub_balance( const name owner, const asset value ) {
	accounts from_acnts( get_self(), owner.value );
	const auto& from = from_acnts.find( value.symbol.code().raw() );	
	if( from == from_acnts.end() ) {
		check( false, "FROM ["+owner.to_string()+"] dont have ["+value.symbol.code().to_string()+"] tokens" );
	}else{
		check( from->balance.amount >= value.amount, "Overdraw balance on token ["+value.symbol.code().to_string()+"] on ["+owner.to_string()+"]" );
		
		from_acnts.modify( from, owner, [&]( auto& a ) {
			a.balance -= value;
		});
	}
}

void basetoken::add_balance( const name owner, const asset value, const name ram_payer )
{
	accounts to_acnts( get_self(), owner.value );
	auto to = to_acnts.find( value.symbol.code().raw() );
	if( to == to_acnts.end() ) {
		to_acnts.emplace( ram_payer, [&]( auto& a ){
			a.balance = value;
		});
	} else {
		to_acnts.modify( to, same_payer, [&]( auto& a ) {
			a.balance += value;
		});
	}
}

void basetoken::get_staked_balance( const name from, asset quantity ){
	accounts from_acnts( get_self(), from.value );
	auto balance = from_acnts.find( quantity.symbol.code().raw() );
	if( balance != from_acnts.end() ){
		stakeds staked( get_self(), get_self().value );
		auto stake = staked.find( from.value );
		if( stake != staked.end() ) {
			if( balance->balance.amount < ( quantity.amount + stake->staked.amount ) ){
				check( false, "FROM ["+from.to_string()+"] account have staked amount ["+std::to_string( stake->staked.amount )+"]. Balance is less then possible transfer." );
			}
		}
	}
}

void basetoken::open( const name& owner, const symbol& symbol, const name& ram_payer )
{
	require_auth( ram_payer );
	getblacklist( owner );
	getblacklist( ram_payer );

	check( is_account( owner ), "owner ["+owner.to_string()+"] account does not exist" );

	auto sym_code_raw = symbol.code().raw();
	stats statstable( get_self(), sym_code_raw );
	const auto& st = statstable.get( sym_code_raw, "Symbol does not exist" );
	check( st.supply.symbol == symbol, "Symbol precision mismatch" );

	accounts acnts( get_self(), owner.value );
	auto it = acnts.find( sym_code_raw );
	if( it == acnts.end() ) {
		acnts.emplace( ram_payer, [&]( auto& a ){
			a.balance = asset{0, symbol};
		});
	}
}

void basetoken::close( const name& owner, const symbol& symbol )
{
	require_auth( owner );
	getblacklist( owner );
	accounts acnts( get_self(), owner.value );
	auto it = acnts.find( symbol.code().raw() );
	check( it != acnts.end(), "Balance row already deleted or never existed. Action won't have any effect." );
	check( it->balance.amount == 0, "Cannot close because the balance is not zero." );
	acnts.erase( it );
}
 
void basetoken::stake( const name from, const asset quantity )
{
	require_auth( "testedemonft"_n );
	check_quantity( quantity );
	
	accounts from_acnts( get_self(), from.value );
	auto balance = from_acnts.find( quantity.symbol.code().raw() );
	if( balance != from_acnts.end() ){
		if( balance->balance.amount < quantity.amount ){
			check( false, "FROM ["+from.to_string()+"] balance ["+std::to_string( balance->balance.amount )+"] is less then want stake ["+std::to_string( quantity.amount )+"]" );
		}
	}else{
		check( false, "FROM ["+from.to_string()+"] account have balance" );
	}
	
	stakeds staked( get_self(), get_self().value );
	auto to = staked.find( from.value );
	if( to == staked.end() ) {
		staked.emplace( get_self(), [&]( auto& t ){
			t.account = from;
			t.staked = quantity;
		});
	} else {
		staked.modify( to, get_self(), [&]( auto& t ) {
			t.staked += quantity;
		});
	}
}

void basetoken::unstake( const name from, const asset quantity )
{
	require_auth( "testedemonft"_n );
	check_quantity( quantity );
	stakeds staked( get_self(), get_self().value );
	auto stake = staked.find( from.value );
	if( stake == staked.end() ){
		check( false, "FROM ["+from.to_string()+"] account does have stake" );
	}else{
		if( stake->staked.amount == quantity.amount ){
			staked.erase( stake );
		}else if( stake->staked.amount < quantity.amount ){
			check( false, "FROM ["+from.to_string()+"] account have less staked amount ["+std::to_string( stake->staked.amount )+"] then want unstake ["+std::to_string( quantity.amount )+"]" );
		}else{
			staked.modify( stake, get_self(), [&]( auto& a ) {
				a.staked -= quantity;
			});
		}
	}
}

void basetoken::getblacklist( name account ){
	db_blacklist blacklist(get_self(), get_self().value);
	auto black = blacklist.find( account.value );
	if(black != blacklist.end()){
		check(false, "Account is on BLACKLIST");
	}
}
	
void basetoken::blacklist( name account, bool a ){
	require_auth(get_self());
	require_recipient( account );
	if( account == get_self()){
		check(false, "SELF not should be added");
	}
	db_blacklist blacklist(get_self(), get_self().value);
	auto black = blacklist.find( account.value );
	if(black == blacklist.end()){
		if(!a){ check(false, "Account dont exist"); }
		blacklist.emplace(get_self(), [&](auto& t){
			t.account = account;
		});
	}else{
		if(a){
			check(false, "Account already exist");
		}else{
			blacklist.erase(black);
		}
	}
}

void basetoken::check_quantity( asset quantity ){
	auto sym = quantity.symbol;
	check( quantity.is_valid(), "Invalid quantity" );
	check( sym.is_valid(), "Invalid symbol name" );
	check( quantity.amount > 0, "Quantity must be positive");
}

} /// namespace eosio
```
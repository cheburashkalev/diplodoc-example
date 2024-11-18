# DEX API

## Exchange Workflow

### Creating a Pool
```
gf.cdt create [ "useraccount", "gf.cdt", "4,CDT", "3.2500 GFT" ]
```
``Token Contract | Action | [ User | Token Account | Token Symbol | Cost per Token ]``

### Funding the User's Balance on the Exchange
```
gf.cdt transfer '[ "useraccount", "gf.dex", "10.1000 CDT", "add_balance" ]
```
``Token Contract | Action | [ User | Exchange Account | Transfer Amount | Memo with Balance Top-up Identifier ]``

### Transferring Funds from User's Balance to the Pool
```
gf.dex deposit '[ "useraccount", "gf.cdt", "20.0000 GFT" ]
```
``Exchange Contract | Action | [ User | Token Account | Amount ]``

### Optionally - Topping Up the Launch Pool for Passive Earnings
```
gf.cdt transfer '[ "useraccount", "gf.dex", "0.1000 CDT", "testdextknaa:FAA:4" ]
```
``Token Contract | Action | [ User | Exchange Account | Exchange Amount | Memo with Parameters "Token Account for Exchange: Token Symbol for Exchange : Token Precision for Exchange" ]``

### Trading
```
eosio.token transfer '[ "useraccount", "gf.cdt", "0.6000 GFT", "testdextknaa" ]
```
``Token Contract | Action | [ User | Exchange Account | Exchange Amount | Memo with Parameters "Token Account for Exchange" ]``

- **Exchanging TRX for GFL (on the market)** - Leave Memo Empty

- **Exchanging TRX for ETH** - Specify gf.eth (Exchange Contract) in Memo``

- **Exchanging GFL for TRX** - Specify gf.trx (Exchange Contract) in Memo

### Withdrawing Tokens from the Exchange Balance
```
gf.dex withdraw '[ "useraccount", "gf.cdt", 223 ]
```
``Exchange Contract | Action | [ User | Pool Contract | ID from the Pooled Table ]``

### Withdrawing Free Tokens from the Exchange
```
gf.dex tokenback '[ "useraccount", "eosio.token", "1.0000 GFT" ]
```
``Exchange Contract | Action | [ User | Token Contract | Withdrawal Amount ]``

### Withdrawing Earnings
```
gf.dex claim '[ "useraccount", "gf.cdt", "4,CDT" ]'
```
``Exchange Contract | Action | [ User | Token Contract | Token Symbol ]``

## Action '**Create**'

- **Account name**: owner
- **Contract name**: pool token contract
- **Symbol ticker**: pool token symbol
- **Asset price**: starting price of the pool

### Example
```
{
  account: "useraccount",
  contract: "tokenrerer11",
  ticker: "6,TRXTEST",
  price: "665.0000 CFF"
}
```

After creation, the pool is available in the pools table:
```json
"rows": [
{
    "contract": "tokenrerer11",
    "owner": "tokenrerere2",
    "ticker": "6,TRXTEST",
    "price": "72.4164 CFF",
    "v_price": "7241641917",
    "token": "23.042094 TRXTEST",
    "v_token": 2304209486,
    "market": "1668.6260 CFF",
    "v_market": "166862600000",
    "orders": 1
}
]
```

## Balance Refill

- **Memo** - ``add_balance``
- **Table** - ``balance``

### Example
``https://history.dev.globalforce.io/v1/chain/get_table_rows?code=gf.dex&scope=testdexacco1&table=balance&json=true&lower_bound=testdextknaa&limit=2``

```json
"rows": [
    {
        "contract": "tokenrerere1", // token
        "quantity": "4995.2634 USDTEST", // balance
        "onpool": "123.0000 USDTEST" // pool
    }, 
    {
        "contract": "eosio.token",
        "quantity": "1100.0000 CFF",
        "onpool": "123.0000 CFF"
    }, 
    {
        "contract": "tokenrerer11",
        "quantity": "9941.460877 TRXTEST",
        "onpool": "123.0000 TRXTEST"
    }
]
```

## Action '**Deposit**'

- **Account Name**: owner
- **Contract Name**: pool token contract
- **Symbol Market**: the amount of CFF tokens being added to the pool. The amount of paired tokens is calculated in the smart contract and deducted from the balance table.  

### Example
```
{  
	account: "tokenrerere2",  
	contract: "tokenrerer11",  
	market: "105.0000 CFF"  
}  
```

## Pooled

After adding to the pool, a new object is added to the pooled table

- **Table** - ``pooled``

### Example

``https://history.dev.globalforce.io/v1/chain/get_table_rows?code=gf.dex&scope=gf.cdt&table=pooled&index_position=2&key_type=i64&json=true&lower_bound=testdexacco1&limit=10``

```json
"rows": [{
      "id": 1,
      "pair": "7115687411245383680",
      "owner": "gf",
      "contract": "gf.cdt",
      "price": "3.2317 GFT",
      "v_price": 323171046,
      "h_price": "323171046",
      "market": "10.5000 GFT",
      "token": "3.2490 CDT",
      "timestamp": 1708004454
    }
  ]
```

### Trading

To trade, you need to send a token transfer to the exchange's smart contract. If the token is CFF, you must specify the pool token's smart contract in the memo.
for example:

- to trade **TRXTEST**, send **CFF** with the memo ``tokenrerer11``
- to trade **CFF**, send **TRXTEST** with an ``empty memo``

to exchange one token for another, send the tokens and specify the target token's contract in the memo.
for example:
- to exchange **TRXTEST** for **USDTEST**, send **TRXTEST** with the memo ``tokenrerer11``

## Action '**Withdraw**'

- **Account Name**: owner
- **Contract Name**: pool contract
- **Id**: uint64_t ID of the pool share in the pooled.id table

### Example

```
{  
	account: "tokenrerere2",  
	contract: "gf.cdt",  
	id: 123  
}
```
```
withdraw '[ "tokenrerere2", "gf.cdt", 123 ]'
```

## Action '**Tokenback**'

- **Account Name**: owner
- **Contract Name**: all tokens in the balances.balance[i].contract table
- **Asset Quantity**: amount

### Example

```
{  
	account: "tokenrerere2",  
	contract: "eosio.token",  
	quantity: "1.0000 CFF"  
}
```
```
tokenback '[ "tokenrerere2", "eosio.token", "1.0000 CFF" ]'
```
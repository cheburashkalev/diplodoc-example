# DEX API

## Exchange Workflow

### Creating a Pool
```
gf.dex create [ "useraccount", "gf.eth", "8,ETH", "3.2500 GFT" ]
```
``Token Contract | Action | [ User | Token Account | Token Symbol | Token Price ]``

### Depositing Balance to the Exchange
```
gf.eth transfer '[ "useraccount", "gf.dex", "10.10000000 ETH", "add_balance" ]'
```
``Token Contract | Action | [ User | Exchange Account | Transfer Amount | Memo with Deposit Identifier ]``

### Transferring Funds from User Balance to Pool
```
gf.dex deposit '[ "useraccount", "gf.eth", "20.0000 GFL" ]'
```
``Exchange Contract | Action | [ User | Token Account | Amount ]``

### Trading
```
eosio.token transfer '[ "useraccount", "gf.eth", "0.6000 GFL", "gf.trx" ]'
```
``Token Contract | Action | [ User | Exchange Account | Exchange Amount | Memo with "Token Account for Exchange" parameters ]``
- Exchange TRX to GFL (by market) - do not specify anything in the memo
- Exchange TRX to ETH - specify **gf.eth** (exchange contract) in the memo
-  Exchange GFL to TRX - specify **gf.trx** (exchange contract) in the memo

###  Withdrawing Free Tokens from the Exchange Balance
```
gf.dex withdraw '[ "useraccount", "gf.eth", " 0.10000000 ETH"]'
```
``Exchange Contract | Action | [ User | Token Contract | Withdrawal Amount from the balance table `balance.quantity` ]``


## Action '**Create**'

- **Account name**: owner
- **Contract name**: pool token contract
- **Symbol ticker**: pool token symbol
- **Asset price**: starting price of the pool

#### Example
```json
{
  "account": "useraccount",
  "contract": "gf.eth",
  "ticker": "8,ETH",
  "price": "665.0000 GFL"
}
```

After creation, the pool is available in the pools table:
```json
"rows": [{
      "contract": "gf.eth",
      "owner": "poolowneracc",
      "ticker": "6,ETH",
      "price": "72.4164 GFL",
      "v_price": "7241641917",
      "token": "23.04200094 ETH",
      "v_token": 230420009486,
      "market": "1668.6260 GFL",
      "v_market": "166862600000",
      "lp": 9167.968574
    }
  ]
```

## Balance Refill

- **Memo** - ``add_balance``
- **Table** - ``balance``

#### Example
``https://history.dev.globalforce.io/v1/chain/get_table_rows?code=gf.dex&scope=useraccount&table=balance&json=true&lower_bound=useraccount&limit=2``

```json
"rows": [{
      "contract": "gf.eth",
      "quantity": "4995.26000034 ETH",
    },{
      "contract": "eosio.token",
      "quantity": "1100.0000 GFL"
    }
  ]

```

## Action '**Deposit**'

- **Account Name**: owner
- **Contract Name**: pool token contract
- **Symbol Market**: the amount of GFL tokens being added to the pool. The amount of paired tokens is calculated in the smart contract and deducted from the balance table.  

#### Example
```json
{  
	"account": "tokenrerere2",  
	"contract": "gf.eth",  
	"market": "105.0000 GFL"  
}  
```

## Pooled

After adding to the pool, a new object is added to the pooled table

- **Table** - ``pooled``

#### Example

``https://history.dev.globalforce.io/v1/chain/get_table_rows?code=gf.dex&scope=gf.eth&table=pooled&index_position=2&key_type=i64&json=true&lower_bound=testdexacco1&limit=10``

```json
"rows": [{
      "owner": "gf",
      "lp": "15253.4527 LP",
      "timestamp": 1708004454
    }
  ]

```

## Action '**Outpool**'

- **Account Name**: owner
- **Contract Name**: pool contract
- **Asset Lp**: percentage of its part of the pool in the pooled table

#### Example

```json
{  
	"account": "tokenrerere2",  
	"contract": "gf.eth",
	"quantity": "5.0000 LP"
}
```
```
outpool '[ "tokenrerere2", "gf.eth", 5.00 ]'
```

## Action '**Withdraw**'

- **Account Name**: owner
- **Contract Name**: pool contract
- **Quantity**: Total sum

#### Example

```json
{  
	"account": "useraccount",  
	"contract": "eosio.token",
	"quantity": "1.0000 GFL"
}
```
```
withdraw '[ "tokenrerere2", "eosio.token", "1.0000 GFL" ]'
```
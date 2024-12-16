# HOLD

## Stake token
```
gf.hold stake [ "useraccount", "3.2500 GFL", "" ]
```
``Contract | Action | [ User | Token Amount, Memo (Optional) ]``

## Unstake token
```
gf.hold unstake '[ "gf", "1000000.0000 GFL"]'
```
``Contract | Action | [ User | Token Amount ]``

## Token giveaway
```
eosio.token transfer '[ "useraccount", "gf.hold", "10.5000 GFL", "applystake"]'
```
``Contract | Action | [ User | Stake Account | Quantity | Memo]``
## Take reward
```
gf.hold claim '[ "useraccount" ]'
```
``Exchange Contract | Action | [ User ]``

## Action '**Stake**'
- **Account from**: user
- **Quantity**: amount of tokens
- **Memo**: memo (optional)

#### Example
```json
{
  "from": "useraccount",
  "quantity": "665.0000 GFL",
  "memo": ""
}
```

After stake balance is ready to check in table ``stake``:
``https://history.dev.globalforce.io/v1/chain/get_table_rows?code=gf.hold&scope=gf.hold&table=stake&json=true&lower_bound=useraccount&limit=1``

```json
"rows": [{
      "account": "useraccount",				
      "staked": "72.4164 GFL",				
      "rewards": [{							
		"contract":"eosio.token",
		"quantity":"304029.9408 GFT"
	  }],
      "claim": [{
		"contract":"eosio.token",
		"quantity":"113538879.3409 GFL"
	  }],
      "unstake": "0.0000 GFL",
      "unstake_time": "1668626000"
    }
  ]
```

## Action '**Unstake**'
- **Account from**: user
- **Quantity**: amount of tokens


#### Example
```json
{
  "from": "useraccount",
  "quantity": "665.0000 GFL",
}
```

After unstake data is available in table ``stake``:
``https://history.dev.globalforce.io/v1/chain/get_table_rows?code=gf.hold&scope=gf.hold&table=stake&json=true&lower_bound=useraccount&limit=1``

```json
"rows": [{
      "account": "useraccount",		
      "staked": "72.4164 GFL",		
      "rewards": [{					
		"contract":"eosio.token",
		"quantity":"304029.9408 GFT"
	  }],
      "claim": [{							
		"contract":"eosio.token",
		"quantity":"113538879.3409 GFL"
	  }],
      "unstake": "0.0000 GFL",
      "unstake_time": "1668626000"
    }
  ]
```

## Action '**Claim**'
- **Account**: user

```json
{
  "account": "useraccount"
}

``https://history.dev.globalforce.io/v1/chain/get_table_rows?code=gf.hold&scope=gf.hold&table=stake&json=true&lower_bound=useraccount&limit=1``

```json
"rows": [{
      "account": "useraccount",		
      "staked": "72.4164 GFL",		
      "rewards": [{					
		"contract":"eosio.token",
		"quantity":"304029.9408 GFT"
	  }],
      "claim": [{
		"contract":"eosio.token",
		"quantity":"113538879.3409 GFL"
	  }],
      "unstake": "0.0000 GFL",			
      "unstake_time": "1668626000"		
    }
  ]
```
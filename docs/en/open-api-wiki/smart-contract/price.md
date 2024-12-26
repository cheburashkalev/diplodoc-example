# Price

## Adding a token for price monitoring
```
gf.price create '[ "eosio.token", "4,USDT", "4,GFL", 4]'
```
``Contract | Action | [ Token Contract | Pair Symbol | Token Symbol | Number of decimal places ]``

## Token price update
```
gf.price update '[ "eosio.token", "0.0011 USDT"]'
```
``Contract | Action | [ Token Contract | Token Price ]``
## Token deletion
```
gf.price remove '[ "eosio.token" ]'
```
``Contract | Action | [ Token Contract ]``

## Action '**Create**'

- **contract**: Token Contract
- **token**: Pair Symbol
- **trade**: Token Symbol
- **decimal**: Number of decimal places (int)

#### Example
```json
{
    "contract": "eosio.token",
	"token": "4,GFL",
	"trade": "",
    "decimal": 4
}
```

## Action '**Update**'

- **contract**: Token Contract
- **price**: Token Price

#### Example
```json
{
    "contract": "eosio.token",
	"price": "0.0011 USDT"
}
```

## Action '**Remove**'

- **contract**: Token Contract

#### Example
```json
{
    "contract": "eosio.token"
}
```

## Prices

``https://history.dev.globalforce.io/v1/chain/get_table_rows?code=gf.price&scope=gf.price&table=prices&json=true&limit=500``
``https://history.dev.globalforce.io get table gf.price gf.price prices``

```json
"rows": [{
    "contract": "eosio.token",
    "trade": "GFL",
    "decimal": 4,
    "price": "0.1005 USDT",
    "last_update": 1730100204
	}
  ]
```

## Price Rates

``https://history.dev.globalforce.io/v1/chain/get_table_rows?code=gf.price&scope=gf.price&table=rates&json=true&lower_bound=eosio.token&limit=1``
``https://history.dev.globalforce.io get table gf.price gf.price rates``

```json
"rows": [{
    "contract": "eosio.token",
    "rate": [
			{
				"contract": "eosio.token",
				"price": "0.1005 USDT",
				"last_update": 1730100204
			}
		],
		"last_update": 1730100204
	}
  ]
```

## Price Config

``https://history.dev.globalforce.io/v1/chain/get_table_rows?code=gf.price&scope=gf.price&table=config&json=true&limit=500``
``https://history.dev.globalforce.io get table gf.price gf.price config``

```json
 "rows": [{
		"contract": "eosio.token",
		"token": "GFL",
		"decimal": 4,
		"networks": [
			{
				"network": "GF",
				"transfer": 0,
				"swapout": 0
			}
		]
	}
  ]
```
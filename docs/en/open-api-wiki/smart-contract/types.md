# Types

## Creating a network record
```
gf.types create '[ "ETHEREUM", "ETH", "https://etherscan.io/tx/","https://etherscan.io/address/" ]'
```
``Contract | Action | [ Network | Network Type | Transaction URL | Account URL ]``

## Network record update
```
gf.types update '[ "ETHEREUM", "ETH", "https://etherscan.io/tx/","https://etherscan.io/address/" ]'
```
``Contract | Action | [ Network | Network Type | Transaction URL | Account URL ]``

## Deletion of network record
```
gf.types remove '[ 1 ]''
```
``Contract | Action | [ Network ID ]``

## Action '**Create**'

- **NETNAME**: Network name
- **TYPE**: Network type
- **EXPLORER**: Transaction URL
- **ADDRESS**: Account URL

#### Example
```json
{
    "NETNAME": "ETHEREUM",
    "TYPE": "ETH",
    "EXPLORER": "https://etherscan.io/tx/",
    "ADDRESS": "https://etherscan.io/address/"
}
```

## Action '**Update**'

- **NETNAME**: Network name
- **TYPE**: Network type
- **EXPLORER**: Transaction URL
- **ADDRESS**: Account URL

#### Example
```json
{
    "NETNAME": "ETHEREUM",
    "TYPE": "ETH",
    "EXPLORER": "https://etherscan.io/tx/",
    "ADDRESS": "https://etherscan.io/address/"
}
```

## Action '**Remove**'

- **id**: Network ID (uint64)

#### Example
```json
{
    "id": 2
}
```

``https://history.dev.globalforce.io/v1/chain/get_table_rows?code=gf.types&scope=gf.types&table=types&json=true&limit=500``

``https://history.dev.globalforce.io get table gf.types gf.types types``

```json
"rows": [
	  {
		"id": 1,
		"NETNAME": "GF",
		"TYPE": "GF",
		"EXPLORER": "https://globalforce.io/transaction/",
		"ADDRESS": "https://globalforce.io/account/"
	  },
	  {
		"id": 2,
		"NETNAME": "BITCOIN",
		"TYPE": "BTC",
		"EXPLORER": "https://www.blockchain.com/btc/tx/",
		"ADDRESS": "https://www.blockchain.com/explorer/addresses/btc/"
	  }
	]
```
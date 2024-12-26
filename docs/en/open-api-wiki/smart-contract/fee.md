# Fees

## Creating a record of the amount of fees
```
gf.fee create '[ "ETHEREUM", "ETH", "gf.eth", "8,ETH" ]'
```
``Contract | Action | [ Network | Network Type | Token Contract | Symbol ]``

## Updating the record of fees
```
gf.fee update '[ 2, "0.00000124 ETH" ]'
```
``Contract | Action | [ Network Id | Network Fee ]``

## Removing of fees records
```
gf.fee remove '[ 2 ]'
```
``Contract | Action | [ Network Id ]``

## Action '**Create**'

- **NETNAME**: Network name
- **TYPE**: Network type
- **contract**: Contract name
- **token**: Symbol

#### Example
```json
{
  "NETNAME": "ETHEREUM",
    "TYPE": "ETH",
    "contract": "gf.eth",
    "token": "8,ETH"
}
```

## Action '**Update**'

- **id**: Network ID (uint64)
- **fee**: Network fees

#### Example
```json
{
	"id": 2,
	"fee": "0.00000124 ETH"
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

``https://history.dev.globalforce.io/v1/chain/get_table_rows?code=gf.fee&scope=gf.fee&table=fees&json=true&limit=500``

```json
"rows": [{
      "id": "1",						
      "NETNAME": "ETHEREUM",
	  "TYPE": "ETH",
	  "contract": "gf.eth",
	  "fee": "0.00002400 ETH"
    }
  ]
```
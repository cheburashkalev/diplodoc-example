# Address

## Address Creation
```
gf.address create '[ "gf", [{ "network":"ETHEREUM", "type":"ETH", "address":"0x0000000000000000000000000000000000000001" }]]'
```
``Contract | Action | [ User | Address array ]``

## Address Update
```
gf.address update '[ "gf", [{ "network":"ETHEREUM", "type":"ETH", "address":"0x0000000000000000000000000000000000000001" }]]'
```
``Contract | Action | [ User | Address array ]``

## Address Remove
```
gf.address remove '[ "gf" ]'
```
``Contract | Action | [ User ]``

## Action '**Create**'

- **account**: Account name
- **address[]**: Address array

#### Example
```json
{
  "account": "gf",
  "address": [ 
      { 
        "network":"ETHEREUM", 
        "type":"ETH", 
        "address":"0x0000000000000000000000000000000000000001" 
      }
    ]
}
```

## Action '**Update**'

- **account**: Account name
- **address[]**: Address array

#### Example
```json
{
  "account": "gf",
  "address": [ 
      { 
        "network":"ETHEREUM", 
        "type":"ETH", 
        "address":"0x0000000000000000000000000000000000000001" 
      }
    ]
}
```

## Action '**Remove**'

- **account**: Account name

#### Example
```json
{
  "account": "gf"
}
```

``https://history.dev.globalforce.io/v1/chain/get_table_rows?code=gf.address&scope=useraccount&table=address&json=true&lower_bound=gf&limit=1``

``https://history.dev.globalforce.io get table gf.address useraccount address``

```json
"rows": [{
    "contract": "account",
    "address": [{ 
		"network":"ETHEREUM",
		"type":"ETH",
		"address":"0xer718erb8erbr5d4bdfbdf"
	  }],						
    }
  ]
```
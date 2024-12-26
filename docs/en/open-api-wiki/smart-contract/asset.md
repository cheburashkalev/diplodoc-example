# Asset

## Configure the price for storing assets
```
gf.asset configure '["0.0002 GFL", 1024, 102400]'
```
``контракт | экшн | [ цена за байт | минимальный размер байт | максимальный размер байт ]``

## Store asset
```
gf.asset store '[ "useraccount", "useraccount", "/9j/4AAQSkZBAQEASABIAAD/4QAiRXhbjk9eaZ" ]'
```
``контракт | экшн | [ издатель | владелец | ассет base64 ]``

## Destroy asset
```
gf.asset destroy '[ 1 ]'
```
``контракт | экшн | [ id ассета ]``


## Asset owner change
```
gf.asset setowner '[ 1, "useraccount" ]'
```
``контракт | экшн | [ id ассета | новый владелец ]``


## Action '**Configure**'

- **price**: Price per byte
- **min_size**: Mininmal byte size (uint64)
- **max_size**: Maximal byte size (uint64)

#### Example
```json
{
    "price": "0.0002 GFL",
	"min_size": 1024,
	"max_size": 102400
}
```

## Action '**Store**'

- **issuer**: Asset issuer
- **owner**: Asset owner
- **base64**: Asset (base64 encoding)

#### Example
```json
{
    "issuer": "useraccount",
	"owner": "useraccount",
	"base64": "/9j/4AAQSkZBAQEASABIAAD/4QAiRXhbjk9eaZ"
}
```

## Action '**Destroy**'

- **asset_id**: Asset id (uint64)

#### Example
```json
{
    "asset_id": 1
}
```

## Action '**Setowner**'

- **asset_id**: Asset id (uint64)
- **owner**: New asset owner

#### Example
```json
{
    "asset_id": 1,
    "owner": "useraccount"
}
```

## Asset Config

``https://history.dev.globalforce.io/v1/chain/get_table_rows?code=gf.asset&scope=gf.asset&table=config&json=true&limit=1``
``https://history.dev.globalforce.io get table gf.asset gf.asset config``

```json
"rows": [{
		"id": 1,
		"pricebyte": "0.0002 GFL",
		"min_size": 1024,
		"max_size": 409600,
		"last_update": 1728314164
	}
  ]

```

## Asset Imagestore

``https://history.dev.globalforce.io/v1/chain/get_table_rows?code=gf.asset&scope=gf.asset&table=imagestore&json=true&limit=1``
``https://history.dev.globalforce.io get table gf.asset gf.asset imagestore``

```json
"rows": [{
		"asset_id": 1,
		"owner": "onenewaccnt1",
		"paid": "0.2544 GFL",
		"base64": "iVBORw0KVIolgAAAABJRU5ErkJggg==",
		"last_update": 1694878787
	}
  ]
```
# KYC

## Add check status
```
gf.kyc add '[ "useraccount", 1, "completed" ]'
```
``Contract | Action | [ User Account | KYC Level | KYC Status ]``

## Delete check status
```
gf.kyc del '[ "useraccount" ]'
```
``Contract | Action | [ User Account ]``

## Action '**Add**'

- **account**: User Account
- **level**: KYC Level (int32)
- **status**: KYC Status

#### Example
```json
{
    "account": "useraccount",
	"level": 1,
	"status": "completed"
}
```

## Action '**Del**'

- **account**: User Account

#### Example
```json
{
    "account": "useraccount"
}
```

``https://history.dev.globalforce.io/v1/chain/get_table_rows?code=gf.kyc&scope=gf.kyc&table=accounts&json=true&lower_bound=useraccount&limit=1``
``https://history.dev.globalforce.io get table gf.kyc gf.kyc accounts``

```json
"rows": [{
		"account": "useraccount",
		"status_level1": "completed",
		"status_level2": "",
		"status_level3": ""
	}
  ]
```
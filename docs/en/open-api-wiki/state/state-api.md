
# State API

## Servers
- **Production**: `https://history.globalforce.io/api`
- **Development**: `https://history.dev.globalforce.io/api`

## Endpoints

### `/sync`
- **GET**: StateApi status sync
  - **Responses:**
    - `200`: if successful `{"last_block_num":12616900,"head_block_num":19077303,"sync":6460403}`

---

### `/usercount`
- **GET**: User count in network
  - **Responses:**
    - `200`: if successful return `{"usercount":95}`

---

### `/userlist`
- **GET**: User list in network
  - **Parameters:**
    - **skip** (required, integer, int64): The number of users to skip.
      - Example: `1000`
  - **Responses:**
    - `200`: if successful return `[{"account":"eosio.bpay"},{"account":"eosio.vpay"}]`

---

### `/tokenbalance/{token_account}/{token_symbol}/{account_name}`
- **GET**: User token balance
  - **Parameters:**
    - **token_account** (required, string): The token account.
      - Example: `eosio.token`
    - **token_symbol** (required, string): The token symbol.
      - Example: `GFL`
    - **account_name** (required, string): The account name.
      - Example: `todoboostamg`
  - **Responses:**
    - `200`: if successful return `{"balance":"59321693.8766 GFT"}`

---

### `/holdercount/{token_account}/{token_symbol}`
- **GET**: Token holders count
  - **Parameters:**
    - **token_account** (required, string): The token account.
      - Example: `eosio.token`
    - **token_symbol** (required, string): The token symbol.
      - Example: `GFL`
  - **Responses:**
    - `200`: if successful return `{"holders":79}`

---

### `/topholders/{token_account}/{token_symbol}/{limit}`
- **GET**: List topholders of token
  - **Parameters:**
    - **token_account** (required, string): The token account.
      - Example: `eosio.token`
    - **token_symbol** (required, string): The token symbol.
      - Example: `GFL`
    - **limit** (required, integer, int64): The number of top holders to return.
      - Example: `1000`
  - **Responses:**
    - `200`: if successful return `[{"account":"eosio","amount":140000001,"balance":"140000001.0000 GFT"}]`

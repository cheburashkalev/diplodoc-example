# NFT API

## Servers
- **Production:** `https://history.globalforce.io/api/nft`
- **Development:** `https://history.dev.globalforce.io/api/nft`

## Endpoints

### /search

#### **GET**: Find NFT
- **Tags:** NFT search
- **Summary:** Find NFT by various filters and search parameters
- **Operation ID:** `getOrderById`

##### Parameters:
- `by` (required, string, default: `tid`): Filter by specific fields such as `tid`, `cid`, `towner`, `tcreator`, `asset_id`, `sell`, `tstake`, `tfreezetime`, `tlifetime`
  - **Enum:** `tid`, `cid`, `towner`, `tcreator`, `asset_id`, `sell`, `tstake`, `tfreezetime`, `tlifetime`
- `query` (required, string): Search query (e.g., nameaccount)
- `limit` (required, integer): Limit number of results, min: 0, max: 100
- `position` (required, integer): Position in pagination, min: 0
- `sort` (required, string, default: `desc`): Sorting direction
  - **Enum:** `desc`, `asc`
- `sort_key` (optional, string): Sort by field (e.g., `cid`, `towner`, `tcreator`, `asset_id`, etc.)
- `sort_value` (optional, string): Filter value used with `sort_key` (e.g., testtestte44)
- `asset` (optional, boolean): When `true`, response will not contain base64 encoded image

##### Responses:
- **200:** Successful response containing a list of NFT objects.
  - **Content:** `application/json`
  - **Schema:** `NFTresult`

---

### /market

#### **GET**: Collections on market
- **Tags:** NFT collections on market
- **Summary:** Fetch NFT collections on the market
- **Operation ID:** `getMarket`

##### Parameters:
- `limit` (required, integer): Limit number of results, min: 0, max: 100
- `position` (required, integer): Position in pagination, min: 0
- `sort` (required, string, default: `desc`): Sorting direction
  - **Enum:** `desc`, `asc`

##### Responses:
- **200:** Successful response containing a list of NFT collections.
  - **Content:** `application/json`
  - **Schema:** `MARKETresult`

---

### Schemas

#### **NFTresult**
- **Description:** Server response for the NFT search
- **Type:** object
- **Properties:**
  - `total` (integer): Total count of NFTs, example: 18
  - `result` (array): List of NFT objects
    - **Items:** `NFTobject`

#### **MARKETresult**
- **Description:** Server response for market collections
- **Type:** object
- **Properties:**
  - `total` (integer): Total count of collections, example: 18
  - `result` (array): List of market objects
    - **Items:** `MARKETobject`

#### **NFTobject**
- **Description:** NFT object
- **Type:** object
- **Properties:**
  - `tid` (integer): Unique token ID, example: 977
  - `cid` (integer): Collection ID, example: 2
  - `tname` (string): Token name, example: Super Awesome Meme Token
  - `cname` (string): Collection name (max: 128 characters), example: Simple Collections
  - `cdesc` (string): Collection description (max: 1024 characters), example: Descr Collections
  - `cowner` (string): Collection owner, example: testtestte44
  - `towner` (string): Token owner, example: testtestte44
  - `tcreator` (string): Token creator, example: testtestte44
  - `tcreatorfee` (integer): Creator fee percentage, example: 0
  - `turl` (string): URL in token description (optional), example: https://my-aswesome-token.com
  - `asset_id` (integer): Asset ID, example: 1021
  - `base64` (string): Base64 encoded image string, example: iVBORw0KGgoAAAANSUhEUgAAA9QAAAN
  - `sell` (integer): Market flag: 1 if listed for sale, example: 0
  - `price` (string): Sale price, example: 1.0000 GFT
  - `order_id` (integer): Order ID, example: 23
  - `token` (string): Token account, example: eosio.token
  - `tstake` (integer): Stake flag: 1 if staked, example: 0
  - `tfreezetime` (integer): Freeze time in seconds, example: 0
  - `tlifetime` (integer): Token lifetime in seconds, example: 0
  - `idata` (string): Non-overwritable JSON string, example: {}
  - `mdata` (string): Overwritable JSON string, example: {}
  - `last_update` (integer): Token creation timestamp, example: 1694877432

#### MARKETobject
- **Description:** Market collection object
- **Type:** object
- **Properties:**
  - `cid` (integer): Unique collection ID, example: 2
  - `anybody` (integer): Flag for public token creation: 1 if any user can create tokens, example: 0
  - `cname` (string): Collection name, example: Test collection
  - `cocdescwner` (string): Collection owner, example: testtestte44
  - `cdesc` (string): Collection description, example: testtestte44
  - `last_update` (integer): Last update timestamp, example: 1694877432

---
### Example Response Objects:

#### NFT Search Response Example (`NFTresult`)
```json
{
  "total": 18,
  "result": [
    {
      "tid": 977,
      "cid": 2,
      "tname": "Meme NFT Card",
      "cname": "Simple Collections",
      "cdesc": "Descr Collections",
      "cowner": "testtestte44",
      "towner": "testtestte44",
      "tcreator": "testtestte44",
      "tcreatorfee": 0,
      "turl": "https://your-meme.com",
      "asset_id": 1021,
      "base64": "iVBORw0KGgoAAAANSUhEUgAAA9QAAAN",
      "sell": 0,
      "price": "1.0000 GFT",
      "order_id": 23,
      "token": "eosio.token",
      "tstake": 0,
      "tfreezetime": 0,
      "tlifetime": 0,
      "idata": "{}",
      "mdata": "{}",
      "last_update": 1694877432
    }
  ]
}
```
---

#### NFT Market Collections Example (`MARKETresult`)
```json
{
  "total": 18,
  "result": [
    {
      "cid": 2,
      "anybody": 0,
      "cname": "Test colletion",
      "cocdescwner": "testtestte44",
      "cdesc": "testtestte44",
      "last_update": 1694877432
    }
  ]
}
```
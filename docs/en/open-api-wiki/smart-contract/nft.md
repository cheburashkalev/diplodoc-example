# NFT API

## ACTION `cncreate`
**Create a collection.**
- **Parameters:**
  - `cname` (string): Collection name.
  - `anybody` (uint64_t): 
    - `0`: Anyone can create tokens in the collection.
    - `1`: Only the creator can create tokens.
  - `owner` (name): Owner of the collection.
  - `desc` (string): Description of the collection.


## ACTION `cnsetowner`
**Transfer collection ownership.**
- **Parameters:**
  - `id` (uint64_t): Collection ID.
  - `owner` (name): New owner of the collection.

## ACTION `cnedit`
**Edit a collection.**
- **Parameters:**
  - `id` (uint64_t): Collection ID.
  - `cname` (string): New collection name.
  - `desc` (string): New collection description.


## ACTION `issuenft`
**Create an NFT.**
- **Parameters:**
  - `id` (uint64_t): Collection ID.
  - `tname` (string): Token name (not unique).
  - `creatorfee` (uint64_t): Creator fee percentage for sales.
  - `url` (string): Website URL (1–1024 characters).
  - `asset_id` (uint64_t): Asset ID.
  - `freezetime` (uint64_t): Freeze time in seconds. `0` means it's available immediately.
  - `lifetime` (uint64_t): Token lifespan in seconds. `0` means perpetual. Current time + `lifetime` = token expiration.
  - `immutable` (string): Non-updatable data (JSON).
  - `mutables` (string): Updatable data (JSON). Can be changed with `setnftmdata`.


## ACTION `burnnft`
**Burn a token.**
- **Parameters:**
  - `id` (uint64_t): Token ID.

## ACTION `setnftmdata`
**Update token data.**
- **Parameters:**
  - `id` (uint64_t): Token ID.
  - `mutables` (string): Updatable data (JSON).

## ACTION `stakenft`
**Stake a token.**
- **Parameters:**
  - `id` (uint64_t): Token ID.
  - `stake` (uint64_t): Stake flag. Set to `1`.
  - `freezetime` (uint64_t): Freeze timestamp. If staking for 1 minute, set to current timestamp + 60 seconds.

## ACTION `unstakenft`
**Unstake a token.**
- **Parameters:**
  - `id` (uint64_t): Token ID.

## ACTION `setnftowner`
**Transfer token ownership.**
- **Parameters:**
  - `id` (uint64_t): Token ID.
  - `owner` (name): New token owner.

## ACTION `sellnft`
**List a token for sale on the market.**
- **Parameters:**
  - `id` (uint64_t): Token ID.
  - `price` (asset): Sale price in the specified token. Example: `1.0000 GFL`.
  - `token` (name): Token contract for the sale. Example: `eosio.token`.


## ACTION `unsellnft`
**Remove a token from the market.**
- **Parameters:**
  - `id` (uint64_t): Token ID.

---

## Token Purchase

**To purchase a token, transfer the specified amount to the smart contract address with the token order ID in the memo.**

### Example:
- **From**: `testedemonft`  
- **To**: `gf.nft`  
- **Quantity**: `1.0000 USDTEST`  
- **Memo**: `153`

## UI Representation

### Token Data (From the Table):
- **`tid`**: Token ID.
- **`cid`**: Collection ID. *(Can load the collection name and description.)*
- **`tname`**: Token name.
- **`towner`**: Token owner.
- **`tcreator`**: Token creator.
- **`tcreatorfee`**: Creator's sale commission percentage.
- **`turl`**: URL.
- **`asset_id`**: Asset ID.
- **`base64`**: Base64 data.
- **`sell`**: Sale status.
  - `0`:  
    - **Owner View**: Show "Sell" button. Triggers `sellnft` action.  
    - **User View**: Only visible in search results.
  - `1`:  
    - **Owner View**: Show "Remove from Sale" button. Triggers `unsellnft` action.  
    - **User View**: Show "Buy" button to purchase the token.
- **`tstake`**: Stake status.
  - `0`:  
    - **Owner View**: Show "Stake" button. Triggers `stakenft` action.
  - `1`:  
    - **Owner View**: Show "Unstake" button. Triggers `unstakenft` action.
- **`tfreezetime`**: Timestamp.  
  - If non-zero and less than the current time, the following actions are blocked:
    - `stakenft`
    - `unstakenft`
    - `burnnft`
    - `setnftowner`
    - `sellnft`
    - `unsellnft`
    - Token purchase.
- **`tlifetime`**: Lifespan in seconds.  
  - If non-zero:  
    `current_time - (last_update + tlifetime)` = Remaining token lifespan in days, hours, and minutes.
- **`idata`**: Immutable JSON data (if available).
- **`mdata`**: Mutable JSON data (if available).  
  - **Owner View**: Show "Edit" button. Triggers `setnftmdata` action.
- **`last_update`**: Token creation timestamp.
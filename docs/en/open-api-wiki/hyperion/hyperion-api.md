# Hyperion API

## Endpoints

### /v2/history/export_actions

#### **GET**: Request Large Action Data Export
- **Tags:** history
- **Summary:** Request a large export of action data
- **Operation ID:** `exportActions`

##### Responses:
- **200:** Successful response
  - **Description:** Default Response

---

### /v2/history/get_abi_snapshot

#### **GET**: Fetch ABI at Specific Block
- **Tags:** history
- **Summary:** Fetch contract ABI at a specific block
- **Operation ID:** `getAbiSnapshot`

##### Parameters:
- `contract` (required, string): Contract account name
  - **Min Length:** 1
  - **Max Length:** 12
- `block` (optional, integer): Target block number, minimum: 1
- `fetch` (optional, boolean): Indicates whether to fetch the ABI

##### Responses:
- **200:** Successful response
  - **Description:** Default Response

---

### /v2/history/check_transaction

#### **GET**: Check if a Transaction was Included in a Block
- **Tags:** history
- **Summary:** Check the inclusion status of a transaction in a block
- **Operation ID:** `checkTransaction`

##### Parameters:
- `id` (required, string): Transaction ID
  - **Min Length:** 64
  - **Max Length:** 64

##### Responses:
- **200:** Successful response with transaction details
  - **Content:** `application/json`
  - **Schema:** [CheckTransactionResult](#checktransactionresult)

---

### /v2/history/get_actions

#### **GET**: Get Root Actions
- **Tags:** history
- **Summary:** Retrieve actions based on the notified account. This endpoint also supports generic filters based on indexed fields (e.g., `act.authorization.actor=eosio` or `act.name=delegatebw`), combined with an AND operator.
- **Operation ID:** `getActions`

##### Parameters:
- `limit` (optional, integer): Limit of results per page, minimum: 1
- `skip` (optional, integer): Number of results to skip, minimum: 0
- `account` (optional, string): Notified account name, minLength: 1, maxLength: 12
- `track` (optional, string): Total results to track (number or true)
- `filter` (optional, string): Code:name filter, minLength: 3
- `sort` (optional, string): Sort direction
  - **Enum:** `desc`, `asc`, `1`, `-1`
- `after` (optional, string): Filter results after specified date (ISO8601 format)
- `before` (optional, string): Filter results before specified date (ISO8601 format)
- `simple` (optional, boolean): Enable simplified output mode
- `hot_only` (optional, boolean): Search only the latest hot index
- `noBinary` (optional, boolean): Exclude large binary data
- `checkLib` (optional, boolean): Perform reversibility check

##### Responses:
- **200:** Successful response containing action details
  - **Content:** `application/json`
  - **Schema:** [ActionResponse](#actionresponse)

---

### /v2/history/get_created_accounts

#### **GET**: Get Created Accounts
- **Tags:** accounts
- **Summary:** Retrieve all accounts created by a specified creator
- **Operation ID:** `getCreatedAccounts`

##### Parameters:
- `limit` (optional, integer): Limit of results per page, minimum: 1
- `skip` (optional, integer): Number of results to skip, minimum: 0
- `account` (required, string): Creator account name, minLength: 1, maxLength: 12

##### Responses:
- **200:** Successful response containing account creation details
  - **Content:** `application/json`
  - **Schema:** [CreatedAccountsResponse](#createdaccountsresponse)

---

### /v2/history/get_creator

#### **GET**: Get Account Creator
- **Tags:** accounts
- **Summary:** Retrieve the creator of a specified account.
- **Operation ID:** `getCreator`

##### Parameters:
- `account` (required, string): The account name for which to retrieve the creator, minLength: 1, maxLength: 12

##### Responses:
- **200:** Successful response containing creator information
  - **Content:** `application/json`
  - **Schema:** [CreatorResponse](#creatorresponse)

---

### /v2/history/get_deltas

#### **GET**: Get State Deltas
- **Tags:** history
- **Summary:** Retrieve state deltas with optional filtering criteria.
- **Operation ID:** `getDeltas`

##### Parameters:
- `limit` (optional, integer): Limit of results per page, minimum: 1
- `skip` (optional, integer): Number of results to skip, minimum: 0
- `code` (optional, string): Contract account
- `scope` (optional, string): Table scope
- `table` (optional, string): Table name
- `payer` (optional, string): Payer account
- `after` (optional, string): Filter results after specified date (ISO8601 format)
- `before` (optional, string): Filter results before specified date (ISO8601 format)
- `present` (optional, number): Delta present flag

##### Responses:
- **200:** Successful response containing state delta information
  - **Content:** `application/json`
  - **Schema:** [DeltasResponse](#deltasresponse)

---

### /v2/history/get_schedule

#### **GET**: Get Producer Schedule by Version
- **Tags:** history
- **Summary:** Retrieve the producer schedule based on a specified version or filters.
- **Operation ID:** `getSchedule`

##### Parameters:
- `producer` (optional, string): Producer to search by
- `key` (optional, string): Search by key
- `after` (optional, string): Filter results after specified date (ISO8601 format)
- `before` (optional, string): Filter results before specified date (ISO8601 format)
- `version` (optional, integer): Schedule version, minimum: 1

##### Responses:
- **200:** Successful response containing the producer schedule details
  - **Content:** `application/json`
  - **Schema:** [ScheduleResponse](#scheduleresponse)

---

### /v2/history/get_table_state

#### **GET**: Get Table State at Specific Block Height
- **Tags:** history
- **Summary:** Retrieve the state of a specified table at a certain block height.
- **Operation ID:** `getTableState`

##### Parameters:
- `code` (required, string): Contract to search by
- `table` (required, string): Table to search by
- `block_num` (optional, integer): Target block, minimum: 1
- `after_key` (optional, string): Last key for pagination

##### Responses:
- **200:** Successful response containing table state information
  - **Content:** `application/json`
  - **Schema:** [TableStateResponse](#tablestateresponse)

---

### /v2/history/get_transaction

#### **GET**: Get Transaction by ID
- **Tags:** history
- **Summary:** Retrieve all actions within a transaction by transaction ID.
- **Operation ID:** `getTransaction`

##### Parameters:
- `id` (required, string): Transaction ID
- `block_hint` (optional, integer): Block hint to speed up transaction recovery

##### Responses:
- **200:** Successful response containing transaction details
  - **Content:** `application/json`
  - **Schema:** [TransactionResponse](#transactionresponse)

---

### /v2/history/get_transaction_legacy

#### **GET**: Get Transaction by ID (Legacy)
- **Tags:** history
- **Summary:** Retrieve all actions within a transaction by transaction ID (legacy endpoint).
- **Operation ID:** `getTransactionLegacy`

##### Parameters:
- `id` (required, string): Transaction ID

##### Responses:
- **200:** Successful response containing transaction details
  - **Content:** `application/json`
  - **Schema:** [TransactionResponse](#transactionresponse)

---

### /v2/state/get_account

#### **GET**: Get Account Summary
- **Tags:** accounts
- **Summary:** Retrieve summary data of an account, including tokens and actions.
- **Operation ID:** `getAccount`

##### Parameters:
- `limit` (optional, integer): Limit of results per page, minimum: 1
- `skip` (optional, integer): Number of results to skip, minimum: 0
- `account` (required, string): Account name, minLength: 1, maxLength: 12

##### Responses:
- **200:** Successful response containing account details
  - **Content:** `application/json`
  - **Schema:** [AccountSummaryResponse](#accountsummaryresponse)

---

### /v2/state/get_key_accounts

#### **GET**: Get Accounts by Public Key
- **Tags:** accounts
- **Summary:** Retrieve a list of accounts associated with a specific public key.
- **Operation ID:** `getKeyAccounts`

##### Parameters:
- `limit` (optional, integer): Limit of results per page, minimum: 1
- `skip` (optional, integer): Number of results to skip, minimum: 0
- `public_key` (required, string): Public key for account lookup
- `details` (optional, boolean): Include permission details if set to true

##### Responses:
- **200:** Successful response containing account details
  - **Content:** `application/json`
  - **Schema:** [KeyAccountsResponse](#keyaccountsresponse)

#### **POST**: Get Accounts by Public Key
- **Tags:** accounts, state
- **Summary:** Retrieve accounts associated with a public key through a POST request.
- **Operation ID:** `postKeyAccounts`

##### Parameters:
- `body` (required, object): JSON object with a public key
  - **Schema**:
    - `public_key` (required, string): Public key for account lookup

##### Responses:
- **200:** Successful response containing account names
  - **Content:** `application/json`
  - **Schema:** [KeyAccountsResponse](#keyaccountsresponse)

---

### /v2/state/get_links

#### **GET**: Get Permission Links
- **Tags:** accounts
- **Summary:** Retrieve permission links for an account.
- **Operation ID:** `getPermissionLinks`

##### Parameters:
- `account` (optional, string): Account name
- `code` (optional, string): Contract name
- `action` (optional, string): Method or action name
- `permission` (optional, string): Permission name

##### Responses:
- **200:** Successful response containing permission link details
  - **Content:** `application/json`
  - **Schema:** [PermissionLinksResponse](#permissionlinksresponse)

---

### /v2/state/get_proposals

#### **GET**: Get Proposals
- **Tags:** system
- **Summary:** Retrieve a list of proposals.
- **Operation ID:** `getProposals`

##### Parameters:
- `proposer` (optional, string): Filter by proposer name
- `proposal` (optional, string): Filter by proposal name
- `account` (optional, string): Filter by requested or provided account
- `requested` (optional, string): Filter by requested account
- `provided` (optional, string): Filter by provided account
- `executed` (optional, boolean): Filter by execution status
- `track` (optional, string): Track total results (as number or "true")
- `skip` (optional, integer): Number of actions to skip, minimum: 0
- `limit` (optional, integer): Limit of actions per page, minimum: 1

##### Responses:
- **200:** Successful response containing proposal data
  - **Content:** `application/json`
  
---

### /v2/state/get_voters

#### **GET**: Get Voters
- **Tags:** system
- **Summary:** Retrieve a list of voters.
- **Operation ID:** `getVoters`

##### Parameters:
- `limit` (optional, integer): Limit of results per page, minimum: 1
- `skip` (optional, integer): Number of results to skip, minimum: 0
- `producer` (optional, string): Filter by voted producer (comma-separated), max length: 12

##### Responses:
- **200:** Successful response containing voter data
  - **Content:** `application/json`
  - **Schema:** [VotersResponse](#votersresponse)

---

### /v2/state/get_tokens

#### **GET**: Get Tokens
- **Tags:** accounts
- **Summary:** Retrieve a list of tokens associated with an account.
- **Operation ID:** `getTokens`

##### Parameters:
- `limit` (optional, integer): Limit of results per page, minimum: 1
- `skip` (optional, integer): Number of results to skip, minimum: 0
- `account` (required, string): Account name to retrieve tokens for, min length: 1, max length: 12

##### Responses:
- **200:** Successful response containing token data
  - **Content:** `application/json`

---

### /v2/stats/get_action_usage

#### **GET**: Get Action and Transaction Stats
- **Tags:** stats
- **Summary:** Retrieve action and transaction statistics for a specific period.
- **Operation ID:** `getActionUsage`

##### Parameters:
- `period` (required, string): Time period to analyze (e.g., "1d", "1w")
- `end_date` (optional, string): End date for the analysis period
- `unique_actors` (optional, boolean): Flag to compute unique actors

##### Responses:
- **200:** Successful response containing action usage statistics
  - **Content:** `application/json`

---

### /v2/stats/get_missed_blocks

#### **GET**: Get Missed Blocks
- **Tags:** stats
- **Summary:** Retrieve missed blocks based on various filters.
- **Operation ID:** `getMissedBlocks`

##### Parameters:
- `producer` (optional, string): Filter by producer name
- `after` (optional, string): Filter by date (ISO8601) after specified date
- `before` (optional, string): Filter by date (ISO8601) before specified date
- `min_blocks` (optional, integer): Minimum blocks threshold, minimum: 1

##### Responses:
- **200:** Successful response containing missed blocks data
  - **Content:** `application/json`
  - **Schema:** [MissedBlocksResponse](#missedblocksresponse)

### /v2/stats/get_resource_usage

#### **GET**: Get Resource Usage Stats
- **Tags:** stats
- **Summary:** Retrieve resource usage statistics for a specific action.
- **Operation ID:** `getResourceUsage`

##### Parameters:
- `code` (required, string): Contract code name
- `action` (required, string): Action name to analyze

##### Responses:
- **200:** Successful response containing resource usage stats
  - **Content:** `application/json`

---

### /v1/history/get_actions

#### **POST**: Get Actions
- **Tags:** history
- **Summary:** Legacy endpoint to query actions.
- **Operation ID:** `getActions`

##### Request Body Parameters:
- `account_name` (optional, string): Notified account name, min length: 1, max length: 12
- `pos` (optional, integer): Action position for pagination
- `offset` (optional, integer): Limit of actions per page
- `filter` (optional, string): Code:name filter, min length: 3
- `sort` (optional, string): Sort direction, options: `desc`, `asc`, `1`, `-1`
- `after` (optional, string): Filter actions after specified date (ISO8601)
- `before` (optional, string): Filter actions before specified date (ISO8601)
- `parent` (optional, integer): Filter by parent global sequence, minimum: 0

##### Responses:
- **200:** Successful response containing actions data
  - **Content:** `application/json`
  - **Schema:** [ActionsResponse](#actionsresponse)
---

### /v1/history/get_controlled_accounts

#### **POST**: Get Controlled Accounts
- **Tags:** accounts
- **Summary:** Retrieve controlled accounts by specified controlling accounts.
- **Operation ID:** `getControlledAccounts`

##### Request Body Parameters:
- `controlling_account` (required, string): The controlling account name.

##### Responses:
- **200:** Successful response containing controlled accounts.
  - **Content:** `application/json`
  - **Schema:** [ControlledAccountsResponse](#controlledaccountsresponse)

---

### /v1/history/get_key_accounts

#### **POST**: Get Accounts by Public Key
- **Tags:** accounts
- **Summary:** Retrieve accounts associated with a specific public key.
- **Operation ID:** `getKeyAccounts`

##### Request Body Parameters:
- `public_key` (required, string): The public key to filter accounts.

##### Responses:
- **200:** Successful response containing account names.
  - **Content:** `application/json`
  - **Schema:** [KeyAccountsResponse](#keyaccountsresponse)

---

### /v1/history/get_transaction

#### **POST**: Get Transaction by ID
- **Tags:** history
- **Summary:** Retrieve all actions belonging to a specified transaction.
- **Operation ID:** `getTransaction`

##### Request Body Parameters:
- `id` (required, string): Transaction ID to query.
- `block_num_hint` (optional, integer): Optional block number hint.

##### Responses:
- **200:** Successful response containing transaction data.
  - **Content:** `application/json`

---

### /v1/trace_api/get_block

#### **POST**: Get Block Traces
- **Tags:** history
- **Summary:** Retrieve traces for a specified block.
- **Operation ID:** `getBlock`

##### Request Body Parameters:
- `block_num` (optional, integer): Block number to query.
- `block_id` (optional, string): Block ID to query.

##### Responses:
- **200:** Successful response containing block traces.
  - **Content:** `application/json`
  - **Schema:** [BlockTracesResponse](#blocktracesresponse)

---

### /v1/chain/abi_bin_to_json

#### **GET**: Convert ABI Binary to JSON
- **Tags:** chain
- **Summary:** Returns an object containing rows from the specified table.
- **Operation ID:** `abiBinToJson`

##### Query Parameters:
- `code` (required, string): The code of the contract.
- `action` (required, string): The action to perform.
- `binargs` (required, string): Hexadecimal arguments.

##### Responses:
- **200:** Successful response containing the requested data.
  - **Content:** `application/json`

---

#### **HEAD**: Convert ABI Binary to JSON
- Same as the GET request above.

##### Responses:
- **200:** Successful response containing the requested data.
  - **Content:** `application/json`

---

#### **POST**: Convert ABI Binary to JSON
- **Tags:** chain
- **Summary:** Returns an object containing rows from the specified table.
- **Operation ID:** `abiBinToJsonPost`

##### Request Body Parameters:
- `code` (required, string): The code of the contract.
- `action` (required, string): The action to perform.
- `binargs` (required, string): Hexadecimal arguments.

##### Responses:
- **200:** Successful response containing the requested data.
  - **Content:** `application/json`

---

### /v1/chain/abi_json_to_bin

#### **GET**: Convert JSON object to binary
- **Tags:** chain
- **Summary:** Convert JSON object to binary.
- **Operation ID:** `abiJsonToBinGet`

##### Query Parameters:
- `binargs` (required, string): Hexadecimal representation of the binary arguments. Must match the pattern `^(0x)(([0-9a-f][0-9a-f])+)?$`.

##### Responses:
- **200:** Default Response.

---

#### **HEAD**: Convert JSON object to binary
- **Tags:** chain
- **Summary:** Convert JSON object to binary.
- **Operation ID:** `abiJsonToBinHead`

##### Query Parameters:
- `binargs` (required, string): Hexadecimal representation of the binary arguments. Must match the pattern `^(0x)(([0-9a-f][0-9a-f])+)?$`.

##### Responses:
- **200:** Default Response.

---

#### **POST**: Convert JSON object to binary
- **Tags:** chain
- **Summary:** Convert JSON object to binary.
- **Operation ID:** `abiJsonToBinPost`

##### Request Body Parameters:
- `binargs` (required, string): Hexadecimal representation of the binary arguments. Must match the pattern `^(0x)(([0-9a-f][0-9a-f])+)?$`.

##### Responses:
- **200:** Default Response.

---

### /v1/chain/get_abi

#### **GET**: Retrieves the ABI for a contract based on its account name
- **Tags:** chain
- **Summary:** Retrieves the ABI for a contract based on its account name.
- **Operation ID:** `getAbiGet`

##### Query Parameters:
- `account_name` (required, string): The account name of the contract.

##### Responses:
- **200:** Default Response.

---

#### **HEAD**: Retrieves the ABI for a contract based on its account name
- **Tags:** chain
- **Summary:** Retrieves the ABI for a contract based on its account name.
- **Operation ID:** `getAbiHead`

##### Query Parameters:
- `account_name` (required, string): The account name of the contract.

##### Responses:
- **200:** Default Response.

---

#### **POST**: Retrieves the ABI for a contract based on its account name
- **Tags:** chain
- **Summary:** Retrieves the ABI for a contract based on its account name.
- **Operation ID:** `getAbiPost`

##### Request Body Parameters:
- `account_name` (required, string): The account name of the contract.

##### Responses:
- **200:** Default Response.

---

### /v1/chain/get_account

#### **GET**: Returns an object containing various details about a specific account on the blockchain.
- **Tags:** chain
- **Summary:** Returns an object containing various details about a specific account on the blockchain.
- **Operation ID:** `getAccountGet`

##### Query Parameters:
- `account_name` (required, string): The account name to retrieve details for.

##### Responses:
- **200:** Default Response.

---

#### **HEAD**: Returns an object containing various details about a specific account on the blockchain.
- **Tags:** chain
- **Summary:** Returns an object containing various details about a specific account on the blockchain.
- **Operation ID:** `getAccountHead`

##### Query Parameters:
- `account_name` (required, string): The account name to retrieve details for.

##### Responses:
- **200:** Default Response.

---

#### **POST**: Returns an object containing various details about a specific account on the blockchain.
- **Tags:** chain
- **Summary:** Returns an object containing various details about a specific account on the blockchain.
- **Operation ID:** `getAccountPost`

##### Request Body Parameters:
- `account_name` (required, string): The account name to retrieve details for.

##### Responses:
- **200:** Default Response.

---

### /v1/chain/get_activated_protocol_features

#### **GET**: Retrieves the activated protocol features for producer node
- **Tags:** chain
- **Summary:** Retrieves the activated protocol features for producer node.
- **Operation ID:** `getActivatedProtocolFeaturesGet`

##### Query Parameters:
- `lower_bound` (optional, integer): Lower bound for the query.
- `upper_bound` (optional, integer): Upper bound for the query.
- `limit` (optional, integer): The limit, default is 10.
- `search_by_block_num` (optional, boolean): Flag to indicate it should search by block number.
- `reverse` (optional, boolean): Flag to indicate it should search in reverse.

##### Responses:
- **200:** Default Response.

---

#### **HEAD**: Retrieves the activated protocol features for producer node
- **Tags:** chain
- **Summary:** Retrieves the activated protocol features for producer node.
- **Operation ID:** `getActivatedProtocolFeaturesHead`

##### Query Parameters:
- `lower_bound` (optional, integer): Lower bound for the query.
- `upper_bound` (optional, integer): Upper bound for the query.
- `limit` (optional, integer): The limit, default is 10.
- `search_by_block_num` (optional, boolean): Flag to indicate it should search by block number.
- `reverse` (optional, boolean): Flag to indicate it should search in reverse.

##### Responses:
- **200:** Default Response.

---

#### **POST**: Retrieves the activated protocol features for producer node
- **Tags:** chain
- **Summary:** Retrieves the activated protocol features for producer node.
- **Operation ID:** `getActivatedProtocolFeaturesPost`

##### Request Body Parameters:
- `lower_bound` (optional, integer): Lower bound for the query.
- `upper_bound` (optional, integer): Upper bound for the query.
- `limit` (optional, integer): The limit, default is 10.
- `search_by_block_num` (optional, boolean): Flag to indicate it should search by block number.
- `reverse` (optional, boolean): Flag to indicate it should search in reverse.

##### Responses:
- **200:** Default Response.

---

### /v1/chain/get_block

#### GET
- **Summary**: Returns an object containing various details about a specific block on the blockchain. 
- **Tags:** chain  

##### **Parameters:**
- `block_num_or_id` (string, required): Provide a `block number` or a `block id`.  

##### **Responses:**
- **200**: Default Response

---

#### HEAD
- **Summary:** Returns an object containing various details about a specific block on the blockchain.  
- **Tags:** chain  

##### **Parameters:**
- `block_num_or_id` (string, required): Provide a `block number` or a `block id`.  

##### **Responses:**
- **200**: Default Response

---

#### POST
- **Summary:** Returns an object containing various details about a specific block on the blockchain.  
- **Tags:** chain  

##### **Parameters:**
- **Body** (object, required):
  - `block_num_or_id` (string, required): Provide a `block number` or a `block id`.  

##### **Responses:**
- **200**: Default Response

---

## /v1/chain/get_block_header_state

### GET

- **Summary:** Retrieves the block header state.  
- **Tags:** chain  

#### **Parameters:**
- `block_num_or_id` (string, required): Provide a block number or a block ID.  

#### **Responses:**
- **200**: Default Response

---

### HEAD

- **Summary:** Retrieves the block header state.  
- **Tags:** chain  

#### **Parameters:**
- `block_num_or_id` (string, required): Provide a block number or a block ID.  

#### **Responses:**
- **200**: Default Response

---

### POST

- **Summary:** Retrieves the block header state.  
- **Tags:** chain  

#### **Parameters:**
- **Body** (object, required):
  - `block_num_or_id` (string, required): Provide a block number or a block ID.  

#### **Responses:**
- **200**: Default Response

---

## /v1/chain/get_code

### GET

- **Summary:** Retrieves contract code.  
- **Tags:** chain  

#### **Parameters:**
- `account_name` (string, required): The name of the account.  
- `code_as_wasm` (integer, required, default: 1): This must be 1 (true).  

#### **Responses:**
- **200**: Default Response

---

### HEAD

- **Summary:** Retrieves contract code.  
- **Tags:** chain  

#### **Parameters:**
- `account_name` (string, required): The name of the account.  
- `code_as_wasm` (integer, required, default: 1): This must be 1 (true).  

#### **Responses:**
- **200**: Default Response

---

### POST

- **Summary:** Retrieves contract code.  
- **Tags:** chain  

#### **Parameters:**
- **Body** (object, required):
  - `account_name` (string, required): The name of the account.  
  - `code_as_wasm` (integer, required, default: 1): This must be 1 (true).  

#### **Responses:**
- **200**: Default Response

---

## /v1/chain/get_currency_balance

### GET

- **Summary:** Retrieves the current balance.  
- **Tags:** chain  

#### **Parameters:**
- `code` (string, required): Currency code.  
- `account` (string, required): Account name.  
- `symbol` (string, required): Token symbol.  

#### **Responses:**
- **200**: Default Response

---

### HEAD

- **Summary:** Retrieves the current balance.  
- **Tags:** chain  

#### **Parameters:**
- `code` (string, required): Currency code.  
- `account` (string, required): Account name.  
- `symbol` (string, required): Token symbol.  

#### **Responses:**
- **200**: Default Response

---

### POST

- **Summary:** Retrieves the current balance.  
- **Tags:** chain  

#### **Parameters:**
- **Body** (object, required):
  - `code` (string, required): Currency code.  
  - `account` (string, required): Account name.  
  - `symbol` (string, required): Token symbol.  

#### **Responses:**
- **200**: Default Response

---

## /v1/chain/get_currency_stats

### GET

- **Summary:** Retrieves currency stats.  
- **Tags:** chain  

#### **Parameters:**
- `code` (string, required): Currency code.  
- `symbol` (string, required): Token symbol.  

#### **Responses:**
- **200**: Default Response

---

### HEAD

- **Summary:** Retrieves currency stats.  
- **Tags:** chain  

#### **Parameters:**
- `code` (string, required): Currency code.  
- `symbol` (string, required): Token symbol.  

#### **Responses:**
- **200**: Default Response

---

### POST

- **Summary:** Retrieves currency stats.  
- **Tags:** chain  

#### **Parameters:**
- **Body** (object, required):
  - `code` (string, required): Currency code.  
  - `symbol` (string, required): Token symbol.  

#### **Responses:**
- **200**: Default Response

---

## /v1/chain/get_info

### GET

- **Summary:** Returns an object containing various details about the blockchain.  
- **Tags:** chain  

#### **Responses:**
- **200**: Default Response

---

### HEAD

- **Summary:** Returns an object containing various details about the blockchain.  
- **Tags:** chain  

#### **Responses:**
- **200**: Default Response

---

### POST

- **Summary:** Returns an object containing various details about the blockchain.  
- **Tags:** chain  

#### **Responses:**
- **200**: Default Response

---

## /v1/chain/get_producers

### GET

- **Summary:** Retrieves producers list.  
- **Tags:** chain  

#### **Parameters:**
- `limit` (string, optional): Total number of producers to retrieve.  
- `lower_bound` (string, optional): In conjunction with limit can be used to paginate through the results.  
- `json` (boolean, optional): Return result in JSON format.  

#### **Responses:**
- **200**: Default Response

---

### HEAD

- **Summary:** Retrieves producers list.  
- **Tags:** chain  

#### **Parameters:**
- `limit` (string, optional): Total number of producers to retrieve.  
- `lower_bound` (string, optional): In conjunction with limit can be used to paginate through the results.  
- `json` (boolean, optional): Return result in JSON format.  

#### **Responses:**
- **200**: Default Response

---

### POST

- **Summary:** Retrieves producers list.  
- **Tags:** chain  

#### **Parameters:**
- **Body** (object, required):
  - `limit` (string, optional): Total number of producers to retrieve.  
  - `lower_bound` (string, optional): In conjunction with limit can be used to paginate through the results.  
  - `json` (boolean, optional): Return result in JSON format.  

#### **Responses:**
- **200**: Default Response

---

## /v1/chain/get_raw_abi

### GET

- **Summary:** Retrieves raw ABI for a contract based on account name.  
- **Tags:** chain  

#### **Parameters:**
- `account_name` (string, required): Account name.

#### **Responses:**
- **200**: Default Response

---

### HEAD

- **Summary:** Retrieves raw ABI for a contract based on account name.  
- **Tags:** chain  

#### **Parameters:**
- `account_name` (string, required): Account name.

#### **Responses:**
- **200**: Default Response

---

### POST

- **Summary:** Retrieves raw ABI for a contract based on account name.  
- **Tags:** chain  

#### **Parameters:**
- **Body** (object, required):
  - `account_name` (string, required): Account name.

#### **Responses:**
- **200**: Default Response

---

## /v1/chain/get_raw_code_and_abi

### GET

- **Summary:** Retrieves raw code and ABI for a contract based on account name.  
- **Tags:** chain  

#### **Parameters:**
- `account_name` (string, required): Account name.

#### **Responses:**
- **200**: Default Response

---

### HEAD

- **Summary:** Retrieves raw code and ABI for a contract based on account name.  
- **Tags:** chain  

#### **Parameters:**
- `account_name` (string, required): Account name.

#### **Responses:**
- **200**: Default Response

---

### POST

- **Summary:** Retrieves raw code and ABI for a contract based on account name.  
- **Tags:** chain  

#### **Parameters:**
- **Body** (object, required):
  - `account_name` (string, required): Account name.

#### **Responses:**
- **200**: Default Response

---

## /v1/chain/get_scheduled_transaction

### GET

- **Summary:** Retrieves the scheduled transaction.  
- **Tags:** chain  

#### **Parameters:**
- `lower_bound` (string, optional): Date/time string in the format YYYY-MM-DDTHH:MM:SS.sss.
- `limit` (integer, optional): The maximum number of transactions to return.
- `json` (boolean, optional): Whether the packed transaction is converted to JSON.

#### **Responses:**
- **200**: Default Response

---

### HEAD

- **Summary:** Retrieves the scheduled transaction.  
- **Tags:** chain  

#### **Parameters:**
- `lower_bound` (string, optional): Date/time string in the format YYYY-MM-DDTHH:MM:SS.sss.
- `limit` (integer, optional): The maximum number of transactions to return.
- `json` (boolean, optional): Whether the packed transaction is converted to JSON.

#### **Responses:**
- **200**: Default Response

---

### POST

- **Summary:** Retrieves the scheduled transaction.  
- **Tags:** chain  

#### **Parameters:**
- **Body** (object, required):
  - `lower_bound` (string, optional): Date/time string in the format YYYY-MM-DDTHH:MM:SS.sss.
  - `limit` (integer, optional): The maximum number of transactions to return.
  - `json` (boolean, optional): Whether the packed transaction is converted to JSON.

#### **Responses:**
- **200**: Default Response

---

## /v1/chain/get_table_by_scope

### GET

- **Summary:** Retrieves table scope.  
- **Tags:** chain  

#### **Parameters:**
- `code` (string, required): Name of the contract to return table data for.
- `table` (string, optional): Filter results by table.
- `lower_bound` (string, optional): Filters results to return the first element that is not less than the provided value in the set.
- `upper_bound` (string, optional): Filters results to return the first element that is greater than the provided value in the set.
- `limit` (integer, optional): Limit the number of results returned.
- `reverse` (boolean, optional): Reverse the order of returned results.

#### **Responses:**
- **200**: Default Response

---

### HEAD

- **Summary:** Retrieves table scope.  
- **Tags:** chain  

#### **Parameters:**
- `code` (string, required): Name of the contract to return table data for.
- `table` (string, optional): Filter results by table.
- `lower_bound` (string, optional): Filters results to return the first element that is not less than the provided value in the set.
- `upper_bound` (string, optional): Filters results to return the first element that is greater than the provided value in the set.
- `limit` (integer, optional): Limit the number of results returned.
- `reverse` (boolean, optional): Reverse the order of returned results.

#### **Responses:**
- **200**: Default Response

---

### POST

- **Summary:** Retrieves table scope.  
- **Tags:** chain  

#### **Parameters:**
- **Body** (object, required):
  - `code` (string, required): Name of the contract to return table data for.
  - `table` (string, optional): Filter results by table.
  - `lower_bound` (string, optional): Filters results to return the first element that is not less than the provided value in the set.
  - `upper_bound` (string, optional): Filters results to return the first element that is greater than the provided value in the set.
  - `limit` (integer, optional): Limit the number of results returned.
  - `reverse` (boolean, optional): Reverse the order of returned results.

#### **Responses:**
- **200**: Default Response

---

## /v1/chain/get_table_rows

### GET

- **Summary:** Returns an object containing rows from the specified table.  
- **Tags:** chain  

#### **Parameters:**
- `code` (string, required): The name of the smart contract that controls the provided table.
- `table` (string, required): The name of the table to query.
- `scope` (string, optional): The account to which this data belongs.
- `index_position` (string, optional): Position of the index used; accepted parameters: `primary`, `secondary`, `tertiary`, `fourth`, `fifth`, `sixth`, `seventh`, `eighth`, `ninth`, `tenth`.
- `key_type` (string, optional): Type of key specified by index_position (e.g., `uint64_t` or `name`).
- `encode_type` (string, optional): Encoding type.
- `upper_bound` (string, optional): Upper bound for the query.
- `lower_bound` (string, optional): Lower bound for the query.

#### **Responses:**
- **200**: Default Response

---

### HEAD

- **Summary:** Returns an object containing rows from the specified table.  
- **Tags:** chain  

#### **Parameters:** (Same as GET)

#### **Responses:**
- **200**: Default Response

---

### POST

- **Summary:** Returns an object containing rows from the specified table.  
- **Tags:** chain  

#### **Parameters:**
- **Body** (object, required):
  - `code` (string, required): The name of the smart contract that controls the provided table.
  - `table` (string, required): The name of the table to query.
  - `scope` (string, optional): The account to which this data belongs.
  - `index_position` (string, optional): Position of the index used.
  - `key_type` (string, optional): Type of key specified by index_position.
  - `encode_type` (string, optional): Encoding type.
  - `upper_bound` (string, optional): Upper bound for the query.
  - `lower_bound` (string, optional): Lower bound for the query.

#### **Responses:**
- **200**: Default Response

---

## /v1/chain/push_transaction

### POST

- **Summary:** This method expects a transaction in JSON format and will attempt to apply it to the blockchain.  
- **Tags:** chain  

#### **Parameters:**
- **Body** (object, required):
  - `signatures` (array, required): Array of signatures required to authorize the transaction.
  - `compression` (boolean, optional): Compression used, usually false.
  - `packed_context_free_data` (string, optional): JSON to hex.
  - `packed_trx` (string, required): Transaction object JSON to hex.

#### **Responses:**
- **200**: Default Response

---

## /v1/chain/push_transactions

### POST

- **Summary:** This method expects a transaction in JSON format and will attempt to apply it to the blockchain.  
- **Tags:** chain  

#### **Parameters:**
- **Body** (object, required):
  - `expiration` (integer, required): Transaction expiration time.
  - `ref_block_num` (integer, required): Reference block number.
  - `ref_block_prefix` (integer, required): Reference block prefix.
  - `max_net_usage_words` (integer, required): Maximum net usage in words.
  - `max_cpu_usage_ms` (integer, required): Maximum CPU usage in milliseconds.
  - `delay_sec` (integer, required): Delay in seconds.
  - `context_free_actions` (array, optional): Context-free actions.
  - `actions` (array, required): Actions to be executed.
  - `transaction_extensions` (array, optional): Transaction extensions.

#### **Responses:**
- **200**: Default Response

---

## /v1/chain/send_transaction

### POST

- **Summary:** This method expects a transaction in JSON format and will attempt to apply it to the blockchain.  
- **Tags:** chain  

#### **Parameters:**
- **Body** (object, required):
  - `signatures` (array, required): Array of signatures required to authorize the transaction.
  - `compression` (boolean, optional): Compression used, usually false.
  - `packed_context_free_data` (string, optional): JSON to hex.
  - `packed_trx` (string, required): Transaction object JSON to hex.

#### **Responses:**
- **200**: Default Response

---

## /v1/chain/*

### GET  

- **Summary:** Wildcard chain API handler.  
- **Responses:**
  - **200**: Default Response

---

### POST  

- **Summary:** Wildcard chain API handler.  
- **Responses:**
  - **200**: Default Response

---

## /v1/node/get_supported_apis

### GET  

- **Summary:** Get list of supported APIs.  
- **Responses:**
  - **200**: Default Response


## Schemas

#### **CheckTransactionResult**
- **Description:** Server response for checking transaction inclusion
- **Type:** object
- **Properties**:
  - `query_time_ms` (number): Query time in milliseconds
  - `cached` (boolean): Cached result status
  - `hot_only` (boolean): Hot-only flag
  - `lib` (number): Last irreversible block number
  - `total` (object): Total object
    - **Properties**:
      - `value` (number): Total value
      - `relation` (string): Relation description
  - `id` (string): Transaction ID
  - `status` (string): Transaction status
  - `block_num` (number): Block number containing the transaction
  - `root_action` (object): Root action details
    - **Properties**:
      - `account` (string): Account name
      - `name` (string): Action name
      - `authorization` (array): List of authorizations
        - **Items** (object):
          - `actor` (string): Actor name
          - `permission` (string): Permission level
      - `data` (string): Action data
  - `signatures` (array): List of transaction signatures
    - **Items** (string): Signature string

---

#### **ActionResponse**
- **Description:** Server response for retrieving root actions
- **Type:** object
- **Properties**:
  - `query_time_ms` (number): Query time in milliseconds
  - `cached` (boolean): Cached result status
  - `hot_only` (boolean): Hot-only flag
  - `lib` (number): Last irreversible block number
  - `total` (object): Total object
    - **Properties**:
      - `value` (number): Total value
      - `relation` (string): Relation description
  - `simple_actions` (array): Array of simplified action objects
    - **Items**:
      - `block` (number): Block number
      - `timestamp` (string): Action timestamp
      - `irreversible` (boolean): Irreversibility status
      - `contract` (string): Contract name
      - `action` (string): Action name
      - `actors` (string): List of actors
      - `notified` (string): Notified account
      - `transaction_id` (string): Transaction ID
      - `data` (object): Additional action data (key-value pairs)
  - `actions` (array): Array of action objects
    - **Items**:
      - `@timestamp` (string): Timestamp of action creation
      - `timestamp` (string): Action timestamp
      - `block_num` (number): Block number
      - `block_id` (string): Block ID
      - `trx_id` (string): Transaction ID
      - `act` (object): Action details
        - **Properties**:
          - `account` (string): Account name
          - `name` (string): Action name
          - `authorization` (array): List of authorizations
            - **Items**:
              - `actor` (string): Actor name
              - `permission` (string): Permission level
      - `receipts` (array): Action receipts
        - **Items**:
          - `receiver` (string): Receiver name
          - `global_sequence` (number): Global sequence number
          - `recv_sequence` (number): Receiver sequence number
          - `auth_sequence` (array): Authorization sequences
            - **Items**:
              - `account` (string): Account name
              - `sequence` (number): Sequence number
      - `cpu_usage_us` (number): CPU usage in microseconds
      - `net_usage_words` (number): Network usage in words
      - `account_ram_deltas` (array): Account RAM deltas
        - **Items**:
          - `account` (string): Account name
          - `delta` (number): RAM delta
      - `global_sequence` (number): Global sequence number
      - `producer` (string): Producer name
      - `parent` (number): Parent block number
      - `action_ordinal` (number): Action ordinal
      - `creator_action_ordinal` (number): Creator action ordinal
      - `signatures` (array): List of signatures
        - **Items** (string): Signature

---

#### **CreatedAccountsResponse**
- **Description:** Server response for retrieving created accounts
- **Type:** object
- **Properties**:
  - `query_time_ms` (number): Query time in milliseconds
  - `cached` (boolean): Cached result status
  - `hot_only` (boolean): Hot-only flag
  - `lib` (number): Last irreversible block number
  - `total` (object): Total object
    - **Properties**:
      - `value` (number): Total value
      - `relation` (string): Relation description
  - `query_time` (number): Total query time
  - `accounts` (array): List of created account objects
    - **Items**:
      - `name` (string): Account name
      - `timestamp` (string): Account creation timestamp
      - `trx_id` (string): Transaction ID

---

#### **CreatorResponse**
- **Description:** Server response for retrieving account creator information
- **Type:** object
- **Properties**:
  - `query_time_ms` (number): Query time in milliseconds
  - `cached` (boolean): Cached result status
  - `hot_only` (boolean): Hot-only flag
  - `lib` (number): Last irreversible block number
  - `total` (object): Total object
    - **Properties**:
      - `value` (number): Total value
      - `relation` (string): Relation description
  - `account` (string): Account name
  - `creator` (string): Creator account name
  - `timestamp` (string): Account creation timestamp
  - `block_num` (integer): Block number
  - `trx_id` (string): Transaction ID
  - `indirect_creator` (string): Indirect creator account name

---

#### **DeltasResponse**
- **Description:** Server response for retrieving state deltas
- **Type:** object
- **Properties**:
  - `query_time_ms` (number): Query time in milliseconds
  - `cached` (boolean): Cached result status
  - `hot_only` (boolean): Hot-only flag
  - `lib` (number): Last irreversible block number
  - `total` (object): Total object
    - **Properties**:
      - `value` (number): Total value
      - `relation` (string): Relation description
  - `deltas` (array): List of delta objects
    - **Items**:
      - `timestamp` (string): Delta timestamp
      - `present` (number): Delta present flag
      - `code` (string): Contract account
      - `scope` (string): Table scope
      - `table` (string): Table name
      - `primary_key` (string): Primary key
      - `payer` (string): Payer account
      - `block_num` (number): Block number
      - `block_id` (string): Block ID
      - `data` (object): Delta data, additional properties allowed

---

#### **ScheduleResponse**
- **Description:** Server response for retrieving producer schedule by version
- **Type:** object
- **Properties**:
  - `query_time_ms` (number): Query time in milliseconds
  - `cached` (boolean): Cached result status
  - `hot_only` (boolean): Hot-only flag
  - `lib` (number): Last irreversible block number
  - `total` (object): Total object
    - **Properties**:
      - `value` (number): Total value
      - `relation` (string): Relation description
  - `timestamp` (string): Schedule timestamp
  - `block_num` (number): Block number
  - `version` (number): Schedule version
  - `producers` (array): List of producer objects
    - **Items**:
      - `producer_name` (string): Name of the producer
      - `block_signing_key` (string): Block signing key of the producer
      - `legacy_key` (string): Legacy key of the producer

---

#### **TableStateResponse**
- **Description:** Server response for retrieving the state of a table at a specific block height
- **Type:** object
- **Properties**:
  - `query_time_ms` (number): Query time in milliseconds
  - `cached` (boolean): Cached result status
  - `hot_only` (boolean): Hot-only flag
  - `lib` (number): Last irreversible block number
  - `total` (object): Total object
    - **Properties**:
      - `value` (number): Total value
      - `relation` (string): Relation description
  - `code` (string): Contract code
  - `table` (string): Table name
  - `block_num` (number): Block number
  - `after_key` (string): Last key for pagination
  - `next_key` (string): Next key for pagination
  - `results` (array): List of state entries
    - **Items**:
      - `scope` (string): Table scope
      - `primary_key` (string): Primary key
      - `payer` (string): Payer account
      - `timestamp` (string): Entry timestamp
      - `block_num` (number): Block number
      - `block_id` (string): Block ID
      - `present` (number): Present flag
      - `data` (object): Additional data, additional properties allowed
---

#### **TransactionResponse**
- **Description:** Server response for retrieving transaction details by ID
- **Type:** object
- **Properties**:
  - **Content depends on transaction details and may vary per implementation**

---

#### **AccountSummaryResponse**
- **Description:** Server response for retrieving an account summary
- **Type:** object
- **Properties**:
  - `query_time_ms` (number): Query time in milliseconds
  - `cached` (boolean): Cached result status
  - `hot_only` (boolean): Hot-only flag
  - `lib` (number): Last irreversible block number
  - `total` (object): Total object
    - **Properties**:
      - `value` (number): Total value
      - `relation` (string): Relation description
  - `account` (object): Account details with additional properties allowed
  - `links` (array): List of account link objects
    - **Items**:
      - `timestamp` (string): Link timestamp
      - `permission` (string): Permission level
      - `code` (string): Linked contract code
      - `action` (string): Linked action
  - `tokens` (array): List of token objects
    - **Items**:
      - `symbol` (string): Token symbol
      - `precision` (integer): Decimal precision of token
      - `amount` (number): Token amount
      - `contract` (string): Contract of the token
  - `total_actions` (number): Total actions count
  - `actions` (array): List of action objects
    - **Items**:
      - `@timestamp` (string): Action timestamp
      - `timestamp` (string): Action timestamp (legacy)
      - `block_num` (number): Block number of action
      - `block_id` (string): Block ID
      - `trx_id` (string): Transaction ID
      - `act` (object): Action details
        - **Properties**:
          - `account` (string): Account responsible for action
          - `name` (string): Action name
          - `authorization` (array): Authorization details
            - **Items**:
              - `actor` (string): Authorizing account
              - `permission` (string): Permission level
      - `receipts` (array): Receipt objects associated with action
        - **Items**:
          - `receiver` (string): Receiving account
          - `global_sequence` (number): Global sequence number
          - `recv_sequence` (number): Receive sequence number
          - `auth_sequence` (array): Authorization sequences
            - **Items**:
              - `account` (string): Authorizing account
              - `sequence` (number): Sequence number
      - `cpu_usage_us` (number): CPU usage in microseconds
      - `net_usage_words` (number): Net usage in words
      - `account_ram_deltas` (array): RAM deltas associated with account
        - **Items**:
          - `account` (string): Account affected by RAM delta
          - `delta` (number): RAM delta amount
      - `global_sequence` (number): Global sequence number
      - `producer` (string): Producing account
      - `parent` (number): Parent sequence number
      - `action_ordinal` (number): Action ordinal in transaction
      - `creator_action_ordinal` (number): Ordinal of creator action in transaction
      - `signatures` (array): List of transaction signatures
        - **Items**: String representing a signature

---

#### **KeyAccountsResponse**
- **Description:** Server response containing account names and optional permission details linked to a public key
- **Type:** object
- **Properties**:
  - `account_names` (array): List of account names associated with the public key
    - **Items**: string representing an account name
  - `permissions` (array, optional): Permission details if `details` parameter is true
    - **Items**:
      - `owner` (string): Owner of the permission
      - `block_num` (integer): Block number associated with the permission
      - `parent` (string): Parent permission
      - `last_updated` (string): Last updated timestamp
      - `auth` (object): Authorization details
      - `name` (string): Permission name
      - `present` (number): Presence indicator

---

#### **PermissionLinksResponse**
- **Description:** Server response containing permission link information
- **Type:** object
- **Properties**:
  - `query_time_ms` (number): Query time in milliseconds
  - `cached` (boolean): Cached result status
  - `hot_only` (boolean): Hot-only flag
  - `lib` (number): Last irreversible block number
  - `total` (object): Total object
    - **Properties**:
      - `value` (number): Total value
      - `relation` (string): Relation description
  - `links` (array): List of permission link objects
    - **Items**:
      - `block_num` (number): Block number associated with the link
      - `timestamp` (string): Link timestamp
      - `account` (string): Account name associated with the link
      - `permission` (string): Permission name
      - `code` (string): Contract code
      - `action` (string): Linked action
      - `irreversible` (boolean): Whether the link is irreversible

---

#### **VotersResponse**
- **Type:** object
- **Properties**:
  - `query_time_ms` (number): Query time in milliseconds
  - `cached` (boolean): Indicates if result was cached
  - `hot_only` (boolean): Hot-only status
  - `lib` (number): Last irreversible block number
  - `total` (object): Total results
    - `value` (number): Total count
    - `relation` (string): Description of relation
  - `voters` (array): List of voter objects
    - **Items**:
      - `account` (string): Voter account name
      - `weight` (number): Voting weight
      - `last_vote` (number): Last vote timestamp
      - `data` (object): Additional data (key-value pairs)

---

#### **MissedBlocksResponse**
- **Type:** object
- **Properties**:
  - `query_time_ms` (number): Query execution time in milliseconds
  - `cached` (boolean): Whether the data is cached
  - `hot_only` (boolean): Hot-only data status
  - `lib` (number): Last irreversible block number
  - `total` (object): Total results
    - `value` (number): Count of results
    - `relation` (string): Relation to the total count
  - `stats` (object): Statistics, including data by producer
  - `events` (array): List of missed block events
    - **Items**:
      - `@timestamp` (string): Timestamp of the event
      - `last_block` (number): Last block number
      - `schedule_version` (number): Version of the schedule
      - `size` (number): Size of the missed block data
      - `producer` (string): Producer who missed the block

---

#### **ActionsResponse**
- **Type:** object
- **Properties**:
  - `query_time` (number): Time taken for the query
  - `last_irreversible_block` (number): Last irreversible block number
  - `actions` (array): List of action details
    - **Items**:
      - `account_action_seq` (number): Account action sequence
      - `global_action_seq` (number): Global action sequence
      - `block_num` (number): Block number
      - `block_time` (string): Block time
      - `action_trace` (object): Trace data of the action
        - `action_ordinal` (number): Ordinal of the action
        - `creator_action_ordinal` (number): Ordinal of creator action
        - `receipt` (object): Receipt information
          - `receiver` (string): Receiver name
          - `global_sequence` (number): Global sequence number
          - `recv_sequence` (number): Receiver sequence
          - `auth_sequence` (array): Authorization sequence data
        - `receiver` (string): Receiver of the action
        - `act` (object): Action data
          - `account` (string): Account involved
          - `name` (string): Name of the action
          - `authorization` (array): Authorization details
          - `data` (object): Additional data
          - `hex_data` (string): Hexadecimal representation of data
        - `trx_id` (string): Transaction ID
        - `block_num` (number): Block number where action occurred
        - `block_time` (string): Block time in ISO8601 format

---

### ControlledAccountsResponse
- **Type:** object
- **Properties**:
  - `controlled_accounts` (array): List of controlled accounts.
    - **Items**: (string)

---

### KeyAccountsResponse
- **Type:** object
- **Properties**:
  - `account_names` (array): List of account names associated with the public key.
    - **Items**: (string)

---

### BlockTracesResponse
- **Type:** object
- **Properties**:
  - `query_time_ms` (number): Time taken to execute the query in milliseconds.
  - `cached` (boolean): Whether the response was cached.
  - `hot_only` (boolean): Whether only hot data is included.
  - `lib` (number): Last irreversible block number.
  - `total` (object): Total results.
    - `value` (number): Count of results.
    - `relation` (string): Relation to the total count.
  - `id` (string): Block ID.
  - `number` (integer): Block number.
  - `previous_id` (string): Previous block ID.
  - `status` (string): Block status.
  - `timestamp` (string): Block timestamp in ISO8601 format.
  - `producer` (string): Block producer.
  - `transactions` (array): List of transactions in the block.
    - **Items**:
      - `id` (string): Transaction ID.
      - `actions` (array): List of actions within the transaction.
        - **Items**:
          - `receiver` (string): Receiver of the action.
          - `account` (string): Account initiating the action.
          - `action` (string): Name of the action.
          - `authorization` (array): Authorization details.
            - **Items**:
              - `account` (string): Authorized account.
              - `permission` (string): Required permission.
          - `data` (object): Additional data associated with the action.

# What is the GlobalForce blockchain

Blockchain is decentralized infrastructure software without a centralized, controlling entity. Blockchains are defined differently, but they all share common characteristics: decentralized, immutable, traceable, and transparent.

Transactions are recorded in a block, and the blocks form an immutable chain of historical data due to the fact that each subsequent block seals the previous block using its HASH amount. Thus, it is impossible to make any changes to the previous block. All information in blocks is publicly available at any time, making the history of the blockchain completely transparent.

The GlobalForce blockchain is built on EOSIO and consists of a number of components and libraries that are used to manage blockchain nodes, collect blockchain data, interact with those nodes, and create smart contracts. We use open source software available under free licenses. All rights to the used developments belong to their respective owners.

The main component is ```nodeos``` (node + EOSIO = ```nodeos```). This is the core EOSIO node daemon that can be configured with plugins to run a node. Example uses are block production, dedicated API endpoints, and local development. ```Cleos``` (CLI + EOSIO = ```Cleos```) is a command line interface which interacts with ```nodeos```, allowing you to send commands and actions to a blockchain. ```Cleos``` also interacts with ```keosd``` (key + EOSIO = ```keosd```), a local component that securely stores EOSIO keys.

To build smart contracts you require ```EOSIO.CDT```, the Block.one developed toolchain and libraries, which generate the ```WebAssembly``` binary instructions or ```bytecode``` into ```wasm``` files. The generated ```wasm``` files are the smart contracts which can be deployed to EOSIO blockchains.

## Nodeos

Nodeos is the core EOSIO node daemon. Nodeos handles the blockchain data persistence layer, peer-to-peer networking, and contract code scheduling. For development environments, nodeos enables you to set up a single node blockchain network. Nodeos offers a wide range of features through plugins which can be enabled or disabled at start time via the command line parameters or configuration files.

You can read detailed documentation about ```nodeos``` [here](https://developers.eos.io/manuals/eos/latest/nodeos/index).

## Cleos

```cleos``` is a command line tool that interfaces with the REST APIs exposed by nodeos. You can also use ```cleos``` to deploy and test EOSIO smart contracts.

You can read detailed documentation about ```cleos``` [here](https://developers.eos.io/manuals/eos/latest/cleos/index).

## Keosd

```keosd``` is a key manager daemon for storing private keys and signing digital messages. ```keosd``` provides a secure key storage medium for keys to be encrypted in the associated wallet file. The ```keosd``` daemon also defines a secure enclave for signing transaction created by ```cleos``` or a third party library.

{% note tip %}

```keosd``` can be accessed using the wallet API, but it is important to note that the intended usage is for local light client applications. ```keosd``` is not for cross network access by web applications trying to access users' wallets.

{% endnote %}

You can read detailed documentation about ```keosd``` [here](https://developers.eos.io/manuals/eos/latest/keosd/index).

## EOSIO.CDT

```EOSIO.CDT``` is a toolchain for ```WebAssembly``` (```Wasm```) and a set of tools to facilitate contract writing for the EOSIO platform. In addition to being a general-purpose ```WebAssembly``` toolchain, EOSIO-specific optimizations are available to support building EOSIO smart contracts. This new toolchain is built around ```Clang 7```, which means that ```EOSIO.CDT``` has most of the current optimizations and analyses from ```LLVM```.

## EOSJS

A Javascript API SDK for integration with EOSIO-based blockchains using the EOSIO RPC API.
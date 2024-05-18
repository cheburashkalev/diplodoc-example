## Accounts

An account is a human-readable name that is stored on the blockchain. It can be owned through authorization by an individual or group of individuals depending on permissions configuration. An account is required to transfer or push any valid transaction to the blockchain.

Ownership of each account on an GlobalForce blockchain is solely determined by the account name. Therefore, an account can update its keys without having to redistribute them to other parties.

## Wallet

A wallet is a client application that stores keys that can be associated with the permissions of one or more accounts. The wallet stores a private key that is protected by a high entropy password. This key is intended to sign transactions on the blockchain according to the permissions for a given account. In addition to the basic functions of the wallet, for the convenience of users, this client application provides a wide range of functions such as key management, authorization management, transaction whitelists and blacklists, fungible token (FT) exchange, staking, non-fungible token (NFT) market and so on.

## Authorization

The account identifies a participant in the GlobalForce blockchain by signing the transaction with the private key of the user's account. Authorization can be done by an individual or a group, depending on the permissions assigned to the account. Accounts are also participants in smart contracts that send and receive actions from other accounts on the blockchain. Actions are always contained within transactions. A transaction can be one or more atomic actions.

## Permissions

Permissions control what accounts can do and how actions are allowed. This is achieved through a flexible permissions structure that associates each account with a list of hierarchical named permissions and each named permission with a table of permissions.

Let's say we have permission to post on a social network. However, we do not want to tie this permission to sensitive actions such as transfers or withdrawals. In this scenario, it makes sense to associate an action with a permission. This allows you to define a permission structure that can authorize a post on a social network, but cannot satisfy the default permissions for all other actions. This permission structure can delegate rights to another account at any named permission level.
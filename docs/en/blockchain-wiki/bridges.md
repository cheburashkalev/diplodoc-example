# Bridges

The general concept of GlobalForce bridges for all external networks is a smart contract in the GF network that implements the functionality of bridges for networks.

The smart contract is responsible for issuing a token entering the GF network or burning a token leaving the GF network.
Each user of the GF network has a unique address in all networks corresponding to GF, which allows you to receive tokens from these networks for a specific user.
The main bridge server listens in real time to transactions of networks corresponding with GF and when it detects a transaction to one of the addresses of users of the GF network, it starts the procedure for exchanging an external token received for an internal token that will be issued in the GF network.

If the amount of token received at the user’s address is equal to or exceeds the minimum amount of token input into the network, the procedure for exchanging the external token received for the internal token issued for this user is launched. If the amount is lower, the exchange will not be made, the token will remain on the address balance until the balance of the external address increases to the minimum exchange amount.

Next, a token transaction is made from the user’s unique address to the network’s hot wallet. To do this, the bridge server makes a request to the signature server, passing the transaction that needs to be signed. The signature server checks the balance of the user's wallet, replenishes the user's wallet with a token to carry out the transaction, for the Ethereum network it is ETH, for the BSC network it is BNB, for the Tron network it is TRX and so on, signs and carries out the transaction. After receiving funds to the external hot wallet GF, the GF network issues the corresponding amount of the received token and transfers it to the user’s wallet.

When withdrawing a token from the GF network to the corresponding network, the user makes a token transaction into the smart contract of the bridge of the corresponding network, indicating the address where the token will be sent. When funds arrive in the smart contract of the network bridge, the bridge server sends the transaction to the signature server. The signature server, in turn, verifies the transaction, signs and posts it on the appropriate network.

If there is a lack of liquidity on the network’s hot wallet, the signature server transmits a request to replenish liquidity from the network’s cold wallet, waits for replenishment, and then carries out the transaction.

The sum of any token in the GF network is equal to the sum of tokens in the hot and cold wallets of this token in the corresponding network.

Thus, more tokens cannot be issued in the GF network than entered into the network from corresponding networks.
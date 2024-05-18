# GlobalForce Ecosystem

GlobalForce is not just a blockchain, it is a financial and business ecosystem aimed at the functioning of decentralized applications. You can evaluate all the capabilities of the ecosystem yourself by installing the GlobalForce wallet, where all the capabilities of the ecosystem are built in in the most user-friendly interface. We tried to simplify as much as possible any task that a user may set for himself when working with the ecosystem and make the work simple and enjoyable. We are constantly developing, expanding and improving the ecosystem for your best blockchain experience.

## Blockchain

The high-speed GlobalForce blockchain consists of a test network and a main network. The test network serves as the main testing ground for the development, assembly and testing of smart contracts for decentralized applications. Thanks to free transactions on the test network, it is possible to organize almost any conditions for the future operation of the application before its deployment to the main network.

The GlobalForce Main Network is a high-speed, high-performance blockchain designed to run transaction-intensive decentralized applications. Releasing 2 blocks per second, with a total throughput of approximately 10,000 transactions per second and a block irreversibility time of approximately 90 seconds, GlobalForce is capable of storing financial and other mission-critical data for virtually any cutting-edge application.

## System steak

The system stake is a smart contract gf.hold. Any user of the GlobalForce blockchain has the opportunity to stake GFL network coins and receive their share of the distribution of rewards for block production. 20% of block production rewards are distributed in the gf.hold smart contract between users in proportion to their contribution to the stake. That is, you can receive a permanent stable passive income by sending your GFL tokens to the stake and withdraw tokens from the stake when you need them.

## Decentralized exchange

The decentralized exchange is a ```gf.dex``` smart contract created on the basis of liquidity pools with automatic market making. The principle of the contract is simple: when a trading pair is created, two tokens are added to the liquidity pool of this pair - a trading token and a market token.

The trading token can be anything originally issued on the GlobalForce network, or it can be a swap token moved across bridges from a third-party network, and the market token is always the base coin of the GlobalForce GFL network. The ratio of tokens added to the liquidity pool determines the initial trading price. When purchasing a trade token, the GFL market coin is sent to the pool and the trade coin is taken away. As a result, the number of GFL in the pool increases, and the number of trade coins decreases, and the price of the trade coin increases accordingly. When selling a trade token, the opposite happens: the quantity of the market token decreases, and the quantity of the trade token increases, causing the price of the trade token to fall.

In fact, on the exchange you can purchase any tradable coin for any other, but if we buy something other than GFL or sell it for any other token except GFL, then not one transaction will be made on the exchange, but two.

{% note tip %}

Any GlobalForce user can create a trading pair directly from their wallet by sending the corresponding assets to the pair's liquidity pool. Also simple: the user can withdraw his assets from the pool in proportion to the current value of the assets.

{% endnote %}

The owner or any other user can add a pool of rewards to any trading pair, which will be distributed among the liquidity holders. The reward pool is transferred voluntarily and serves as a factor in attracting capital to the trading pair. A reward pool is optional and unlimited in size, but if there is no reward or the reward is too small, it will be difficult to beat the competition for liquidity provided by users. To obtain additional liquidity from users, token owners will have to pay for this not with ephemeral exchange tokens, the value of which gradually drops to zero, but with liquid tokens.

Currently there are no trading commissions on the exchange, but in the future there will be a small trading commission - 0.3% of the transaction amount.

{% note tip %}

Swiss Tech Capital AG does not try to make a profit on trading transactions, but only to satisfy the interests of clients.

{% endnote %}

This commission will not be aimed at making a profit, but will replenish the trading pool in equal shares, which will stimulate the influx of liquidity to the pools and allow users to trade on more favorable terms, since the greater the volume of liquidity in the pool, the less fluctuations in the token during a transaction.

[More details](./exchange.md)

## External asset price data provider

Since smart contracts running on the blockchain do not have independent access to data outside the blockchain, and the network uses assets that come through bridges from other networks, we have developed a provider of external asset price data, which is the gf.price smart contract. This smart contract can be used by any decentralized application via the API to obtain external asset prices, and it is also used by the wallet to display the value of assets.

## NFT protocol

NFT is one of the most popular blockchain technologies today, but we are confident that thanks to the widest functionality, this technology will be in demand in the future. Our team has developed a unique NFT protocol that allows you to create different types of NFTs, each of which has its own purpose. Perpetual NFTs (with an unlimited lifespan) can represent a patent, certificate, diploma, become proof of ownership of an item with an unlimited service life, can serve as a key or access right, store copyright, become a work of digital art. Temporary NFTs (with a limited lifespan) can become a ticket, a certificate, a license, ownership of an item with a limited lifespan, and so on. Both permanent and temporary NFTs can be static or dynamic. Static NFTs cannot be changed by anyone; they store the original information embedded in it when it was created. Dynamic NFTs have an immutable part that is set at creation and a mutable part that can be changed by the creator. Dynamic NFTs can change owners, but the creator always has the right to change the dynamic part. Dynamic NFTs are mainly used in games, where the NFT represents some kind of game object - an item or character that can be changed or improved within the rules of the game. This object can be donated, sold to another user, and he will also be able to continue upgrading it. Moreover, this NFT can be used in another game, the smart contract of which is not the creator of this NFT. This is where the magic of GlobalForce blockchain permissions begins. A creator's named right to change the NFTs they issue can be transferred to another user, in this case another game's smart contract, if they agree, for example, to mutually exchange rights to change dynamic NFTs. In this case, two or more games at once will support each other’s NFTs and the world of games will become even more vibrant and diverse for you.

Any NFT that you own and is free from blocking can be put up for sale directly in your wallet, and you can also purchase NFTs offered for sale there.

NFTs are locked by users themselves in smart contracts to use NFTs in decentralized applications, for example, to participate in games, distribute income, gain access to information, or any other operations in accordance with the objectives of the decentralized application using NFTs.

## Crosschain bridges

We call bridges the infrastructure that makes it possible to ensure the use of tokens from one blockchain in the network of another blockchain. Currently, there are many bridge architectures that allow cross-network operations, and there are also fully decentralized architectures. Unfortunately, due to the diversity of blockchain architectures themselves, many of which do not have smart contract capabilities, decentralized architectures cannot be used in all blockchains. Moreover, decentralized bridge architectures are economically significantly inferior to centralized ones, since confirmation of a transaction in a decentralized environment is essentially a transaction and a commission is charged from it as for a full-fledged transaction; multiple confirmations to achieve consensus can amount to hundreds of dollars. Paying hundreds of dollars to transfer funds from one network to another is extremely expensive.
In our bridges, we used a semi-decentralized architecture, that is, the part of the bridge responsible for distributing tokens entering and leaving our network is decentralized. This part is a smart contract that performs the transfer and withdrawal of tokens. Each user of the GlobalForce network has an associated wallet in each network corresponding to the GlobalForce network. When funds are credited to the wallet associated with the user, funds from this wallet are collected on the GlobalForce hot wallet on this network. At the same time, the corresponding token is issued in the GlobalForce blockchain and the amount of the token is credited to the wallet of the user who received the payment. When withdrawing a token from the GlobalForce network to another network, the user makes a transaction to the address of the bridge smart contract, indicating the target network and recipient address in the MEMO field. Upon receiving this transaction, the smart contract burns the sent amount and initiates the payment process from the hot wallet of this network to the address specified by the user.
Most importantly, all coins of other networks created on the GlobalForce network have corresponding liquidity in the hot wallet on the corresponding network. That is, the number of coins in the GlobalForce network is always equal to the number of the corresponding coin in the wallet in the corresponding network.

## Service for developers

For ease of development and deployment of smart contracts, we have developed an online service that allows you to assemble and deploy smart contracts without the need to install a network node. This service also allows you to create key pairs, but we recommend using them only on a test network. We recommend creating key pairs for the main network in a wallet or using a network node.
For quick development, we have prepared examples of smart contracts, examples of decentralized applications in JavaScript, C#, C++.




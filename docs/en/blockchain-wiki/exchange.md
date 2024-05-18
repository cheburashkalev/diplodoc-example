# Smart contract gf.dex

The decentralized exchange is a ```gf.dex``` smart contract created on the basis of liquidity pools with automatic market making. The principle of the contract is simple: when a trading pair is created, two tokens are added to the liquidity pool of this pair - a trading token and a market token.

The trading token can be anything originally issued on the GlobalForce network, or it can be a swap token moved across bridges from a third-party network, and the market token is always the base coin of the GlobalForce GFL network. The ratio of tokens added to the liquidity pool determines the initial trading price. When purchasing a trade token, the GFL market coin is sent to the pool and the trade coin is taken away. As a result, the number of GFL in the pool increases, and the number of trade coins decreases, and the price of the trade coin increases accordingly. When selling a trade token, the opposite happens: the quantity of the market token decreases, and the quantity of the trade token increases, causing the price of the trade token to fall.

In fact, on the exchange you can purchase any tradable coin for any other, but if we buy something other than GFL or sell it for any other token except GFL, then not one transaction will be made on the exchange, but two.

{% note info %}

Any GlobalForce user can create a trading pair directly from their wallet by sending the corresponding assets to the pair's liquidity pool. Also simple: the user can withdraw his assets from the pool in proportion to the current value of the assets.

{% endnote %}

The owner or any other user can add a pool of rewards to any trading pair, which will be distributed among the liquidity holders. The reward pool is transferred voluntarily and serves as a factor in attracting capital to the trading pair. A reward pool is optional and unlimited in size, but if there is no reward or the reward is too small, it will be difficult to beat the competition for liquidity provided by users. To obtain additional liquidity from users, token owners will have to pay for this not with ephemeral exchange tokens, the value of which gradually drops to zero, but with liquid tokens.

Currently there are no trading commissions on the exchange, but in the future there will be a small trading commission - 0.3% of the transaction amount.

{% note info %}

Swiss Tech Capital AG does not try to make a profit on trading transactions, but only to satisfy the interests of clients.

{% endnote %}

This commission will not be aimed at making a profit, but will replenish the trading pool in equal shares, which will stimulate the influx of liquidity to the pools and allow users to trade on more favorable terms, since the greater the volume of liquidity in the pool, the less fluctuations in the token during a transaction.

## Calculation

Transaction calculations are made based on the equation ```a * b = k```
Where:
```a``` - trading token;
```b``` - market token
```k``` - liquidity ratio

If a purchase transaction is made in the pool for amount ```x```, then amount ```y``` will be sent to the client, while the coefficient ```k``` will remain unchanged. Also a sales transaction, if the sale is carried out for the amount ```x```, then taking into account the constant coefficient ```k```, we can calculate the amount ```y```.
That is, in the case of a purchase, the equation is:
```(a - y) * (b +x) = k```
And in case of sale the equation will be:
```(a + x) * (b - y) = k```
In both equations we know all the variables except ```y```, which are easy to calculate.

## Fee

Currently, the exchange operates without commissions. The liquidity of the pools is provided free of charge by partners of Swiss Tech Capital AG. But money must work and make a profit, so it was decided to introduce commissions, but not in favor of the company, but in favor of liquidity owners. Each trade on the exchange will be subject to a small commission of 0.3%, which remains in the pool, increasing it and allowing the pool owners to earn money by providing liquidity.
Since each pool consists of two tokens - a trading token and a market token, we need to maintain a balance of tokens in the pool.

To do this, the commission percentage is divided into two equal parts - 0.15% and 0.15%. The first part is charged from the funds received into the contract, regardless of the type of transaction, the second part is collected from the funds sent. After the transaction is completed, both parts of the commission go to the liquidity pool while maintaining parity in the value of the token

## Additional rewards and competition for liquidity

The exchange commission will certainly attract capital to the liquidity pools of trading pairs of well-known and popular tokens on the market. Investing in new tokens and startup tokens will remain a risky endeavor in any case. To attract capital, startups can use a specialized reward pool. To do this, you just need to send a transaction to the appropriate pool and these funds will be distributed among liquidity owners within six months. The more funds enter the pool, the higher the income of liquidity owners. This creates healthy competition between different pools.
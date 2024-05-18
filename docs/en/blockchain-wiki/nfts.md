# Non-fungible tokens

Non-fungible tokens are currently one of the most popular blockchain technologies. This token can serve as a public right not only for digital property, but also for other types of property, such as real estate, cars, servers, ASIC miners and much more. NFTs are used as a means of collecting electronic art, as a license, ticket, and more. In general, NFT is a universal means for owning and transferring any rights.

Until now, the main problem has been the lack of flexibility of this tool. The DAPPs market is huge and custom NFT solutions are often required. In some cases, a perpetual, immutable token is required that will represent the right to the collectible, but sometimes it is necessary to establish a period of ownership if the right is, for example, a license. In another case, where the ownership is a game character, changes must be made to a given NFT as the character develops.

We have created an NFT protocol that allows us to overcome these problems. To do this, we have introduced two main categories of NFTs - static (unchangeable) and dynamic (changeable). With static ones everything is simple; NFTs can never be changed. Dynamic NFTs have an unchangeable part in which its main parameters are stored and a changeable part where additional parameters can be stored.

{% note alert %}

Attention! The mutable part of a dynamic NFT can initially only be changed by its creator's account (not the owner's account).

{% endnote %}

There are two additional categories in our protocol - temporary NFTs and perpetual NFTs. Perpetual ones have no life limit, but temporary ones will be burned at the end of their lifespan. The lifetime is set when the NFT is created.
# Smart contract gf.price

One of the difficulties of working with smart contracts is the so-called oracle problem in the blockchain. Smart contracts do not have the ability to interact with external resources, such as external data providers or API services, and, accordingly, smart contracts themselves cannot be a means of validating the results of real events occurring outside the blockchain.

But such a need is present for many smart contracts. One of the main data used by smart contracts is exchange price quotes for assets. This data is used by many different DAPPs, including exchanges, bridges, games...

The difficulty is that any third-party influence on external data can lead to serious financial losses on the part of DAPPs. An attacker, by changing the supplier's input data, has the opportunity to buy an asset at a reduced price or sell an asset at an inflated price.

Together with the ```gf.price``` smart contract, we have developed a protocol - a set of logical-level agreements that determine the order of data exchange between data sources and the smart contract.

To obtain information from sources, their public API is used. Information about quotations comes from several trusted sources, and if one of the sources reports a value that differs from most other sources by 5% or more, such a source is considered compromised and is ignored. The price of an asset is determined as the average price from uncompromised sources.
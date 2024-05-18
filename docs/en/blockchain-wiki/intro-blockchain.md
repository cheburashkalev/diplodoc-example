# Introduction to GlobalForce

## About blockchain

Blockchain technology was introduced in 2008 with the example of the Bitcoin blockchain. Initially, there was no mass adoption across various sectors of the economy, but entrepreneurs and developers focused on scaling the technology and developing alternative solutions to suit their needs.

High fees and limitations imposed by computing power requirements have prevented the widespread adoption of blockchain technology and its adaptation to community needs.

Global Force is a fork of the EOS platform that uses its own unique RBPS (Randomized Block Producer Selection) consensus algorithm. Global Force has a GFL (Global Force Liquidity) token issued on the Global Force blockchain.

After many years of platforms operating on the dPOS consensus algorithm, it becomes obvious that for stable business operation there must be a different financial model of the network, not subject to the influence of large capitals. The dPoS network consensus, in fact, any algorithm of the POS family, has shown its vulnerability in practice. In fact, a group with a capital of more than 50% of the network’s coins takes over the network and becomes the Center (leader) of this network, that is, de facto, the network ceases to be decentralized.

The Global Force project proposes to change both the financial and economic model of the blockchain and the network consensus algorithm to an algorithm that can completely eliminate this vulnerability.

## Technical features

### Compiling ```WebAssembly``` C++

GlobalForce uses C++ as its smart contract programming language. A C++ developer does not need to learn a new programming language to understand how smart contracts work. GlobalForce supports smart contract development using C++ classes and structures. With available C++ programming capabilities, a developer can accelerate GlobalForce smart contract development using canonical GlobalForce C++ code constructs and smart contract APIs.

On top of the main GlobalForce layer, the ```WebAssembly``` (```wasm```) EOS VM runs smart contract code and from scratch. ```wasm``` is designed to meet the demanding requirements of blockchain applications, which require much more from the ```WebAssembly``` engine. The choice to use ```wasm``` allows GlobalForce to reuse optimized and field-tested compilers and toolkits that are supported and improved by the wider community. In addition, the adoption of the ```wasm``` standard also makes it easier for compiler developers to port other programming languages to the GlobalForce platform.

### Higher throughput, faster confirmations and lower latency

GlobalForce is designed with high transaction throughput in mind, and each new version provides significant improvements.

The Random Block Producer Selection (RBPS) consensus mechanism provides high transaction throughput because RBPS does not need to wait for all nodes to complete a transaction to achieve finality. This behavior results in faster confirmation and lower latency.

### Efficient energy consumption

Thanks to the RBPS consensus mechanism, GlobalForce consumes much less energy to validate transactions and secure the blockchain compared to other consensus algorithms.
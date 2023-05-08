# **Chainlink**
- `chainlink` is a cryptocurreny and technology platform that enables non-blockchain enterprise to securely conenct with blockchain platforms
- chainlink is middleware that connects blockchain-based smart contracts with external data, eg: stock prices
- chainlink is known as a decentralized oracle network or blockchain abstraction layer, it uses blockchain technology to securely enable computations on and off chain, supporting what it calles hybird smart contracts
- enterprises using chainlink cna access any major blockchain network, including Ethereum and Solana
- Chainlink tokens - called `LINK` - serve as currency to pay Chainlink network operators for retrieving and preparing off-chain data and performing computations

# **Features**
- Chainlink blockchain can suuport the secure sharing of inputs, outputs, and computations. features included:
## **1. supporting decentralized data feeds**
- data from many sources can be securely colelcted and processed for hybrid smart contracts
## **2. providing verifiable sources of randomness**
- applications such as games that require cryptographically secured randomness can use Chainlink
## **3. enabling automation**
- chainlink smart contracts can automate critical functions and event-driven tasks for enterprise
## **4. supporting cross-blockchain interoperability**
- chainlink can connect blockchain platforms to support the exchange of messages, tokens, and specific actions

# **Oracles**
- `oracles` are entities that connect blockchain to external systems, thereby enabling smart contracts to be execute based upon inputs and outputs from the real world
- `oracle` provide a way for the decentralized web3 ecosystem to access existing data source, legacy systems, and advanced computations
- `decentralized oracle networks (DONs)` enable the creation of hybrid smart contracts, where on-chain node and off-chain node infrastructure are combined to support advanced decentralized applications that react to real-world events and interoperate with traditional systems
![blockchain oracle](https://assets-global.website-files.com/61163fe987f45b44cc88bc6a/61277245f4962c179dcab303_Hybrid%20Smart%20Contract.png)
- smart contract has a big limitation - they cannot inherently interact with data and systems existing outside their native blockchain environment
- securely interoperating with off-chain systems from a blockchain requires an additional piece of infrastructure known as an `oracle` to bridge the 2 environments
- oracle expand the type of digital agreements that blockchains can support by offering a universal gateway to off-chain resources while still upholding the valuable security properties of blockchains
- major industries benefit from combining oracles and smart contracts including asset prices from finance, weather information for insurance, randonmess for gaming, IoT sensors for supply chain, ID verification for goverment
![oracle bridge](https://assets-global.website-files.com/5f6b7190899f41fb70882d08/6148588af8ce998ca21d8db8_Blockchain%20Oracle%20Problem.jpg)

# **Types of blockchain oracles**
- Given the extensive range of off-chain resources, blockchain oracles come in many shapes and sizes. Not only do hybrid smart contracts need various types of external data and computation, but they require various mechanisms for delivery and different levels of security
- Generally, each type of oracle involves some combination of fetching, validating, computing upon, and delivering data to a destination
## **1. Input Oracles**
- most widely recognized type of oracle today
- fetches data from the real-world (off-chain) and delivers it onto a blockchain network for smart contract consumption
- are used to power Chainlink Price Feeds, providing DeFi smart contracts with on-chain access to financial market data
## **2. Output Oracles**
- opposite of input oracles
- allow smart contracts to send commands to off-chain systems that trigger them to execute certain actions
- include informing a banking network to make a payment, telling a storage provider to store the supplied data, or pinging an IoT system to unlock a car door once the on-chain rental payment is made
## **3. Cross-Chain Oracles**
- can read and write information between different blockchains
- enable interoperability for moving both data and assets between blockchains, such as using data on one blockchain to trigger an action on another or bridging assets cross-chain so they can be used outside the native blockchain they were issued on
## **4. Compute-Enables Oracles**
- use secure off-chain computation to provide decentralized services that are impractical to do on-chain due to technical, legal, or financial constraints
- include using Chainlink Automation to trigger the running of smart contracts when predefined events take place, computing zero-knowledge proofs to generate data privacy, or running a verifiable randomness function to provide a tamper-proof and provably fair source of randomness to smart contracts

# **Use Cases**
- Smart contract developers use oracles to build more advanced decentralized applications across a wider range of blockchain use cases.
- While there are a potentially infinite number of possibilities, below are the use cases with the most current adoption.
## **1. Decentralized Finance (DeFi)**
- A large portion of the decentralized finance (DeFi) ecosystem requires oracles to access financial data about assets and markets. 
- For example, decentralized money markets use price oracles to determine users’ borrowing capacity and check if users’ positions are undercollateralized and subject to liquidation. 
- Similarly, synthetic asset platforms use price oracles to peg the value of tokens to real-world assets and automated market makers (AMMs) use price oracles to help concentrate liquidity at the current market price to improve capital efficiency. 
## **2. Dynamic NFTs amd Gaming**
- Oracles enable non-financial use cases for smart contracts too such as dynamic NFTs—Non-Fungible Tokens that can change in appearance, value, or distribution based on external events like the time of day or the weather
- Additionally, compute oracles are used to generate verifiable randomness that projects then use to assign randomized traits to NFTs or to select random lucky winners in high-demand NFT drops.
- On-chain gaming applications also use verifiable randomness to create more engaging and unpredictable gameplay experiences like the appearance of random loot boxes or randomized matchmaking during a tournament. 
# **3. Insurance**
- Insurance smart contracts use input oracles to verify the occurrence of insurable events during claims processing, opening up access to physical sensors, web APIs, satellite imagery, and legal data
- Output oracles can also provide insurance smart contracts with a way to make payouts on claims using other blockchains or traditional payment networks.
# **4. Enterprise**
- Cross-chain oracles offer enterprises a secure blockchain middleware that allows them to connect their backend systems to any blockchain network. 
- In doing so, enterprise systems can read/write to any blockchain and perform complex logic on how to deploy assets and data across chains and with counterparties using the same oracle network. 
- The result is institutions being able to quickly join blockchains in high demand by their counterparties and swiftly create support for smart contract services wanted by their users without having to spend time and development resources integrating with each individual blockchain.
# **5. Sustainability**
- Hybrid smart contracts are advancing environmental sustainability by creating better incentives to partake in green practices through advanced verification techniques around the true impact of green initiatives. 
- Oracles are a critical tool to supplying smart contracts with environmental data from sensor readings, satellite imagery, and advanced ML computation, which then allow smart contracts to dispense rewards to people practicing reforestation or engaging in conscious consumption. 
- Oracles are also supporting many new forms of carbon credits to offset the impacts of climate change.
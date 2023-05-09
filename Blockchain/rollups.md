# **Zero Knowledge Rollups**
- `zero-knowledge rollups` is a layer-2 scalability solution that allows blockchain to validate transaction faster while also ensuring that gas fees remain minimal
- is a later 2 solution that performs computations and storage off-chain while funds are held in a smart contract
- manage to perform better than traditional layer-1 blockchains because they combine on and off-chain processes
- Ethereum miannet explicitlu utilizes `on-chain` activities to process transactions and validate blocks, layer 2 zk-rollup solutions introduce off-chain functionalities as well
- one of the main components that allow them to successfully validate transactions faster than layer-1 blockchains are `Merkle Trees`, an important mathematical structure that allows blockchains to ensure that no one can fake data on the on-chain records of a zk-rollup
- Usually, a zk-rollup consists of two Merkle Trees which are both stored on a smart contract, or in other words, on-chain. One tree is dedicated to storing accounts, while the other stores all balances. Any other type of data generated and used by the zk-rollup is stored off-chain

# **ZK-Rollups Woking Principle**
- is a layer-2 scaling solution increasing Ethereum's throughput by processing transactions outside of the Ethereum mainnet. It alleviates congestion on the base layer and bolsters scalability
- 3 primary components of a zero-knowledge rollup include a `smart contract on Ethereum, a prover, and a set of verifiers`
- Interactions between chains are managed by the smart contract. A third-party prover generates cryptographic proofs of transaction validity on the layer-2 chain, while verifiers are a group of nodes responsible for confirming these proofs and submitting them to the smart contract.
1. Users sign transactions and submit them to the prover, who verifies and queues them. 
2. Periodically, the prover batches thousands of transactions from the queue into a block and generates a zero-knowledge proof of their validity. 
3. This proof is a concise piece of data that can be verified in just a few milliseconds without revealing any transaction information. 
4. The prover then submits the proof and a small amount of data — such as the state root and the transaction root — to Ethereum as a single transaction. 
5. The smart contract verifies the proof and updates its state accordingly.
6. Withdrawing funds necessitates an exit request, which is submitted to an Ethereum block. 
7. The smart contract then unlocks and transfers the funds. No waiting period is required for withdrawals, as they are verified by proofs.
- A key feature of zk-rollups is their use of zero-knowledge proofs to verify transactions on-chain without requiring any interaction or trust. This enables high scalability, low latency, and privacy features.
# **Mempool**
- `mempool` is like a waiting room for unmined transactions on the blockchain, it is used to describe the storage area of a node where validated transactions hang out, waiting to be mined and added to the blockchain
- there is NO ONE mempool per blockchain, in fast, every node comprising a network has its own mempool, for example, every node on the Bitcoin blockchain has its own pool of waiting transactions, those individual nodes with their individual pools, together form a collective global pool

# **How Does Mempool work?**
- when we broadcast a transaction, it is send to a node or nodes that is connected to
- those nodes will validate (or reject) the transaction according to a set of criterion, for example, it will ensure the signature is correct, that the coins belong to the seller, and the outputs don't exceed the inputs
- if everything checks out, the nodes will pass this transaction on to all the other nodes they are connected to, and so on and so forth, with each node adding it to its memory pool, waiting for a miner to come along and do its thing
- Normal transaction lifecycle:
1. Users initiate a transaction in their wallet, for example sending funds to another wallet, and sign the transaction with their private key. 
2. The signed transaction is broadcast to a node on the blockchain (Ethereum, Bitcoin, etc.) 
3. The node will check and validate the transaction, adding it to its mempool and broadcasting it to its peers. 
4. Each node that receives the transaction will do the same, replicating the transaction across the network. 
5. Some of these nodes will be mining nodes, which will add the transactions to a block and then compete to solve the hash of the block to be the one to add it to the blockchain. 
6. Once a miner is successful and the block of transactions is added to the chain, the new block is broadcast back across the network.  
7. All the nodes receive the new block and can see the included transactions. If they have any of those mined transactions stored in their mempool, they are removed

# **How does the Mempool affects the transaction fee?**
- `mempool` isnt a infinite space - it has limits, the size of available memory will depend on the individual node
- although the default mempool size is `300MB`, each ndoe will have its own rules for which transaction it allows into its own mempool
- when the ndoe is nearing its RAM limit, it will set a minimum fee rate and communicate this to its peers so that they wont forward transactions below this rate for the time being
- a node with a smaller or larger mempool may drop transactions earlier or later which results in differing mempool size
- this is what causes congestion and at this point, users can either wait for the congestion to clear (when a block is mined and other transactions are removed from the queue), or they can pay higher fees to try push their transactions through faster

# **How to speed up bitcoin transactions?**
- if we find our Bitcoin transaction is "pending" much longer than we'd like, we can make it more attractive to miners to speed it along
- the way to speed up bitcoin transaction depend on the architecture of the wallet we are using
- we may be given the choice of an opt-in `Replace-by-Fee (RBF)`, which let us resend our transaction replacing the lower fee with a higher fee
- if our wallet doesn't support this feature, we may have to use the `child pays for parent (CPFP)` technique, where we need to broadcast a new transaction (child transaction) using the change (unspend output) from the original parent transaction, but with a much higher fee
- it's more attractive, but in order for a miner to access the higher fees, they must validate the original transaction with the lower fee too
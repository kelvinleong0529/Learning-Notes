# **Soft Fork**
- `soft fork` is a change to software protocol where only previously valid transaction blocks are made invalid
- because old-nodes will recognize the new blocks as valid, it is backwards-compatible
- requires only a majority of miners upgrading to enforce the new rules, as opposed to `hard fork` which requires all nodes to upgrade and agree on the new version

# **How Soft Fork Works**
- new transaction types can often be added as soft forks, requiring only that the participants (eg: sender and receiver) and miners to understand the new transaction type
- this is done by having the new transaction type appear to older clients as a `pay-to-anybody` transaction (of a special form) and getting the miners to agree to reject blocks including these transactions unless the transaction validates under the new rules
- can also occer at times due to a temporary divergence in the blockchain when miners using non-upgraded nodes violate a new consensus rule their nodes don't know about

# **Hard Fork**
- `hard fork` is a radical change to a network's protocol that makes previously invalid blocks and transactions valid, or vice-versa
- refers to a radical change to the protocol of a blockchain metwork that effectively results in 2 branches, one that follows the previous protocol and one that follows the new version
- in a `hard fork`, token holders in original blockchain will be granted tokens in the new fork as well, but miners must choose which blockchain to continue verifying
- `hard fork` requries all nodes or users to upgrade to the latest version of the protocol software
- maybe initiated by developers or members of a crypto community who grow dissatisfied with functionalities offered by existing blockchain implementations
- may also emerge as a way to crowdsource funding for new technology projects or cryptocurrency offerings

# **How Hard Fork Works**
- adding new rule to the code essentially creates a fork in the blockchain: one path follows the new, upgraded blockchain, and the other path continues along the old path
- generally, those on the old chain will realize that their version of the blockchain is outdated or irrelevant and quickly upgrade to the latest version
- all miners need to agree about the new rules and about what comprises a valid block in the chain, a `fork` is required to indicate there's been a change in or a diversion to the protocol, the developers can then update all of the software to reflect the new rules
- it is through tis forking process that various digital currencies with names similar to the native asset have come to be, eg: `bitcoin cash`, `bitcoin gold`

# **Why Hard Fork?**
- reasons for hard fork:
1. correcting important security risks found in older version of the software
2. add new functionality
3. reverse transaction, such as when Ethereum blockchain created a hard fork to reverse the hack on DAO
- proposal for a `hard fork` did not exactly unwind the network's transaction history, rather it relocated the funds tied to the DAO to a newly created smart contract with the purpose of letting the original owners to withdraw their funds

## **Hard Forks VS Soft Forks**
- both are essentially the same in the sense that when a cryptocurrency platform's existing code is changed, an old version remains on the network while the new version is created
- With a soft fork, only one blockchain will remain valid as users adopt the update.
- Whereas with a hard fork, both the old and new blockchains exist side by side, which means that the software must be updated to work by the new rules. 
- Both forks create a split, but a hard fork creates two blockchains and a soft fork is meant to result in one
- Considering the differences in security between hard and soft forks, almost all users and developers call for a hard fork, even when a soft fork seems like it could do the job.
- Overhauling the blocks in a blockchain requires a tremendous amount of computing power, but the privacy gained from a hard fork makes more sense than using a soft fork
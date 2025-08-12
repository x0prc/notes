---
dg-publish: true
permalink:
---






## ==Aspects==

- Who maintains the ledger?
- Who has authority over which transactions are valid?
- Who creates new Bitcoins?
    - Peer-to-Peer network
        - Mining, open to anyone
    - Updates to software, core devs are trusted and have great power

## ==Distributed Consensus==

- Protocol terminates and all correct nodes decide on the same value, which must have been proposed by some correct node.
- ==To explain the working; at any given time:==
    - All nodes have a sequence of blocks of transactions they’ve reached consensus on.
    - Each node has a set of outstanding transactions it’s heard about.

## ==Why is Consensus hard?==

- Nodes may crash or may be malicious
- ==Network could be imperfect:==
    - Not all pairs of nodes connected
    - Faults in network, latency
    - No notion of global time

## ==Implicit Consensus==

1. Random node is picked in each round.
2. This node proposes the next block in the chain
3. Other nodes implicitly accept/reject this block
    1. by either extending it
    2. or ignoring it and extending a chain from earlier block

> _Every block contains hash of the block it extends._

  

## ==Hash Puzzles==

- To create a block, find nonce s.t.
    
    ```Plain
    H(nonce || prev_hash || tx || … || tx) is very small
    ```
    
    ### Proof of Work properties
    
    1. Difficult to compute about 10**20 hashes/block (those who bother — miners)
    2. Parameterizable Cost: Nodes calculate the target every two weeks
        - _average time between blocks = 10 minutes_
            
            ![Screenshot_2023-07-10_at_9.49.40_PM.png](/img/user/img/Screenshot_2023-07-10_at_9.49.40_PM.png)
            
    
      
    
    1. Trivial to verify: Nonce must be published as part of block to verify the output it less than target.
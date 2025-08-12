---
dg-publish: true
permalink:
---






## ==P2P==

- Ad-hoc protocol (runs on TCP port 8333)
- Ad-hoc network with random topology (no geographic topology)
- All nodes are equal
- New nodes can join anytime
- Forgets non-responding nodes after 3 hours

## ==Transaction Propogation (Flooding)==

- Randomly arranged nodes transfer the transaction metadata within their group
- Every node verifies if :
    - Transaction is valid with current block chain
    - Script matches a whitelist
    - Haven’t seen before (Avoid infinite loops)
    - Doesn’t conflict with others it has relayed (Avoid double spends)

  

> _**Nodes may differ on transaction pool.**_

### ==If Block Propogration is nearly identical:==

- Relay a new block when you hear it if:
    - Block meets the hash target
    - Block has all valid transactions
    - Block builds on current longest chain

  

## ==Tracking the UTXO Set==

- **Unspent Transaction Output**
    - Everything else can be stored on disk
- Currently ~ 12 M UTXOs
- Can easily fit into RAM
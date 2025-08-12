---
dg-publish: true
permalink:
---






- ==Goal : Pool participants all attempt to mine a block with the same coinbase recipient==
    - Send money to key owned by pool manager
- ==Distribute revenues to members based on how much work they have performed==
    - Minus a cut for pool manager

## ==Pool Variations==

- **==Pay per share==** : flat reward per share
    - Minus a significant fee
    - Can’t trust miners
- **==Proportional==** : Since last block
    - Lower risk for pool manager
    - More work to verify
- **==“Luke-Jr” Approach==** : No management fee
    - Miners only get paid out in whole BTC
    - Pool owner keeps spread

## ==Pool Protocols==

- API for fetching blocks, submitting shares
    - Stratum
    - Getwork
    - Getblocktemplate
- Proposed for standardization with a BIP
- Increasingly important; some hardware support
---
dg-publish: true
permalink:
---






## ==Hard-coded limits in Bitcoin==

1. 10 min. average creation time per block
2. 1 M bytes in a block
3. 20,000 signature operations per block
4. 100 M satoshis per bitcoin [smallest discrete unit of btc]
5. 21M total bitcoins maximum
6. 50,25,12.5… bitcoin mining reward

## ==Throughput limits in Bitcoin==

1. 1 M bytes/block (10 min)
2. >250 bytes/transaction
3. 7 transactions/sec

## ==Cryptographic limits in Bitcoin==

1. Only 1 signature algorithm (ECDSA/P256)
2. Hard-coded hash functions

## ==Hard-forking a Blockchain==

- Block chain will split every node on the network would be on one side of it, based on which version of the protocol it’s running and they’ll never join together again.

## ==Soft forks==

- Observation: We can add new features which only limit the set of valid transactions
- Need majority of nodes to enforce new rules
- Old nodes will approve
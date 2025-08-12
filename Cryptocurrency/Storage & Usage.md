---
dg-publish: true
permalink:
---






## ==Simplest Approach==

- Store key in a file on your computer or phone
- Very convenient
- As available as your device
- As secure as your device

## ==Encoding Addresses==

- As a text string : base58 notation
- Use a QR Code

## ==Hot & Cold Storage==

- Hot Secret Keys & Cold Addresses : Online, Convenient but risky
- Cold Secret Keys & Hot Addresses : Offline, Archival but safer

## ==Hierarchical Key Generation==

generateKeysHier :

1. ==Address Gen Info ➜ genAddr ➜ i(th) address==
2. ==Private Key Gen Info ➜ genKey ➜ i(th) key==

## ==Store Cold Information==

1. Info stored in device, device locked in a safe
2. “Brain Wallet”
    1. Encrypt info under passphrase that user remembers
3. Paper Wallet
    1. Print info on paper
    2. Lock up the paper
4. In “tamperproof” device
    1. Device will sign things for you, but won’t divulge keys
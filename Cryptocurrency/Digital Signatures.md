---
dg-publish: true
permalink:
---






- Only you can sign, but anyone can verify.
- Operations of the API for Digi Sign:

```Plain
1. (sk,pk) := generateKeys(keysize)

sk: Secret Signing Key 
pk: Public Verification Key 

2. sig := sign(sk, message)

3. isValid := verify(pk, message, sig)
```

## ==Requirements for Signatures==

  

“valid signatures verify”

```Plain
verify(pk, message, sign(sk, message)) == true
```

“can’t forge signatures”

```Plain
adversary who: 
			knows pk
			gets to see signatures on messages of his choice
can't produce a verifiable signature on another message
```

  

> [!important] Bitcoin uses Elliptic Curve Digital Signature Algorithm (ECDSA) — Good randomness is essential

  

## ==Public Keys As Identities (Decentralization)==

  

- Each pair of Public and Secret Key (pk, sk) is considered as an _Identity/Address._
- Anybody can make as many identities as they want, no central point of coordination.

  

## ==Privacy==

  

- Addresses are not connected to the real word identity
- But observer can link together an address’s activity over time, making inferences.
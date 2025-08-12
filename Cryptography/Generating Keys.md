---
dg-publish: true
permalink:
---






- Cryptographic keys may be generated in one of three ways:

1. _==**Randomly**==_
    1. Using a pseudorandom number generator (PRNG) and, when needed, a key-generation algorithm.
2. ==_**From a password**_==
    1. Using a key derivation function (KDF), which transforms the user-supplied password into a key.
3. ==_**Through a key agreement protocol**_==
    1. A series of message exchanges between two or more parties that ends with the establishment of a shared key.

## ==Symmetric Keys==

- Secret keys shared by two parties, and they are the simplest to generate.
- They are usually the same length as the security level they provide: ==**a 128-bit key provides 128-bit security**==, and any of the 2^128 possible keys is a valid one that can do the job as well as any other key.
- To generate a symmetric key of n bits using a cryptographic PRNG, you simply ask it for n pseudorandom bits and use those bits as the key.

```Shell
openssl rand -hex 16

Result : ec7748687c10b572ca670ace7f76afcd
```

## ==Asymmetric Keys==

- Asymmetric keys **==aren’t just raw bit sequences==**; instead, they represent a specific type of object, such as **==a large number with specific properties==** (in RSA, a product of two primes).
- To generate an asymmetric key, ==**you send pseudorandom bits as a seed to a key-generation algorithm**==. This key-generation algorithm takes as input a seed value that’s at least as long as the intended security level and then **==constructs from it a private key and its respective public key==**, ensuring that both satisfy all the necessary criteria.

```Shell
openssl genrsa 4096

Result (Longer) : 

-----BEGIN PRIVATE KEY-----
MIIJQwIBADANBgkqhkiG9w0BAQEFAASCCS0wggkpAgEAAoICAQDOMcd5tPzVJPWh
fdfs264GsXYWxbzmkzL4T2dYnBM2SmBTiOPt/QbbAt8QadwTr7/VOGbn1B2a3DsT
-----END PRIVATE KEY-----
```

- To test key wrapping argument -aes128 can be added to encrypt the key with the cipher.
    - The passphrase requested will be used to encrypt the newly created key.

```Shell
openssl genrsa -aes128 4096

Result (Longer) :
-----BEGIN PRIVATE KEY-----
MIIJQwIBADANBgkqhkiG9w0BAQEFAASCCS0wggkpAgEAAoICAQDOMcd5tPzVJPWh
fdfs264GsXYWxbzmkzL4T2dYnBM2SmBTiOPt/QbbAt8QadwTr7/VOGbn1B2a3DsT
+1pHia4Hk3F+olu2gV9ngFexCeH2yU+5PBGJXCYScBs3Pindoee3b7Xv70pwxzdk
DhRvRst1YfGv/Kad
-----END PRIVATE KEY-----
```
---
dg-publish: true
permalink:
---






## ==Using MACs==

- Combined in one of three ways to both encrypt and authenticate a plaintext:
    - encrypt-and-MAC,
    - MAC-then-encrypt,
    - and encrypt-then-MAC.

![Screenshot_2023-08-04_at_6.31.33_PM.png](/img/user/img/Screenshot_2023-08-04_at_6.31.33_PM.png)

### ==Encrypt-and-MAC==

- Given a plaintext (P), the sender computes a ciphertext ==**C = E(K1, P),**== where E is an encryption algorithm and C is the resulting ciphertext.
- The authentication tag (T) is calculated from the plaintext as ==**T = MAC(K2, P).**== You can compute C and T first or in parallel.
- It is the least secure MAC and cipher composition because even a ==**secure MAC could leak information on P**==, which would make P easier to recover.
- In practice, encrypt-and-MAC has proven **==good enough for use with SSH==**, thanks to the use of strong MAC algorithms like HMAC-SHA-256 that don’t leak information on P.

### ==MAC-then-Encrypt==

- Protects a message, P, by first computing the authentication tag ==**T = MAC(K2, P).**==
    - Next, it creates the ciphertext by encrypting the plaintext and tag together, according to ==**C = E(K1, P || T).**==
    - Once these steps have been completed, **==the sender transmits only C==**, which contains both the encrypted plaintext and tag. Upon receipt, **==the recipient decrypts C by computing P || T = D(K1, C) to obtain the plaintext and tag T.==**
    - Next, the recipient verifies the **==received tag T==** by computing a tag directly from the plaintext according to **==MAC(K2, P)==** in order to confirm that the computed tag is equal to the tag T.

### ==Encrypt-then-MAC==

- Sends two values to the recipient: the ciphertext produced by **==C = E(K1, P)==** and a tag based on the ciphertext, ==**T = MAC(K2, C).**==
    - The receiver computes the tag using **==MAC(K2, C)==** and verifies that it equals the T received.
    - If the values are equal, the plaintext is computed as **==P = D(K1, C)==**; if they are not equal, the plaintext is discarded.

## ==Authenticated Ciphers==

- They are like normal ciphers except that they return an ==**authentication tag together with the ciphertext.**==
- The authenticated cipher encryption is represented as **==AE(K, P) = (C, T)==**
- Its authentication should be as strong as a MAC’s, meaning that **==it should be impossible to forge a ciphertext and tag pair (C, T)==** that the decryption function AD will accept and decrypt.

### ==Encryption with Associated Data==

- An AEAD algorithm allows you to attach cleartext data to a ciphertext in such a way that ==**if the cleartext data is corrupted, the authentication tag will not validate and the ciphertext will not be decrypted.**==
- ==**AEAD(K, P, A) = (C, A, T)**==
    - Decryption requires the key, ciphertext, associated data, and tag in order to compute the plaintext and associated data, ==**and it will fail if either C or A has been corrupted.**==

### ==Good Authenticated Cipher Requirements==

- Security Criteria
- Performance Criteria
- Functional Criteria

## ==AES-GCM==

- Galois Counter Mode (GCM) of operation is ==**essentially a tweak of the CTR mode that incorporates a small and efficient component to compute an authentication tag.**==
- One advantage of GCM mode is that both GCM encryption and decryption are parallelizable, ==**allowing you to encrypt or decrypt different plaintext blocks independently.**==
- Many features resemble to those of ==**OCB (Offset Codebook).**==

## ==SIV==

- Synthetic IV is an authenticated cipher mode typically used with AES.
- Unlike GCM and OCB, SIV is secure even if you use the same nonce twice: if an attacker gets two ciphertexts encrypted using the same nonce, ==**they’ll only be able to learn whether the same plaintext was encrypted twice.**==
- Specifically, compute the tag ==**T = PRF(K1, N || P)**== and then compute the ciphertext **==C = E(K2, T, P),==** where T acts as the nonce of E. Thus, SIV needs two keys **==(K1 and K2) and a nonce (N).==**

## ==How Things Can Go Wrong==

- AES-GCM and Weak Hash Keys
    - Specifically, if the value H belongs to some specific, mathematically defined subgroups of all 128-bit strings, ==**attackers might be able to guess a valid authentication tag for some message simply by shuffling the blocks of a previous message.**==
- AES-GCM and Small Tags
    - When a 128-bit tag is used, an attacker who attempts a forgery should succeed with a probability of 1/2^128 because there are 2^128 possible 128-bit tags.
    - But when shorter tags are used, ==**the probability of forgery is much higher than 1/2n due to weaknesses in the structure of GCM that are beyond the scope of this discussion.**==
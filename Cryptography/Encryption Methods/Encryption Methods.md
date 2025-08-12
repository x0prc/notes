---
dg-publish: true
permalink:
---






## ==_Authenticated Encryption_==

- ==**Encryption**== sets **AE(K, P) = (C, T)**, where  
    the authentication tag T is a short string that’s impossible to guess without a key.  
    
- **==Decryption==** takes K, C, and T and returns the plaintext P only if it verifies that T is a valid tag for that plaintext ciphertext pair.
- When K is shared with only one other party, the tag also guarantees that the message was sent by that party; that is, it implicitly ==authenticates== the expected sender as the actual creator.

  

![Screenshot_2023-07-28_at_12.26.10_PM.png](/img/user/img/Screenshot_2023-07-28_at_12.26.10_PM.png)

### Authenticated Encryption with Associated Data (AEAD)

is an extension of authenticated encryption that takes some cleartext and unencrypted data and uses it to generate the authentication tag **==AEAD(K, P, A) = (C, T)==**.

## ==_Format-Preserving Encryption_==

- It can create ciphertexts that ==have the same format== as the plaintext.
- FPE can encrypt IP addresses to IP addresses, ZIP codes to ZIP codes, credit card numbers to credit card numbers with a valid checksum, and so on.

## ==_Fully Homomorphic Encryption_==

- It enables its users to replace a ciphertext, **==C = E(K, P)==**, with another ciphertext, ==**C′ = E(K, F(P))**==, for F(P) can be any function of P, and without ever decrypting the initial C.

## ==_Searchable Encryption_==

- Enables searching over an encrypted database without leaking the searched terms by encrypting the search query itself.
- However, searchable encryption remains experimental within the research community.

## ==_Tweakable Encryption_==

- Is similar to basic encryption, except for an additional parameter called ==the tweak==, which aims to simulate different versions of a cipher.
- The tweak might be a unique per-customer value to ensure that a ==customer’s cipher can’t be cloned== by other parties using the same product.
- In disk encryption, TE encrypts the ==content of storage devices== such as hard drives or solid-state drives.
- TE uses a tweak value  
    that depends on the ==position of the data encrypted==, which is usually a sector  
    number or a block index.  
    

  

![Screenshot_2023-07-28_at_12.42.38_PM.png](/img/user/img/Screenshot_2023-07-28_at_12.42.38_PM.png)
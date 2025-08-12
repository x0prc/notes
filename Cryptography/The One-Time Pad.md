---
dg-publish: true
permalink:
---






> The one-time pad is the most secure cipher. In fact, it guarantees perfect secrecy: even if an attacker has unlimited computing power, it’s impossible to learn anything about the plaintext except for its length.

  

## ==Encryption==

# _C = P ⊕ K_

- Where C (ciphertext) , P (plaintext), and K (random key) are bit strings of the same length and where ⊕ is the bitwise exclusive OR operation (XOR), defined as 0 ⊕ 0 = 0, 0 ⊕ 1 = 1, 1 ⊕ 0 = 1, 1 ⊕ 1 = 0.

  

## ==Decryption==

# _P = C ⊕ K_

- The one-time pad’s decryption is identical to encryption; it’s just an XOR as stated above. Indeed, we can verify C ⊕ K = P ⊕ K ⊕ K = P because XORing K with itself gives the all-zero string 000 . . . 000.
- The important thing is that a one-time pad can only be used one time:  
    each key K should be used only once.  
    

## ==Why is One-Time Pad Secure?==

- If a ciphertext is 128 bits long (meaning the plaintext is 128 bits as well), there are 2^128 possible ciphertexts; therefore, there should be 2^128 possible plaintexts from the attacker’s point of view.

> [!important] You must have a key as long as the plaintext to achieve perfect security, but this quickly becomes impractical for real-world use.
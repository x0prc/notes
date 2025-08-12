---
dg-publish: true
permalink:
---






## ==IND-CPA (indistinguishability against chosen-plaintextattackers)==

- It captures the intuition that ciphertexts shouldn’t leak any information about plaintexts as long as the key is secret.
- Encryption must return different ciphertexts if called twice on the same plaintext; otherwise, an attacker could identify duplicate plaintexts from their ciphertexts.

### ==_Randomized Encryption_==

- Randomizes the encryption process and returns different ciphertexts when the same plaintext is encrypted twice.
- **Encryption** can then be expressed as C = E(K, R, P), ==where R is fresh random bits.==
- **Decryption** remains deterministic, however, because given E(K, R, P), you should always  
    get P, ==regardless of the value of R==.

### ==_Achieving Semantically Secure Encryption_==

- One of the simplest constructions of a semantically secure cipher uses a ==deterministic random bit generator (DRBG)==, an algorithm that returns random looking bits given some secret value:
    
    > [!important] E(K, R, P) = (
    > 
    > **DRBG**(K R) _⊕_ P, R)
    
- Here, R is a string randomly chosen for each new encryption and given to a DRBG along with the key (K || R denotes the string consisting of K followed by R). This approach is reminiscent of the one-time pad: instead of picking a random key of the same length as the message, we ==leverage a random bit generator to get a random-looking string==.
---
dg-publish: true
permalink:
---






- NIST standardized AES in 2000 as a replacement for DES, at which point it became the world’s de facto encryption standard.

## ==AES Internals==

- AES manipulates bytes. It views a 16-byte plaintext as a two-dimensional array of bytes

**==(s = s0, s1, . . . , s15).==**

- The letter s is used because this array is called the ==**internal state**==, or just ==**state**==.
- In order to transform its state, AES uses an SPN structure with 10 rounds for 128-bit keys, 12 for 192-bit keys, and 14 for 256-bit keys.

  

![Screenshot_2023-07-30_at_10.41.45_PM.png](/img/user/img/Screenshot_2023-07-30_at_10.41.45_PM.png)

  

- ==**AddRoundKey**== XORs a round key to the internal state.
- **==SubBytes==** Replaces each byte (s0, s1, . . . , s15) with another byte according to an S-box. In this example, the S-box is a lookup table of 256 elements.
- ==**ShiftRows**== Shifts the ith row of i positions, for i ranging from 0 to 3.
- ==**MixColumns**== Applies the same linear transformation to each of the four columns of the state (that is, each group of cells with the same shade of gray).

  

![Screenshot_2023-07-30_at_10.44.11_PM.png](/img/user/img/Screenshot_2023-07-30_at_10.44.11_PM.png)

## ==Implementing AES==

### ==Table-Based Implementations==

- A combination of ==**XORs and lookups in tables**== hardcoded into the program and loaded in memory at execution time.
- You can build **==four tables with 256 entries each==**, one for each byte value, and implement the sequence SubBytes-MixColumns by looking up four 32-bit values and XORing them together.
- Table-based implementations are vulnerable to **==cache-timing attacks==**, which exploit timing variations when a program reads or writes elements in cache memory.

### ==Native Instructions==

- AES native instructions (AES-NI) ==**solve the problem of cache-timing attacks**== on AES software implementations.
- Instead of coding an AES round as a sequence of assembly instructions, when using AES-NI, you ==**just call the instruction AESENC and the chip will compute the round for you.**==

## ==Modes of Operation==

### ==The Electronic Codebook (ECB) Mode==

- ECB takes plaintext blocks P1, P2, . . . , PN and processes each independently by computing ==**C1 = E(K, P1), C2 = E(K, P2). Simple but insecure operation.**==
- When the ECB mode is used, **==identical ciphertext blocks reveal identical plaintext blocks==** to an attacker, whether those are blocks within a single ciphertext or across different ciphertexts.

### ==The Cipher Block Chaining (CBC) Mode==

- Instead of encrypting the ith block, Pi, as Ci = E(K, Pi), CBC sets ==**Ci = E(K, Pi ⊕ Ci − 1), where Ci − 1 is the previous ciphertext block**==—thereby chaining the blocks (Ci − 1) and Ci.
- When encrypting the first block, P1, there is no previous ciphertext block to use, so CBC takes a random initial value (IV).
- The CBC mode makes each ==**ciphertext block dependent on all the previous blocks**==, and ensures that identical plaintext blocks won’t be identical ciphertext blocks.
    
    ### ==How to Encrypt Any Message in CBC Mode==
    
    - **==Padding a Message==** : A technique that allows you to ==**encrypt a message of any length**==,  
        even one smaller than a single block.  
        - Used to expand a message to fill a complete block by adding extra bytes to the plaintext.
    - ==**Ciphertext Stealing**== : Another trick used to encrypt a message whose length isn’t a multiple of the block size.
        - Extends the last incomplete plaintext block with bits from the previous ciphertext block, and then encrypts the resulting block. The last, incomplete ciphertext block is ==**made up of the first blocks from the previous ciphertext block**==; that is, the bits that have not been appended to the last plaintext block.

### ==The Counter (CTR) Mode==

- CTR is hardly a block cipher mode: it turns a block cipher into a stream cipher that just takes bits in and spits bits out and doesn’t embarrass itself with the notion of blocks.
- Block cipher algorithm won’t transform plaintext data. Instead, it will encrypt blocks ==**composed of a counter and a nonce**==.
- No two blocks ==**should use the same counter within a message,**== but different messages can use the same sequence of counter values (1, 2, 3, . . .).

## ==How Things Can Go Wrong==

### ==Meet-in-the-Middle Attacks (MitM)==

- The 3DES block cipher is an ==**upgraded version of the 1970s standard DES**== that takes a key of 56×3 = 168 bits (an improvement on DES’s 56-bit key).
- 3DES encrypts a block using the ==**DES encryption and decryption functions**==: first encryption with a key, K1, then decryption with a key, K2, and finally encryption with another key, K3.

![Screenshot_2023-07-31_at_7.36.13_PM.png](/img/user/img/Screenshot_2023-07-31_at_7.36.13_PM.png)

![Screenshot_2023-07-31_at_7.36.36_PM.png](/img/user/img/Screenshot_2023-07-31_at_7.36.36_PM.png)

- If K1 = K2, ==**the first two calls cancel themselves out and 3DES boils down to a single DES**== with key K3. 3DES does encrypt-decrypt-encrypt rather than encrypting thrice to allow systems to emulate DES when necessary using the new 3DES interface.
- The whole attack thus succeeds after performing about 2^112 operations, meaning that 3DES ==**gets only 112-bit security despite having 168 bits of key material.**==

### ==Padding Oracle Attacks==

- A padding oracle is a system that behaves differently **==depending on whether the padding in a CBC-encrypted ciphertext is valid==.**
- You can see it as a black box or an API that returns either a ==**success or an error value**==.
- Given a padding oracle, padding oracle attacks ==**record which inputs have a valid padding and which don’t**==, and exploit this information to decrypt chosen ciphertext values.

  

![Screenshot_2023-07-31_at_7.45.09_PM.png](/img/user/img/Screenshot_2023-07-31_at_7.45.09_PM.png)
---
dg-publish: true
permalink:
---






- The **==encryption algorithm==** (E) takes a key, K, and a plaintext block, P, and produces a ciphertext block, C. We write an encryption operation as ==**C = E(K, P)**==.
- The ==**decryption algorithm**== (D) is the inverse of the encryption algorithm and decrypts a message to the original plaintext, P. This operation is written as **==P = D(K, C)==**.

## ==_Block Size_==

- In order to encrypt a 16-bit message when blocks are 128 bits, you’ll ==**first need to convert the message into a 128-bit block**==, and only then will the block cipher process it and return a 128-bit ciphertext.
- As for the memory footprint, in order to process a 128-bit block, **==you need at least 128 bits of memory==**.
    - This is small enough to fit in the registers of most CPUs or to be implemented  
        using dedicated hardware circuits.  
        
- 128-bit or larger blocks are better, mainly because ==**128-bit blocks can be processed more efficiently than 64-bit ones**== on modern CPUs and are also more secure.
    
    ### ==The Codebook Attack==
    
    - While blocks shouldn’t be too large, ==**they also shouldn’t be too small;**== otherwise, they may be susceptible to codebook attacks, which are ==**attacks against block ciphers that are only efficient when smaller blocks are used**==.
    - With 32-bit blocks, **==memory needs grow to 16 gigabytes==**, which is still manageable. But with 64-bit blocks, ==**you’d have to store 270 bits (a zetabit, or 128 exabytes).**==

## ==**_How to Construct Block Ciphers_**==

### ==A Block Cipher’s Rounds==

- In a block cipher, a round is a ==**basic transformation that is simple to specify and to implement**==, and which is iterated several times to form the block cipher’s algorithm.
- For example, a block cipher with three rounds encrypts a plaintextby computing
    
    ==**C = R3(R2(R1(P)))**==, where the rounds are **==R1, R2, and R3 and P is a plaintext==**.
    
- Each round should also have an inverse in order to make it possible for a recipient to compute back to plaintext. Specifically, **==P = iR1(iR2(iR3(C)))==**, where **==iR1 is the inverse of R1==**, and so on.
- These round functions are parameterized by a value called the ==**_round key_**==. Derived from the main key, K, using an algorithm called a _**==key schedule==**_. For example, R1 takes the round key K1, R2 takes the round key K2, and so on.

### ==**The Slide Attack and Round Keys**==

- In a block cipher, no round should be identical to another round in order to avoid a **==slide attack.==** The problem is that ==**knowing the input and output of a single round**== often  
    helps recover the key.  
    

![Screenshot_2023-07-29_at_1.54.29_PM.png](/img/user/img/Screenshot_2023-07-29_at_1.54.29_PM.png)

### ==Substitution-Permutation Networks==

- Substitution often appears in the form of S-boxes, or substitution boxes, which are small lookup tables that transform chunks of 4 or 8 bits.
- The first of the eight S-boxes of the block cipher Serpent is composed of the 16 elements (3 8 f 1 a 6 5 b e d 4 2 7 0 9 c), where each element represents a 4-bit nibble. This particular S-box maps the 4-bit nibble 0000 to 3 (0011), the 4-bit nibble 0101 (5 in decimal) to 6 (0110), and so on.

### ==Feistel Schemes==

1. Split the 64-bit block into two 32-bit halves, L and R.
2. Set L to L ⊕ F(R), where F is a substitution–permutation round.
3. Swap the values of L and R.
4. Go to step 2 and repeat 15 times.
5. Merge L and R into the 64-bit output block.
    
    # L = L ⊕ F(R) & R = R ⊕ F(L)
    
      
    
    ![Screenshot_2023-07-30_at_6.08.36_PM.png](/img/user/img/Screenshot_2023-07-30_at_6.08.36_PM.png)
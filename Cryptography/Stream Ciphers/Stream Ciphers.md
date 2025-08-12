---
dg-publish: true
permalink:
---






- Stream ciphers, don’t mix plaintext and key bits; instead, they ==**generate pseudorandom bits from the key and encrypt the plaintext**== by XORing it with the pseudorandom bits.

## ==How Stream Ciphers Work==

- Stream ciphers are **==more akin to deterministic random bit generators (DRBGs)==** than they are to full-fledged pseudorandom number generators (PRNGs).

1. Stream ciphers produce a pseudorandom stream of bits called the ==**keystream**==.
2. The keystream is ==**XORed to a plaintext to encrypt it**== and then ==**XORed again to the ciphertext to decrypt it.**==

![Screenshot_2023-07-31_at_8.44.39_PM.png](/img/user/img/Screenshot_2023-07-31_at_8.44.39_PM.png)

- SC is the stream cipher algorithm,
- KS the keystream,
- P the plaintext,
- and C the ciphertext.

- A stream cipher computes **==KS = SC(K, N),==** encrypts as ==**C = P ⊕ KS**==, decrypts as ==**P = C ⊕ KS**==.
    - The ==**encryption and decryption functions are the same**== because both do the same thing namely, XOR bits with the keystream.

### ==**Stateful and Counter-Based Stream Ciphers**==

- Stateful stream ciphers ==**have a secret internal**== state that evolves throughout keystream generation.
- The cipher ==**initializes the state from the key**== and the nonce and then calls an update function to **==update the state value==** and produce one or more keystream bits from the state.

![Screenshot_2023-07-31_at_8.53.55_PM.png](/img/user/img/Screenshot_2023-07-31_at_8.53.55_PM.png)

- Counter-based stream ciphers **==produce chunks of keystream from a key==**, a nonce, and a counter value.
- Unlike stateful stream  
    ciphers, such as Salsa20, ==**no secret state is memorized during keystream**  
    **generation.**  
    ==

![Screenshot_2023-07-31_at_8.54.19_PM.png](/img/user/img/Screenshot_2023-07-31_at_8.54.19_PM.png)

## ==Hardware-Oriented Stream Ciphers==

### ==Feedback Shift Registers==

- An FSR is simply an array of bits equipped with ==**an update feed-back function**==, which I’ll denote as f.
- The FSR’s state is stored in the array, or register, and each update of the FSR uses the feedback function to change the state’s value and to produce one output bit.
- If R0 is the initial value of the FSR, the next state, R1, **==is defined as R0 left-shifted by 1 bit,==** where the bit leaving the register is returned as output, and where the **==empty position is==**  
    **filled with f(R0).**  
    - That is, given Rt, the FSR’s state at time t, the next state, Rt + 1, is the following:
        
        ## Rt + 1 = (Rt << 1) | f(Rt)
        
- The bit shift moves the bits to the left, ==**losing the leftmost bit in order to retain the state’s bit length**==, and zeroing the rightmost bit.
- The update operation of an FSR is identical, except that instead of being set to 0, ==**the rightmost bit is set to f(Rt).**==
- We say that ==**5 is the period of the FSR**== given any one of the values 1100, 1000, 0001, 0011, or 0110.

### ==Linear Feedback Shift Registers==

- A function that’s the XOR of some bits of the state, such as the example of a 4-bit FSR in the previous section and its feedback function returning the XOR of the register’s 4 bits.

  

![Screenshot_2023-07-31_at_10.33.35_PM.png](/img/user/img/Screenshot_2023-07-31_at_10.33.35_PM.png)

For example, Figure 5-5 shows a 4-bit LFSR with the feedback polynomial 1 + X + X^3 + X^4 in which the **==bits at positions 1, 3, and 4 are XORed together==** to compute the new bit set to L1.

- The state after five updates is the same as the initial one, demonstrating that we’re in a ==**period-5 cycle and proving that the LFSR’s period isn’t the maximal value of 15**==.
    - Alas, using an LFSR as a stream cipher is insecure. If n is the LFSR’s bit length, an ==**attacker needs only n output bits to recover the LFSR’s initial state**==, allowing them to determine all previous bits and predict all future bits.

### ==Filtered LFSRs==

- To mitigate the insecurity of LFSRs, you can hide their linearity by passing their output bits through a nonlinear function before returning them to produce what is called a filtered LFSR.

![Screenshot_2023-07-31_at_10.41.08_PM.png](/img/user/img/Screenshot_2023-07-31_at_10.41.08_PM.png)

- The g function in Figure 5-7 must be a nonlinear function—one that both XORs bits together and combines them ==**with logical AND or OR operations.**==
- Filtered LFSRs are stronger than plain LFSRs because their ==**nonlinear function thwarts straightforward attacks.**==
- Still, more complex attacks will break the system.

### ==Nonlinear FSRs==

- Are like LFSRs but with a ==**nonlinear feedback function**== instead of a linear one.
- Instead of just bitwise XORs, the feedback function can include bitwise AND and OR operations.
- Benefit of the addition of nonlinear feedback functions is that they make NFSRs ==**cryptographically stronger than LFSRs**== because the output bits depend on the initial secret state in a complex fashion, according to equations of exponential size.
- One downside to NFSRs is that there’s no efficient way to determine an NFSR’s period, or simply to know whether its period is maximal.
- For an NFSR of n bits, you’d need to run close to 2n trials to verify that its period is maximal.

### ==Grain-128a==

- Grain-128a is about as simple as a stream cipher can be, combining a 128-bit LFSR, a 128-bit NFSR, **a**==**nd a filter function, h.**==
- The LFSR has a maximal period of 2^ 128–1, which ensures that the ==**period of the whole system is at least 2^128 – 1 to protect against potential short cycles**== in the NFSR.

![Screenshot_2023-07-31_at_10.58.26_PM.png](/img/user/img/Screenshot_2023-07-31_at_10.58.26_PM.png)

## ==Other Stream Ciphers==

1. A5/1 : 2G Mobile Communication
    1. Subtle Attacks
    2. Brutal Attacks
2. RC4 : Used in countless applications, most famously in the first Wi-Fi encryption standard Wireless Equivalent Privacy (WEP) and in the Transport Layer Security (TLS) protocol.
3. Salsa20
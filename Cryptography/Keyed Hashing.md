---
dg-publish: true
permalink:
---






- Keyed hashing forms the basis of two types of important cryptographic algorithms:
    - Message Authentication Codes (MACs), ==**which authenticate a message and protect its integrity.**==
    - Pseudorandom Functions (PRFs), which produce random-looking hash-sized values.

## ==Message Authentication codes (MACs)==

- A MAC protects a message’s integrity and authenticity by creating a value ==**T = MAC(K, M),**== called the authentication tag of the message, M.
- The protocols in Internet Protocol Security (IPSec), Secure Shell (SSH), and Transport Layer Security (TLS) generate a MAC ==**for each network packet transmitted for secure communication.**==

## ==Pseudorandom Functions (PRFs)==

- A PRF is a function that uses a secret key to return PRF(K, M), such that the output looks random. Because **==the key is secret, the output values are unpredictable to an attacker.==**
- The TLS protocol uses a PRF to generate key material from a master secret as well as session-specific random values.
- There’s even a PRF in the ==**noncryptographic hash() function built into the Python language**== to compare objects.

## ==Dedicated MAC Designs==

- PRFs and MACs should not need the whole power of hash functions or block ciphers, which is the point of dedicated design—==**that is, algorithms created solely to serve as PRFs and/or MACs.**==
- Two such algorithms are :
    1. ==**Poly1305**== ==:== Optimized to be super fast on modern CPUs. It is used by Google to secure HTTPS (HTTP over TLS) connections and by OpenSSH, among many other applications.
        1. Uses a universal hash function internally that is ==**much weaker than a cryptographic hash function, but also much faster**==. Universal hash functions don’t have to be collision resistant, for example. That means less work is required to achieve their security goals. ==**You can use a universal hash as a MAC to authenticate no more than one message.**==
        2. A universal hash is parameterized by a secret key: given a message, M, and key, K, we write UH(K, M), which ==**is the computation of the output of a universal hash function, denoted UH.**==
        3. Initially proposed as Poly1305-AES, ==**combining universal hash with the AES block cipher.**==
    2. ==**SipHash :**== Uses a trick that makes it more secure than basic sponge functions: i==**nstead of XORing message blocks only once before the permutation**==, SipHash XORs them before and after the permutation.
        1. Next, the keys are discarded==**, and computing SipHash boils down to iterating through a core function called SipRound**== and then XORing message chunks to modify the four-word internal state.

## ==How Things Can Go Wrong==

### ==Timing Attacks on MAC Verification==

- MACs can be vulnerable to timing attacks when a ==**remote system verifies tags in a period of time that depends on the tag’s value**==
    - thereby allowing an attacker to **==determine the correct message tag by trying many incorrect ones to determine the one that takes the longest amount of time to complete.==**

### ==When Sponges Leak==

- If a process can read the RAM and registers’ values at any time, or read a core dump of the memory,
    - ==**an attacker can determine the internal state of SHA-3 in MAC mode**==, or the internal state of SipHash,
    - ==**and then compute the reverse of the permutation to recover the initial secret state.**==
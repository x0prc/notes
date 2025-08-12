---
dg-publish: true
permalink:
---






- The field of post-quantum cryptography is about designing public-key algorithms **==that cannot be broken by a quantum computer;==**
    - that is, they would be quantum safe and able to replace RSA and elliptic curve–based algorithms in a future where off-the-shelf quantum computers **==could break 4096-bit RSA moduli in a snap.==**

## ==Code Based Cryptography==

- Code-based post-quantum cryptographic algorithms are based on error-correcting codes, which are techniques designed to transmit bits over a noisy channel.
    - Their main limitation is the size of their public key, ==**which is typically on the order of a hundred kilobytes.**==
- ==_Linear codes_== are an example of less trivial error-correcting codes.
    - In the case of linear codes, a word to encode is seen as an n-bit vector v, and encoding consists of multiplying v with an m × n matrix G to **==compute the code word w = vG.==**
    - G is the public key, and the private key is composed of the matrices A, B, and C such that G = ABC. Knowing A, B, and C allows one to decode a **==message reliably and retrieve w.==**

## ==Lattice Based Cryptography==

- Lattices are mathematical structures that essentially consist of ==**a set of points in an n-dimensional space, with some periodic structure.**==
    
    ![Screenshot_2023-08-17_at_7.55.11_PM.png](/img/user/img/Screenshot_2023-08-17_at_7.55.11_PM.png)
    

1. A first hard problem found in lattice-based crypto is known as short **==integer solution (SIS)==**. SIS consists of finding the secret vector s of n numbers given (A, b) such that b = As mod q, where A is a random m × n matrix and q is a prime number.
2. The second hard problem is called **==learning with errors (LWE)==**. LWE consists of finding the secret vector s of n numbers given (A, b), where b = As + e mod q, with A being a random m × n matrix, e a random vector of noise, and q a prime number.
3. The third problem is **==Closest vector problem (CVP)==** on a lattice, or the problem of finding the vector in a lattice closest to a given point, by combining a set of basis vectors.

> [!important] But this doesn’t directly transfer to secure crypto- systems, because some problems are only hard in the worst case (that is, for their hardest instance) rather than the average case (which is what we need for crypto).

## ==Multivariate Cryptography==

- Multivariate cryptography is about building cryptographic schemes that are as ==**hard to break as it is to solve systems of multivariate equations, or equations involving multiple unknowns.**==
- Equations may be over all real numbers, integers only, or over finite sets of numbers. In cryptography, however, **==equations are typically over numbers modulo some prime numbers, or over binary values (0 and 1).==**
    - This hard problem, known as ==_multivariate quadratics_== (MQ) equations, is therefore a potential basis for **==post-quantum systems because quantum computers won’t solve NP-hard problems efficiently.==**
- The actual hardness of solving such problems depends on the parameters of the scheme, such as the number of equations used, the size and type of the numbers, and so on.
    - ==**But choosing secure parameters is hard, and more than one multivariate scheme considered safe has been broken.**==

## ==Hash-Based Cryptography==

- Based on the well-established security of cryptographic hash functions ==**rather than on the hardness of mathematical problems.**==
- Because quantum computers cannot break hash functions, they cannot break anything that relies on the difficulty of finding collisions, **==which is the key idea of hash function–based signature schemes.==**
- The one-time signature, a trick discovered around 1979, and known as _==Winternitz one-time signature (WOTS)==_, after its inventor.
    - Here “one-time” means that a private key can be used to sign only one message; **==otherwise, the signature scheme becomes insecure.==**
- Significant Limitations :
    - **==Signatures can be forged==**
        - From HashM(K), the signature of M, you can compute Hash(HashM(K)) = HashM + 1(K), which is a valid signature of the message M + 1. This problem can be fixed by signing not only M, but also w – M, using a second key.
    - **==It only works for short messages==**
        - If messages are 8 bits long, there are up to 28 – 1 = 255 possible messages, so you’ll have to compute Hash up to 255 times in order to create a signature.
    - **==It only works once==**
        - If a private key is used to sign more than one message, an attacker can recover enough information to forge a signature.
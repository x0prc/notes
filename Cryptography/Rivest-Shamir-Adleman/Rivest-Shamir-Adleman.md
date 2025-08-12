---
dg-publish: true
permalink:
---






- The RSA was da bomb to the cryptosystem in 1977.
- Public-key encryption (also called asymmetric encryption) uses two keys:
    - one is your public key, which can be used by anyone who wants to encrypt messages for you, and
    - the other is your private key, which is required in order to ==**decrypt messages encrypted using the public key.**==

## ==The Math Behind RSA==

- The algorithm sees the plaintext that it’s encrypting as a positive integer between **==1 and n – 1, where n is a large number called the modulus.==**
    - More precisely, RSA works on the numbers less than n that are co-prime with n and therefore that have no common prime factor with n. **==Such numbers, when multiplied together, yield another number that satisfies these criteria.==**
    - We say that these numbers form a group, ==**denoted Zn*, and call the multiplicative group of integers modulo n.**==

## ==Trapdoor Permutation==

- It calculates the value that’s equal to ==**x multiplied by itself e times modulo n and then returns the result.**==
    - When we use the RSA trapdoor permutation to encrypt, **==the modulus n and the exponent e make up the RSA public key.==**
- In order to get x back from y, we use another number, denoted d, to compute the following:

![Screenshot_2023-08-06_at_9.47.04_AM.png](/img/user/img/Screenshot_2023-08-06_at_9.47.04_AM.png)

- Because d is the trapdoor that allows us to decrypt, it is part of the private key in an RSA key pair, and, unlike the public key, it should always be kept secret. **==The number d is also called the secret exponent.==**

## ==RSA Key Generation and Security==

- Key generation is the process by ==**which an RSA key pair is created**==, namely a public key (modulus n and public exponent e) and its private key (secret exponent d).
- The values p and q should be unrelated random prime numbers of similar size. If they are too **==small, or too close together, it becomes easier to determine their value from n.==**
- Finally, the **==RSA trapdoor permutation should not be used directly for encryption or signing.==**
- In order to generate an RSA key pair, first pick two random prime numbers, p and q, and then compute φ(n) from these, and we compute d as the inverse of e.

## ==Encrypting with RSA==

- Encrypting a message or symmetric key with RSA is more complicated than **==simply converting the target to a number x and computing x^e mod n.==**
- Breaking Textbook RSA Encryption’s Malleability is a simple process.
    - An attacker could create a new valid ciphertext from two RSA ciphertexts, allowing them to compromise the security of your encryption by letting them deduce information about the original message.
- In order to make RSA ciphertexts nonmalleable, the ciphertext should consist of the message data and some **==additional data called padding==**.
    - The standard way to encrypt with RSA in this fashion is to use **==Optimal Asymmetric Encryption Padding (OAEP), commonly referred to as RSA-OAEP.==**
    - This scheme involves creating ==**a bit string as large as the modulus by padding the message with extra data**== and randomness before applying the RSA function.
    - OAEP uses a pseudorandom number generator (PRNG) to ensure the **==indistinguishability and nonmalleability of ciphertexts by making the encryption probabilistic.==**

![Screenshot_2023-08-06_at_10.03.52_AM.png](/img/user/img/Screenshot_2023-08-06_at_10.03.52_AM.png)

## ==Signing with RSA==

- Digital signatures can prove that the holder of the private key tied to a particular digital signature signed some message and that the signature is authentic.

> [!important] Encryption provides confidentiality whereas a digital signature is used to prevent forgeries.

- A signature scheme, however, can process messages of arbitrary sizes by using their hash values Hash(M) as a proxy, and it can be deterministic yet secure.

## ==Breaking Textbook RSA Signatures==

- The method that signs a message, x, by directly computing y = xd mod n, where x can be any number between 0 and n – 1.
- ==**Trivial Forgery :**== Upon noticing that 0d mod n = 0, 1d mod n = 1, and (n – 1)d mod n = n – 1, regardless of the value of the private key d, an attacker can forge signatures of 0, 1, or n – 1 without knowing d.
- ==Blinding Attack :== To launch this attack, you could first find some value, R, such that R eM mod n is a message that your victim would knowingly sign.
    - Next, you would convince them to sign that message and to show you their signature, which is equal to S = (R eM)d mod n, or the message raised to the power d.
    - Now, given that signature, you can derive the signature of M, namely M d, with the aid of some straightforward computations.

## ==PSS Signature Standard==

- Probabilistic Signature Scheme, was designed to make ==**message signing more secure, thanks to the addition of padding data.**==
- One particular benefit of PSS is that you can use it to sign messages of any length, because after hashing a message, ==**you’ll obtain a hash value of the same length regardless of the message’s original length.**==
- To verify a signature given a message, M, you compute Hash1(M) and use the public exponent e to retrieve L and H and then M′ **==from the signature, checking the padding’s correctness at each step.==**

## ==Full Domain Hash Signatures==

- The simplest signature scheme you can imagine. To implement it, you simply **==convert the byte string Hash(M) to a number, x, and create the signature y = xd mod n.==**
- Signature verification is straightforward, too. Given a signature that is a number y, you ==**compute x = ye mod n and compare the result with Hash(M).**==

  

- One way to determine the actual speed of RSA is to use the OpenSSL toolkit :

```Shell
openssl speed rsa512 rsa1024 rsa2048 rsa4096
```
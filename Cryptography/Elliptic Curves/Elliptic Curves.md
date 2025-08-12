---
dg-publish: true
permalink:
---






- ECC multiplies large numbers, but unlike RSA it does so in order ==**to combine points on a mathematical curve, called an elliptic curve.**==
- An elliptic curve as used in cryptography is typically a curve whose equation is of the form ==**y^2 = x^3 + ax + b (known as the Weierstrass form**====)==, where the constants a and b define the shape of the curve.
- For example, as a continuous curve, it shows the points at x = 2.0, x = 2.1, x = 2.00002, and so on. Figure 12-2, shows only integers that satisfy this equation, which excludes decimal numbers.
    
    ![Screenshot_2023-08-15_at_11.09.58_AM.png](/img/user/img/Screenshot_2023-08-15_at_11.09.58_AM.png)
    

## ==Adding Two Points==

- The simplest way to under- stand point addition is to determine the position of R = P + Q on the curve relative to P and Q based on a geometric rule:
    
    - draw the line that connects P and Q, find the other point of the curve that intersects with this line, and Q is the reflection of this point with respect to the x-axis.
    
    ![Screenshot_2023-08-15_at_11.17.08_AM.png](/img/user/img/Screenshot_2023-08-15_at_11.17.08_AM.png)
    

  

- The negative of a point P = (xP, yP) is the point –P = (xP, –yP), which is the point mirrored around the x-axis. For any P, we say that P + (–P) = O, where O is called the point at infinity.

### ==Doubling a Point==

- When P = Q (that is, P and Q are at the same position), adding P and Q is equivalent to computing P + P, also denoted 2P. ==**This addition operation is therefore called a doubling.**==

## ==Multiplicating Two Points==

- In order to multiply points on elliptic curves by a given number k, ==**where k is an integer, we determine the point kP by adding P to itself k – 1 times.**==
    - In other words, 2P = P + P, 3P = P + P + P, and so on.

## ==Elliptic Curve Groups==

- If the points P and Q belong to a given curve, then P + Q also belongs to the curve.
- In practice, most elliptic curve–based cryptosystems work with x and y coordinates that are numbers modulo a prime number, p (in other words, numbers in the finite field Zp).
- Computing the number of points on the curve, also known as its cardinality, group order, or just order. Note that this count includes the point at infinity O.

### ==ECDH (Elliptic Curve Diffi-Hellman)==

- In the case of ECC, for some fixed point G, Alice picks a secret random number dA, computes PA = dAG (the point G multiplied by dA), and sends PA to Bob.
    - Bob picks a secret random dB, computes the point PB = dBG, and sends it to Alice.
    - Then both compute the same shared secret, dAPB = dBPA = dAdBG.
    - This method is called elliptic curve Diffie–Hellman, or ECDH.

## ==Signing with Elliptic Curves==

- The standard algorithm used for signing with ECC is ECDSA, ==**which stands for elliptic curve digital signature algorithm.**==
- ECDSA consists of a signature generation algorithm that the signer uses to create a signature using their private key
    - and a ==**verification algorithm**== that a verifier uses to check a signature’s correctness given the signer’s public key.

### ==ECDSA Sig Gen==

- The signer first hashes the message with a cryptographic hash function such as SHA-256 or BLAKE2 to ==**generate a hash value, h, that is interpreted as a number between 0 and n – 1.**==
    - Next, the signer picks a random number, k, between 1 and n – 1 and computes kG, a point with the coordinates (x, y).
- The length of the signature will **==depend on the coordinate lengths being used.==**
    - a curve where coordinates are 256-bit numbers, r and s would both be 256 bits long, yielding a 512-bit-long signature.

### ==ECDSA Sig Ver==

- Verification algorithm **==succeeds in computing point kG, the same point computed during signature generation.==**
- Validation is complete once a ==**verifier confirms that kG’s x coordinate is equal to the r received**==; otherwise, the signature is rejected as invalid.

## ==Encrypting with EC==

- You can fit only about 100 bits of plaintext, as compared to almost 4000 in RSA with the same security level.
- One simple way to encrypt with elliptic curves is to use the ==**integrated encryption scheme (IES)**==, **==a hybrid asymmetric–symmetric key encryption algorithm==** based on the Diffie–Hellman key exchange.
    - When used with elliptic curves, IES relies on ECDLP’s hardness and is called **==elliptic-curve integrated encryption scheme (ECIES).==**

## ==Types of Curves==

- NIST
- Curve25519
- ANSSI
- Brainpool
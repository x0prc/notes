---
dg-publish: true
permalink:
---






- A protocol that allows two parties to ==**establish a shared secret by exchanging information visible to an eavesdropper**== is known as the Diffie–Hellman (DH) protocol.
    - The DH protocol — and its variants — are therefore called key agreement protocols.

## ==DH Function==

- The DH function will usually work with groups denoted Zp (From [[src/site/notes/src/site/notes/src/site/notes/src/site/notes/main/CS/Cryptography/Hard Problems\|Hard Problems]])
    - Another public parameter is the ==**base number, g**==. All arithmetic operations are performed **==modulo p.==**
- DH works its magic by combining either public value with the other private value, such that the result is the same in both cases: Ab = (ga)b = gab and Ba = (gb)a = gba = gab.
    - The resulting value, gab, is the shared secret; it is then passed **==to a key derivation function (KDF) in order to generate one or more shared symmetric keys.==**

```Shell
time openssl dhparam 2048
```

### ==Computational Diffie-Hellman Problem==

- The computational Diffie–Hellman (CDH) problem is that of computing the shared secret gab ==**given only the public values ga and gb, and not any of the secret values a or b.**==
- the DH protocol with a 2048-bit prime p will get you about the same security that RSA with a 2048-bit modulus n offers, which is about 90 bits.

### ==Decisional Diffie-Hellman Problem==

- Given ga, gb, and a value that is either gab or gc for some random c (each of the two with a chance of 1/2), the DDH problem consists of determining whether gab (the shared secret corresponding to ga and gb) was chosen.
    - The assumption that no attacker can solve DDH efficiently is called the Decisional Diffie–Hellman assumption.

## ==Key Agreement Protocols==

- Protocols designed to secure communication between two or more parties communicating over a network with the aid of a shared secret.
- A Non-DH Key Agreement Authentication :
    
    ![Screenshot_2023-08-07_at_10.35.54_PM.png](/img/user/img/Screenshot_2023-08-07_at_10.35.54_PM.png)
    
- An attacker who compromises K can perform a man-in-the-middle attack and ==**listen to all cleartext communication.**==

### ==Attack Models in KA Protocols==

- The eavesdropper
- The data leak
- The breach

### ==Security Goals==

- Authentication
- Key control
- Forward secrecy
- Resistance to key-compromise impersonation (KCI)

## ==DH Protocols==

### ==Anonymous DH==

- It’s called anonymous because it’s not authenticated; the participants **==have no identity that can be verified by either party, and neither party holds a long-term key.==**
    - Each party picks a random value (a for Alice and b for Bob) to **==use as a private key, and sends the corresponding public key to the other peer.==**

![Screenshot_2023-08-07_at_10.58.26_PM.png](/img/user/img/Screenshot_2023-08-07_at_10.58.26_PM.png)

### ==Authenticated DH==

- Equips the two parties ==**with both a private and a public key,**== thereby allowing Alice and Bob to sign their messages **==in order to stop Eve from sending messages on their behalf.==**
    - In order to successfully send messages on behalf of Alice, an attacker would need to forge a valid signature, **==which is impossible with a secure signature scheme.==**

![Screenshot_2023-08-07_at_11.02.09_PM.png](/img/user/img/Screenshot_2023-08-07_at_11.02.09_PM.png)

## ==Menezes–Qu–Vanstone (MQV)==

- MQV is Diffie–Hellman on steroids. It’s **==more secure than authenticated DH, and it improves on authenticated DH’s performance properties.==**
- In particular, ==**MQV allows users to send only two messages, independently of each other, in arbitrary order.**==
    
      
    

![Screenshot_2023-08-07_at_11.05.58_PM.png](/img/user/img/Screenshot_2023-08-07_at_11.05.58_PM.png)

- Other benefits are that **==users can send shorter messages==** than they would be able to with authenticated DH, and **==they don’t need to send explicit signature or verification messages.==**
    
    - Despite its elegance and security, MQV is rarely used in practice. One reason is because **==it used to be encumbered by patents, which hampered its widespread adoption.==**
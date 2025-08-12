---
dg-publish: true
permalink:
---






- An attack model is a set of assumptions about how attackers might interact with a cipher and what they can and can’t do.

## ==**Kerckhoffs’s Principle**==

- Security of a cipher should rely only on the secrecy of the key and not on the secrecy of the cipher.

## ==Black-Box Models==

- A query for our purposes is the operation that sends an input value to some function  
    and gets the output in return, ==without exposing the details of that function==.
- For example, some smart card chips securely protect a cipher’s internals as well as its keys, yet you’re allowed to ==connect to the chip and ask it to decrypt any ciphertext==.

### 1. Ciphertext-only attackers (COA)

Observe ciphertexts but don’t know the associated plaintexts, and don’t know how the plaintexts were selected.

### 2. Known-plaintext attackers (KPA)

Observe ciphertexts and do know the associated plaintexts.

### 3. Chosen-plaintext attackers (CPA)

Can perform encryption queries for plaintexts of their choice and observe the resulting ciphertexts.

### 4. Chosen-ciphertext attackers (CCA)

Can both encrypt and decrypt.

## ==Gray-Box Models==

- In a gray-box model, the attacker has access to a ==cipher’s implementation==.
- By the same token, gray-box models are more difficult to define than black-box ones because they ==depend on physical, analog properties== rather than just on an algorithm’s input and outputs, and crypto theory will often fail to abstract the complexity of the real world.

### Side-Channel Attacks

- Are a family of attacks within gray-box models. A side channel is a source of information that depends on the implementation of the cipher, ==be it in software or hardware==.
- Observe or measure analog characteristics of a cipher’s implementation but don’t alter its integrity; ==they are noninvasive==.

### Invasive Attacks

- Are a family of attacks on cipher implementations that are more powerful than side-channel attacks, and more expensive because they ==require sophisticated equipment==.
- Invasive attacks thus consist of a whole set of techniques and procedures, from using ==nitric acid to remove a chip’s packaging to microscopic imagery acquisition==, partial reverse engineering, and ==possible modification of the chip’s behavior== with something like laser fault injection.
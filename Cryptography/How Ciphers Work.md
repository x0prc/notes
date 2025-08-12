---
dg-publish: true
permalink:
---






## ==The Permutation==

- A cipher’s substitution can’t be just any substitution. It should be a permutation, which is a rearrangement of the letters A to Z, such that each letter has a unique inverse.
- For example, a substitution that transforms the letters A, B, C, and D, respectively to C, A, D, and B is a permutation, because each letter maps onto another single letter. Each letter has exactly one inverse.

### ==In order to be secure, a cipher’s permutation should satisfy three criteria:==

1. The permutation should be determined by the key.
2. Different keys should result in different permutations.
3. The permutation should look random.

## ==Mode of Operation==

- The mode of operation (or just mode) of a cipher mitigates the exposure of duplicate letters in the plaintext by using different permutations for duplicate letters.
    - However, this can still result in patterns in the ciphertext because every Nth letter of the message uses the same permutation. That’s why frequency analysis works to break the Vigenère cipher.
- To build a secure cipher, a secure permutation with a secure mode should be combined.
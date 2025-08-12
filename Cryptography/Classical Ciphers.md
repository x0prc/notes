---
dg-publish: true
permalink:
---






## ==The Caeser Cipher==

- It encrypts a message by shifting each of the letters down three positions in the alphabet, wrapping back around to A if the shift reaches Z.
- The Caesar cipher is super easy to break: to decrypt a given ciphertext,  
    simply shift the letters three positions back to retrieve the plaintext.  
    
- C A E S A R → F D H V D U

## ==The Vigenere Cipher==

- Letters aren’t shifted by three places but rather by values defined by a key, a collection of letters that represent numbers based on their position in the alphabet.
- If the key is DUH, letters in the plaintext are shifted using the  
    values 3, 20, 7 because D is three letters after A, U is 20 letters after A, and H  
    is seven letters after A.  
    
- T H E Y D R I N K T H E T E A → W B L B X Y L H R W B L W Y H
- The group of three letters WBL appears twice in the ciphertext at nine-letter intervals. This suggests that the same three-letter word was encrypted using the same shift values, producing WBL each time. A cryptanalyst can then deduce that the key’s length is either nine or a value divisible by nine (that is, three).
- Cryptanalyst may also determine DUH as a possible encryption key.
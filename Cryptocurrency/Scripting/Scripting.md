---
dg-publish: true
permalink:
---






## ==Design Goals==

1. Built for Bitcoin (inspired by **Forth**)
2. Simple, compact
3. Support for cryptography
4. Stack-based
5. Limits on time/memory
6. No looping

  

## ==Script Executable Example==

```HTML
<sig> <pubKey> OP_DUP OP_HASH160 <pubKeyHash?> OP_EQUALVERIFY OP_CHECKSIG
```

OP_DUP : Take values on the top of the stack, pop it off, write two copies back to the stack.

HASH160 : Take the top value and convert into a hash

OP_EQUALVERIFY : Verifying the top values of the stack are equal. If error, exec will stop.

OP_CHECKSIG : Checks the signature from both the ends.

  

## ==Script Instructions==

1. 256 opcodes total [1 byte each] (15 disabled, 75 reserved)
    
    1. Arithmetic
    2. if/then
    3. Logic/Data Handling
    4. Crypto
        1. Hashes
        2. Signature Verification
        3. Multi-Signature Verification
    
      
    
    > [!important] OP_CHECKMULTISIG lets you check multiple signatures at once - Has built in support for joint signatures - Specify n public keys and parameter t - Verification requires t signatures
    
      
    
    ### Sender’s Script (Has to send the complete hash)
    
    ```HTML
    OP_HASH160
    <hash of redemption script>
    OP_EQUAL
    ```
    
      
    
    ### Receiver’s Script (Has to verify the whole hash sender sent)
    
    ```HTML
    <signature>
    <<pubkey> OP_CHECKSIG>
    ```
    
      
    
    ## ==Applications of Scripting==
    
    1. Escrow Transactions : Involving 3rd parties in the transaction pipe with MULTISIG
    2. Green Addresses : Involving a bank in the transaction. (Not used much in practice)
    
    - Efficient Micro-Payments : All of the transactions could be double spend.
        
        ![Screenshot_2023-07-12_at_5.48.13_PM.png](/img/user/img/Screenshot_2023-07-12_at_5.48.13_PM.png)
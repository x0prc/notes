---
dg-publish: true
permalink:
---






- A cipher is **==t-secure==** when a successful attack needs at least ==**t**== operations.
- We then express security in bits, where ==**“n-bit security”**== means that about ==**2^n**== operations are needed to compromise some particular security notion.
    - If it takes 1000000 operations, the security level is log2(1000000), or about 20 bits (that is, 1000000 is approximately equal to 2^20).

  

- Bit security proves useful when ==**comparing ciphers’ security levels**== but doesn’t provide enough information on the actual cost of an attack.
    - It is sometimes too simple an abstraction because ==**it just assumes that an n-bit-secure cipher**== takes 2n operations to break, whatever these operations are.

## ==_Full Attack Cost_==

- Bit security expresses the cost of the fastest attack against a cipher by estimating ==**the order of magnitude of the number of operations**== it needs to succeed.
- Other factors are as follows :
    
    ### ==Parallelism==
    
    - For example, consider two attacks of 2^56 operations each. The difference between the two is that the second attack can be parallelized but not the first.
    - The first attack performs ==**256 sequentially dependent operations**==, such as xi + 1 = fi(xi) for some x0 and some functions fi (with i from 1 to 256), whereas the second performs ==**256 independent operations**==, such as xi = fi(x) for some x and i from 1 to 256, which can be executed in parallel.
    - Parallel processing can be **==orders of magnitude faster than sequential processing==**.
    - The first attack, however, ==**cannot benefit from having multiple cores available**== because each operation relies on the previous operation’s result.
    
    ### ==Memory==
    
    - Concerning the way space is used, it’s important to consider
        - how many memory lookups are required as part of an attack,
        - the speed of memory accesses (which may differ between reads and writes),
        - the size of the data accessed,
        - the access pattern (contiguous or random memory addresses),
        - and how data is structured in memory.
    
    ### ==Precomputation==
    
    - Need to be **==performed only once and can be reused over subsequent executions==** of the attack. Precomputation is sometimes called the ==**offline stage of an attack.**==
    
    ### ==Number of Targets==
    
    - The greater the number of targets, the greater the attack surface, and ==**the more attackers can learn about the keys they’re after.**==
    - For example, to break one 128-bit key of 2^16 = 65536 target keys, it will take on average 2^128 - 16 = 2^112 evaluations of the cipher. That is, ==**the cost (and speed) of the attack decreases as the number of targets increases.**==
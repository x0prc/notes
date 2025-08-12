---
dg-publish: true
permalink:
---






## ==Computational Hardness==

- The property of computational problems for which there is ==**no algorithm that will run in a reasonable amount of time.**== Such problems are also called **==intractable problems==** and are often practically impossible to solve.

## ==Measuring Running Time==

- ==**Computational complexity**==, or the approximate number of operations done by an algorithm as a function of its input size. The size is **==counted in bits or in the number of elements taken as input.==**
    1. Given a list of n values in a random order, you’ll need on average n × log n basic operations to sort the list, which is sometimes called ==**Linearithmic complexity**==.
    2. ==**Exponential complexity**== means a problem that is practically impossible to solve, because as n grows, the effort very rapidly becomes infeasible.
    3. **==Quadratic complexity==** is somewhere between the two.

## ==Polynomial vs. Superpolynomial Time==

- Polynomial-time algorithms are eminently important in complexity theory and in crypto because ==**they’re the very definition of practically feasible.**==
- When an algorithm runs in polynomial time, or polytime for short, **==it will complete in a decent amount of time even if the input is large.==**
- In contrast, algorithms running in superpolynomial time — that is, in O(f(n)), where f(n) is any **==function that grows faster than any polynomial — are viewed as impractical.==**

## ==Complexity Classes==

- A class is a group of objects ==**with some similar attribute.**==
- All computational problems solvable in time O(n2) denoted as ==**TIME(n^2)**== are one class.
    - ==**TIME(n3)**== is the class of problems solvable in time O(n3)
    - **==TIME(2n)==** is the class of problems solvable in time O(2n) and so on.
- Any problem in the class TIME(n2) also belongs to the class TIME(n3), which both also belong to the class TIME(n4), and so on. **==The union of all these classes of problems, TIME(nk)==**, where k is a constant, **==is called P, which stands for polynomial time.==**
- When selecting an algorithm, you should not only consider its time complexity but also how much memory it uses, **==or its space complexity.==**

## ==Factoring Large Numbers==

- Fastest factoring algorithm is the ==**general number field sieve (GNFS)**==
- However, it’s difficult to get an accurate estimate of GNFS’s actual complexity for a given number size therefore we have to rely on heuristical complexity estimates, **==which show how security increases with a longer n.==**
    - Factoring a 1024-bit number, which would have two prime factors of approximately 500 bits each, will take on the order of 270 basic operations.
    - Factoring a 2048-bit number, which would have two prime factors of approximately 1000 bits each, will take on the order of 290 basic operations, which is about a million times slower than for a 1024-bit number.
- Discrete Logarithm Problem deals with the same issue of factoring problem in the history of cryptography.
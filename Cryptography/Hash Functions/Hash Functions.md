---
dg-publish: true
permalink:
---






- Hash functions take a long input and produce a short output, called a ==**_hash value or digest_**==.
    - Usually 256 or 512 bits.
- The general, theoretical definition of a secure hash function is that it behaves like a ==_**truly random function (sometimes called a random oracle)**_==. Specifically, a secure hash function shouldn’t have any property or pattern.

## ==Secure Hash Functions==

- ==**Protect data integrity**== in an effort to guarantee that data—whether sent in the clear or encrypted—hasn’t been modified.
- When digital signatures are used, applications process the hash of the ==**message to be signed rather than the message itself**==.
- Specific notions are Preimage Resistance and Collision Resistance.

### ==Preimage Resistance==

- A preimage of a given hash value, H, is any message, M, such that Hash(M) = H.
- Sometimes called one-way functions because ==_**you can go from the message to its hash**_==, but not the other way.
- For example, there are 2^256 possible values of a 256-bit hash (a typical length with hash functions used in practice), but there are many more values of, say, 1024-bit messages (namely, 2^1024 possible values). Therefore, it follows that, on average, each possible 256-bit hash value will have 2^1024 / 2^256 = 2^1024 – 256 = ==_**2^768 preimages of 1024 bits each.**_==

### ==The Cost of Preimages==

- Given a hash function and a hash value, you can ==_**search for first preimages**_== by trying different messages until one hits the target hash.

```C++
find-preimage(H){
	repeat {
			M = random_message()
			if Hash(M) == H then return M
		}
}
```

- That’s a hopeless situation when working with n = 256, as in modern hashes like SHA-256 and BLAKE2.

```C
solve-second-preimage(M) {
    H = Hash(M)
    return solve-preimage(H)
}
```

- The best attack we can use to find second preimages is ==_**almost identical to the best attack we can use to find first preimages**_== (unless the hash function has some defect that allows for more efficient attacks).

### ==Collision Resistance==

- Collisions will inevitably exist due to the _**==pigeonhole principle==**_, which states that if you have m holes and n pigeons to put into those holes, and if n is greater than m, ==_**at least one hole must contain more than one pigeon.**_==
- However, despite the inevitable, ==**_collisions should be as hard to find as the original message_**== in order for a hash function to be considered collision resistant.

```C++
solve-collision() {
    M = random_message()
    return (M, solve-second-preimage(M))
}
```

- ==**_Collision Search_**==
    - _**==The Rho method==**_ is an algorithm for finding collisions that requires only a small amount of memory.
    - The sequence of H i s eventually enters a loop, also called a cycle, which resembles the _**==Greek letter rho (ρ) in shape==**_.

![Screenshot_2023-08-01_at_8.30.31_PM.png](/img/user/img/Screenshot_2023-08-01_at_8.30.31_PM.png)

- On average, the cycle and the tail (the part that extends from H1 to H5 in Figure 6-3) each include about 2n/2 hash values, where n is the bit length of the hash values. Therefore, you’ll ==_**need at least 2n/2 + 2n/2 evaluations of the hash to find a collision.**_==

## ==Building Hash Functions==

- The simplest way to hash a message is to ==_**split it into chunks and process each chunk**_== consecutively using a similar algorithm. This strategy is called ==_**iterative hashing**_==, and it comes in two main forms
    1. ==**Compression Function**== : Transforms an input to a smaller output.
    2. ==**Sponge Function**== : Transforms an input to an output of the same size, such that any two different inputs give two different out- puts (that is, a permutation).

### ==Compression Based Hash Functions==

- Also called ==_**Merkle-Damgard Construction**_== after the cryptographers who invented the algorithm.
    - MD4, MD5, SHA-1, and the SHA-2 family, as well as the lesser-known RIPEMD and Whirlpool hash functions are all based on CBHF.

![Screenshot_2023-08-01_at_8.37.39_PM.png](/img/user/img/Screenshot_2023-08-01_at_8.37.39_PM.png)

- To hash a message, the M–D construction splits the message into blocks of identical size and ==_**mixes these blocks with an internal state using a compression function.**_==

> [!important] The block length is fixed for a given hash function. For example, SHA-256 works with 512-bit blocks and SHA-512 works with 1024-bit blocks.

- ==**Padding Blocks**== : Take the chunk of bits left, append 1 bit, then append 0 bits, and finally append the length of the original message, encoded on a fixed number of bits.
    - This padding trick guarantees ==**_that any two distinct messages will give a distinct sequence of blocks_**==, and thus a distinct hash value.
- ==**Multicollisions**== : Occurs when a set of three or more messages hash to the same value.
    - Ideally, multicollisions ==_**should be much harder to find than collisions**_== but there is an easy way for finding them at almost the same cost as tht of a single collision.
    - Repeat and find N times a collision, and you’ll have 2N N-block messages hashing to the same value, or a 2N collision, at the cost of “only” about N2N hash computations.

### ==Sponge Functions==

- Instead of using a ==_**block cipher to mix message bits with the internal state**_==, sponge functions just do an XOR operation.
- The most famous sponge function is Keccak, also known as SHA-3.

![Screenshot_2023-08-01_at_8.56.04_PM.png](/img/user/img/Screenshot_2023-08-01_at_8.56.04_PM.png)

**Steps** :

1. It XORs the first message block, M1, to H0, a _**==predefined initial value of the internal state==**_ (for example, the all-zero string). Message blocks are all the same size and smaller than the internal state.
2. A permutation, P, ==_**transforms the internal state**_== to another value of the same size.
3. It XORs block M2 and applies P again, and then repeats this for the message blocks M3, M4, and so on. _**==This is called the absorbing phase==**_.
4. After injecting all the message blocks, it applies P again and extracts a block of bits from the state to form the hash. (If you need a longer hash, apply P again and extract a block.) _**==This is called the squeezing phase.==**_

## ==SHA-1==

- In 1995 the NSA released SHA-1 to fix an unidentified security issue in SHA-0.
- The reason for the tweak became clear when in 1998 two researchers discovered how to find collisions for ==**_SHA-0 in about 2^60 operations instead of the 2^80 expected for 160-bit hash functions such as SHA-0 and SHA-1._**==

## ==SHA-2==

- SHA-2 is a family of four hash functions: SHA-224, SHA-256, SHA-384, and SHA-512, of which SHA-256 and SHA-512 are the two main algorithms.
- The three-digit numbers represent the bit lengths of each hash.
    
    ### ==SHA-256==
    
    - SHA-256 has ==_**256-bit chaining values**_== or eight 32-bit words.
    - Both SHA-1 and SHA-256 have 512-bit message blocks; however, whereas SHA-1 makes 80 rounds, ==_**SHA-256 makes 64 rounds**_==, expanding the 16-word message block to a 64-word message block using the ==_**expand256() function.**_==

## ==SHA-3==

- Five Finalists :
    1. **==BLAKE==** : An enhanced Merkle–Damgård hash whose compression function is based on a block cipher, which is in turn based on the ==**_core function of the stream cipher ChaCha, a chain of additions, XORs, and word rotations._**==
    2. ==**Grostl**== : An enhanced Merkle–Damgård hash whose compression function ==_**uses two permutations (or fixed-key block ciphers)**_== based on the core function of the AES block cipher.
    3. ==**JH**== : A tweaked sponge function construction ==_**wherein message blocks are injected before and after the permutation rather than just before**_==. The permutation also performs operations similar to a substitution– permutation block cipher.
    4. ==**Keccak**== : A sponge function _**==whose permutation performs only bitwise operations.==**_
    5. ==**Skein**== : Compression function is _**==based on a novel block cipher that uses only integer addition, XOR, and word rotation.==**_
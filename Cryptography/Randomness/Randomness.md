---
dg-publish: true
permalink:
---






## ==**Entropy: A Measure of Uncertainty**==

- We can compute the entropy of a probability distribution.
- If your distribution consists of probabilities p1, p2, . . . , pN, then its entropy is the negative sum of all probabilities multiplied by their logarithm, as shown in this expression:

![Screenshot_2023-07-28_at_1.01.39_PM.png](/img/user/img/Screenshot_2023-07-28_at_1.01.39_PM.png)

- Unlike the natural logarithm, **==the binary logarithm expresses the information in bits==** and yields integer values when probabilities are powers of two.
- Entropy is maximized when the distribution is uniform because a uniform distribution maximizes uncertainty: no outcome is more likely than the others.

## ==**RNGs & PRNGs**==

### ==_**Random Number Generators**_==

- A **==source of uncertainty==**, or source of entropy, provided by random number generators (RNGs).
- A cryptographic algorithm to produce ==**high-quality random bits from the source of entropy**==. This is found in pseudorandom number generators (PRNGs).
- In cryptography, ==**randomness usually comes from random number generators (RNGs)**==, which are software or hardware components that leverage entropy in the analog world to produce unpredictable bits in a digital system.

### ==_Quantum Random Number Generators (QRNGs)_==

- A type of RNG that relies on the randomness arising from ==**quantum mechanical phenomena**== such as radioactive decay, vacuum fluctuations, and observing photons’ polarization.
- These can provide real randomness, rather than ==**just apparent randomness**==.

### **_==Pseudorandom number generators (PRNGs)==_**

- Address the challenge we face in generating randomness by **==reliably producing many artificial random bits==** from a few true random bits.
- PRNGs **==produce random-looking bits quickly from digital sources==**, in a deterministic way, and with maximum entropy.
    
    ![Screenshot_2023-07-28_at_1.17.58_PM.png](/img/user/img/Screenshot_2023-07-28_at_1.17.58_PM.png)
    

### _==How PRNGs Work==_

- A PRNG receives random bits from an RNG at regular intervals and uses them to update the contents of a large memory buffer, called the ==**entropy pool.**==
    - When the PRNG updates the entropy pool, ==**it mixes the pool’s bits together**== to help remove any statistical bias.
- In order to generate pseudorandom bits, the PRNG runs a ==**deterministic random bit generator (DRBG) algorithm**== that expands some bits from the entropy pool into a much longer sequence.
    - The PRNG ensures that its DRBG ==**never receives the same input twice**==, in order to generate unique pseudorandom sequences.
- Performs three operations:
    
    1. _init()_ ➜ Initializes the entropy pool and the internal state of the PRNG.
    2. _refresh(R) ➜_ Updates the entropy pool using some data, R, usually  
        sourced from an RNG.  
        
    3. _next(N)_ ➜ Returns N pseudorandom bits and updates the entropy pool.
    
      
    

> [!important] The following command uses /dev/urandom to write 10MB of random bits to a file:

```Shell
dd if=/dev/urandom of=<output file> bs=1M count=10
```

## ==A Safer Way to use /dev/urandom==

```C
int random_bytes_safer(void *buf, size_t len)
{
struct stat st;
size_t i;
int fd, cnt, flags;
int save_errno = errno;
start:
flags = O_RDONLY;
\#ifdef O_NOFOLLOW
flags |= O_NOFOLLOW;
\#endif
\#ifdef O_CLOEXEC
flags |= O_CLOEXEC;
\#endif
fd = uopen("/dev/urandom", flags, 0);
if (fd == -1) {
if (errno == EINTR)
goto start;
goto nodevrandom;
}
\#ifndef O_CLOEXEC
fcntl(fd, F_SETFD, fcntl(fd, F_GETFD) | FD_CLOEXEC);
\#endif
/* Lightly verify that the device node looks sane */
if (fstat(fd, &st) == -1 || !S_ISCHR(st.st_mode)) {
close(fd);
goto nodevrandom;
}
if (ioctl(fd, RNDGETENTCNT, &cnt) == -1) {
close(fd);
goto nodevrandom;
}
for (i = 0; i < len; ) {
size_t wanted = len - i;
ssize_t ret = vread(fd, (char *)buf + i, wanted);
if (ret == -1) {
if (errno == EAGAIN || errno == EINTR)
continue;
close(fd);
goto nodevrandom;
}
i += ret;
}
close(fd);
if (gotdata(buf, len) == 0) {
errno = save_errno;
return 0;		 /* satisfied */
}
nodevrandom:
errno = EIO;
return -1;
}
```
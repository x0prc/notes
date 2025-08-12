---
dg-publish: true
permalink:
---






## ==1. Collision Free:==

_Nobody can find x and y such that:_

> [ x!=y and Hash(x) = Hash(y) ]

  

_How to find collisions:_  
  
try 2**(130) randomly chosen inputs  
99.8% chance that two will collide  

##   
  
==2. Hiding Property:==

r is chosen form a probability distribution that has high min-entropy, then given H( r | x), it is infeasible to find x.

> _high min-entropy means that distribution is “very spread out”, so that no particular value is chose with more than negligible probability._

  

## ==3. Commitment API:==

```Plain
(com, key) := commit(msg)
match := verify(com, key, msg)
```

  

To seal a message:

```Plain
(com, key) := commit(msg) — then publish com
```

To open the sealed message:

```Plain
publish key, msg 

anyone can use verify() to check validity
```

  

```Plain
commit(msg) := (H(key | msg), key)
									where key is random 256-bit value

verify(com, key, msg) := (H(key | msg) == com)
```

  

## ==4. Security Properties:==

### Hiding

Infeasible to find the message

### Binding

Infeasible to find msg ≠ msg

### Puzzle Friendly

- For every possible output value y, if k is chosen from a distribution with high min entropy, then it is infeasible to find x such that H(k | x) = y.
- Implies that no solving strategy is much better than trying random values of x.
- Y is the target set for various solutions of x.
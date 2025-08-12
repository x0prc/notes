---
dg-publish: true
permalink:
---






- Common errors are frame errors, drops, overruns, and collisions.
    - These errors reduce performance, but don’t necessarily bring the link down.

## ==Windows==

```Shell
netstat -e
```

- The Discards and Errors should always be zero in an ideal world, but a small number is probably okay.

## ==Unix==

```Shell
netstat -i

netstat -w (Updates every few seconds)
```
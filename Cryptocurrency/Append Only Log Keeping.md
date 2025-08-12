---
dg-publish: true
permalink:
---






## ==Timestamping==

- Idea 1 : Specify the hash of your data instead of a valid public key
    - Send 1 satoshi to the address
- Idea 2 : Brute-force a public key & signature starting with the first n bits of ata hash.

## ==Provably unspendable commitments==

- Many websites do this for their customers and publish one unspendable output all together for everyone something of this sort :

```Markdown
OP_RETURN
<arbitrary data>
```
---
dg-publish: true
---






- Verify that the query is returning three columns, using the following payload in the `category` parameter:

```Plain
'+UNION+SELECT+NULL,NULL,NULL--
```

- Try replacing each null with the random value provided by the lab, for example:
    - `'+UNION+SELECT+'abcdef',NULL,NULL--`
    - Replace via Inspector → Selection
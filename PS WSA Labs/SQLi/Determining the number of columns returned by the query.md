---
{"dg-publish":true,"permalink":"/src/site/notes/src/site/notes/src/site/notes/src/site/notes/main/cs/ps-wsa-labs/sq-li/determining-the-number-of-columns-returned-by-the-query/"}
---






- Modify the `category` parameter, giving it the value `'+UNION+SELECT+NULL--`. Observe that an error occurs.
- Modify the `category` parameter to add an additional column containing a null value:`'+UNION+SELECT+NULL,NULL--`
- Keep adding NULLs till a 200 occurs.
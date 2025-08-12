---
{"dg-publish":true,"permalink":"/src/site/notes/src/site/notes/src/site/notes/src/site/notes/main/cs/ps-wsa-labs/csrf/csrf-where-referer-validation-depends-on-header-being-present/"}
---






1. Open Burp's browser and log in to your account. Submit the "Update email" form, and find the resulting request in your Proxy history.
2. Send the request to Burp Repeater and observe that if you change the domain in the Referer HTTP header then the request is rejected.
3. Delete the Referer header entirely and observe that the request is now accepted.
4. Create and host a proof of concept exploit as described in the solution to the [CSRF vulnerability with no defenses](https://portswigger.net/web-security/csrf/lab-no-defenses) lab. Include the following HTML to suppress the Referer header:`<meta name="referrer" content="no-referrer">`
5. Change the email address in your exploit so that it doesn't match your own.
6. Store the exploit, then click "Deliver to victim" to solve the lab.
---
dg-publish: true
---






1. In Burp's browser, log in to your own account and change your email address.
2. In Burp, go to the **Proxy > HTTP history** tab.
3. Study the `POST /my-account/change-email` request and notice that this doesn't contain any unpredictable tokens, so may be vulnerable to CSRF if you can bypass the SameSite cookie restrictions.
4. Look at the response to your `POST /login` request. Notice that the website doesn't explicitly specify any SameSite restrictions when setting session cookies. As a result, the browser will use the default `Lax` restriction level.
5. Recognize that this means the session cookie will be sent in cross-site `GET` requests, as long as they involve a top-level navigation.

### **Bypass the SameSite restrictions**

1. Send the `POST /my-account/change-email` request to Burp Repeater.
2. In Burp Repeater, right-click on the request and select **Change request method**. Burp automatically generates an equivalent `GET` request.
3. Send the request. Observe that the endpoint only allows `POST` requests.
4. Try overriding the method by adding the `_method` parameter to the query string:`GET /my-account/change-email?email=foo%40web-security-academy.net&_method=POST HTTP/1.1`
5. Send the request. Observe that this seems to have been accepted by the server.
6. In the browser, go to your account page and confirm that your email address has changed.

### **Craft an exploit**

1. In the browser, go to the exploit server.
2. In the **Body** section, create an HTML/JavaScript payload that induces the viewer's browser to issue the malicious `GET` request. Remember that this must cause a top-level navigation in order for the session cookie to be included. The following is one possible approach:`<script> document.location = "https://YOUR-LAB-ID.web-security-academy.net/my-account/change-email?email=pwned@web-security-academy.net&_method=POST"; </script>`
3. Store and view the exploit yourself. Confirm that this has successfully changed your email address on the target site.
4. Change the email address in your exploit so that it doesn't match your own.
5. Deliver the exploit to the victim to solve the lab.
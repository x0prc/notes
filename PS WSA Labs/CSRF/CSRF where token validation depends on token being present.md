---
dg-publish: true
---






1. Open Burp's browser and log in to your account. Submit the "Update email" form, and find the resulting request in your Proxy history.
2. Send the request to Burp Repeater and observe that if you change the value of the `csrf` parameter then the request is rejected.
3. Delete the `csrf` parameter entirely and observe that the request is now accepted.
4. If you're using [Burp Suite Professional](https://portswigger.net/burp/pro), right-click on the request, and from the context menu select Engagement tools / Generate CSRF PoC. Enable the option to include an auto-submit script and click "Regenerate".`<form method="POST" action="https://YOUR-LAB-ID.web-security-academy.net/my-account/change-email"> <input type="hidden" name="$param1name" value="$param1value"> </form> <script> document.forms[0].submit(); </script>`
    
    Alternatively, if you're using [Burp Suite Community Edition](https://portswigger.net/burp/communitydownload), use the following HTML template. You can get the request URL by right-clicking and selecting "Copy URL".
    
5. Go to the exploit server, paste your exploit HTML into the "Body" section, and click "Store".
6. To verify if the exploit will work, try it on yourself by clicking "View exploit" and checking the resulting HTTP request and response.
7. Change the email address in your exploit so that it doesn't match your own.
8. Store the exploit, then click "Deliver to victim" to solve the lab.
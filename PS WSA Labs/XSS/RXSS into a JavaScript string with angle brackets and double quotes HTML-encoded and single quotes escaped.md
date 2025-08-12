---
{"dg-publish":true,"permalink":"/src/site/notes/src/site/notes/src/site/notes/src/site/notes/main/cs/ps-wsa-labs/xss/rxss-into-a-java-script-string-with-angle-brackets-and-double-quotes-html-encoded-and-single-quotes-escaped/"}
---






- Vulnerability in the search query tracking functionality where angle brackets and double are HTML encoded and single quotes are escaped.

1. Submit a random alphanumeric string in the search box, then use Burp Suite to intercept the search request and send it to Burp Repeater.
2. Observe that the random string has been reflected inside a JavaScript string.
3. Try sending the payload `test'payload` and observe that your single quote gets backslash-escaped, preventing you from breaking out of the string.
4. Try sending the payload `test\payload` and observe that your backslash doesn't get escaped.
5. Replace your input with the following payload to break out of the JavaScript string and inject an alert:`\'-alert(1)//`
6. Verify the technique worked by right clicking, selecting "Copy URL", and pasting the URL in the browser. When you load the page it should trigger an alert.
---
{"dg-publish":true,"permalink":"/src/site/notes/src/site/notes/src/site/notes/src/site/notes/main/cs/ps-wsa-labs/xss/rxss-into-a-java-script-string-with-single-quote-and-backslash-escaped/"}
---






- Perform a cross-site scripting attack that breaks out of the JavaScript string and calls the `alert` function.

1. Submit a random alphanumeric string in the search box, then use Burp Suite to intercept the search request and send it to Burp Repeater.  
2. Observe that the random string has been reflected inside a JavaScript string.  
3. Try sending the payload   
`test'payload` and observe that your single quote gets backslash-escaped, preventing you from breaking out of the string.  
4. Replace your input with the following payload to break out of the script block and inject a new script:  
`</script><script>alert(1)</script>`  
5. Verify the technique worked by right clicking, selecting "Copy URL", and pasting the URL in the browser. When you load the page it should trigger an alert.
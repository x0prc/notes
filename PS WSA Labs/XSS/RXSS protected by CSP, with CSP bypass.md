---
{"dg-publish":true,"permalink":"/src/site/notes/src/site/notes/src/site/notes/src/site/notes/main/cs/ps-wsa-labs/xss/rxss-protected-by-csp-with-csp-bypass/"}
---






To solve the lab, perform a [cross-site scripting](https://portswigger.net/web-security/cross-site-scripting) attack that bypasses the CSP and calls the `alert` function.

1. Enter the following into the search box:`<img src=1 onerror=alert(1)>`
2. Observe that the payload is reflected, but the CSP prevents the script from executing.
3. In Burp Proxy, observe that the response contains a `Content-Security-Policy` header, and the `report-uri` directive contains a parameter called `token`. Because you can control the `token` parameter, you can inject your own CSP directives into the policy.
4. Visit the following URL, replacing `YOUR-LAB-ID` with your lab ID:`https://YOUR-LAB-ID.web-security-academy.net/?search=%3Cscript%3Ealert%281%29%3C%2Fscript%3E&token=;script-src-elem%20%27unsafe-inline%27`

The injection uses the `script-src-elem` directive in CSP. This directive allows you to target just `script` elements. Using this directive, you can overwrite existing `script-src` rules enabling you to inject `unsafe-inline`, which allows you to use inline scripts.
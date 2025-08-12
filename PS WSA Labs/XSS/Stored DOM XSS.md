---
{"dg-publish":true,"permalink":"/src/site/notes/src/site/notes/src/site/notes/src/site/notes/main/cs/ps-wsa-labs/xss/stored-dom-xss/"}
---






Post a comment containing the following vector:

```Plain
<><img src=1 onerror=alert(1)>
```

In an attempt to prevent [XSS](https://portswigger.net/web-security/cross-site-scripting), the website uses the JavaScript `replace()` function to encode angle brackets. However, when the first argument is a string, the function only replaces the first occurrence. We exploit this vulnerability by simply including an extra set of angle brackets at the beginning of the comment. These angle brackets will be encoded, but any subsequent angle brackets will be unaffected, enabling us to effectively bypass the filter and inject HTML.
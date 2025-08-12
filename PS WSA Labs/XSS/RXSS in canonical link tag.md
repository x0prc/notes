---
{"dg-publish":true,"permalink":"/src/site/notes/src/site/notes/src/site/notes/src/site/notes/main/cs/ps-wsa-labs/xss/rxss-in-canonical-link-tag/"}
---






- This lab reflects user input in a canonical link tag and escapes angle brackets.

1. Visit the following URL, replacing `YOUR-LAB-ID` with your lab ID:`https://YOUR-LAB-ID.web-security-academy.net/?%27accesskey=%27x%27onclick=%27alert(1)`
    
    This sets the `X` key as an access key for the whole page. When a user presses the access key, the `alert` function is called.
    
2. To trigger the exploit on yourself, press one of the following key combinations:
    
    - On Windows: `ALT+SHIFT+X`
    - On MacOS: `CTRL+ALT+X`
    - On Linux: `Alt+X`
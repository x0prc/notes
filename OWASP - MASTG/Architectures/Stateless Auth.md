---
{"dg-publish":true,"permalink":"/src/site/notes/src/site/notes/src/site/notes/src/site/notes/main/cs/owasp-mastg/architectures/stateless-auth/"}
---






- Token-based authentication is implemented by sending a signed token (verified by the server) with each HTTP request.
- JWT tokens consist of three Base64Url-encoded parts separated by dots. The Token structure is as follows:  
      
    

```Java
base64UrlEncode(header).base64UrlEncode(payload).base64UrlEncode(signature)
```

- The signature is created by applying the algorithm specified in the JWT header to the encoded header, encoded payload and a secret value.
    - For example, when using the HMAC SHA256 algorithm the signature is created in the following way:  
          
        

```Java
HMACSHA256(base64UrlEncode(header) + "." + base64UrlEncode(payload), secret)
```
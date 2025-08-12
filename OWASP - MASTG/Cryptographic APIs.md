---
{"dg-publish":true,"permalink":"/src/site/notes/src/site/notes/src/site/notes/src/site/notes/main/cs/owasp-mastg/cryptographic-ap-is/"}
---






- For the analysis process you should focus on functions which are used by the  
    application developer. You should identify and verify the following functions:  
    - Key generation
    - Random number generation
    - Key rotation

# ==Security Provider==

- Android relies on the java.security.Provider class to implement Java Security services. These providers are crucial to ensure secure network communications and secure other functionalities which depend on cryptography.
- You can list the set of existing security providers using following code:

```Java
StringBuilder builder = new StringBuilder();
for (Provider provider : Security.getProviders()) {
		builder.append("provider: ")
					 .append(provider.getName())
					 .append(" ")
				   .append(provider.getVersion())
					 .append("(")
					 .append(provider.getInfo())
					 .append(")\n");
}
String providers = builder.toString();
//now display the string on the screen or in the logs for debugging.
```

# ==Key Generation==

- The KeyGenParameterSpec indicates that the key can be used for encryption and decryption, but not for other purposes, such as signing or verifying.

```Java
String keyAlias = "MySecretKey";

KeyGenParameterSpec keyGenParameterSpec = new KeyGenParameterSpec.Builder(keyAlias,
				KeyProperties.PURPOSE_ENCRYPT | KeyProperties.PURPOSE_DECRYPT)
				.setBlockModes(KeyProperties.BLOCK_MODE_CBC)
				.setEncryptionPaddings(KeyProperties.ENCRYPTION_PADDING_PKCS7)
				.setRandomizedEncryptionRequired(true)
				.build();
KeyGenerator keyGenerator = KeyGenerator.getInstance(KeyProperties.KEY_ALGORITHM_AES,
"AndroidKeyStore");
keyGenerator.init(keyGenParameterSpec);
SecretKey secretKey = keyGenerator.generateKey();
```

# ==Symmetric Cryptography==

## ==Static Analysis==

- First disassemble and decompile the app to obtain Java code, e.g. by using jadx.
    
    - Now search the files for the usage of the SecretKeySpec class, e.g. by simply recursively grepping on them or using jadx search function:
    
    ```Shell
    grep -r "SecretKeySpec"
    ```
    

## ==Dynamic Analysis==

- You can use method tracing on cryptographic methods to determine input / output values such as the keys that are being used.
    - Monitor file system access while cryptographic operations are being performed to assess where key material is written to or read from.
    - For example, monitor the file system by using the API monitor of RMS - Runtime Mobile Security.
---
dg-publish: true
---







![Untitled 7.png|Untitled 7.png](/img/user/img/Untitled%207.png)

# ==Checking FingerprintManager==

```Java
<uses-permission
		android:name="android.permission.USE_FINGERPRINT" />
		
FingerprintManager fingerprintManager = (FingerprintManager)
								context.getSystemService(Context.FINGERPRINT_SERVICE);
fingerprintManager.isHardwareDetected();

KeyguardManager keyguardManager = (KeyguardManager) context.getSystemService(Context.KEYGUARD_SERVICE);
keyguardManager.isKeyguardSecure(); //note if this is not the case: ask the user to setup a protected lock screen
	
```

- If any of the above checks fail, the option for fingerprint authentication should not be offered.  
      
    
- Fingerprint authentication may be implemented by creating a new AES key using the KeyGenerator class by adding setUserAuthenticationRequired(true) in KeyGenParameterSpec.Builder.

```Java
generator = KeyGenerator.getInstance(KeyProperties.KEY_ALGORITHM_AES, KEYSTORE);

generator.init(new KeyGenParameterSpec.Builder (KEY_ALIAS,
				 KeyProperties.PURPOSE_ENCRYPT | KeyProperties.PURPOSE_DECRYPT)
				 .setBlockModes(KeyProperties.BLOCK_MODE_CBC)
				 .setEncryptionPaddings(KeyProperties.ENCRYPTION_PADDING_PKCS7)
				 .setUserAuthenticationRequired(true)
				 .build()
);
generator.generateKey();
```

# ==Implementing Biometric Auth==

```Java
KeyguardManager mKeyguardManager = (KeyguardManager) getSystemService(Context.KEYGUARD_SERVICE);

if (!mKeyguardManager.isKeyguardSecure()) {
// Show a message that the user hasn't set up a lock screen.
}

try {
		KeyStore keyStore = KeyStore.getInstance("AndroidKeyStore");
		keyStore.load(null);
		KeyGenerator keyGenerator = KeyGenerator.getInstance(
							KeyProperties.KEY_ALGORITHM_AES, "AndroidKeyStore");

// Set the alias of the entry in Android KeyStore where the key will appear
// and the constrains (purposes) in the constructor of the Builder

		keyGenerator.init(new KeyGenParameterSpec.Builder(KEY_NAME,
							KeyProperties.PURPOSE_ENCRYPT | KeyProperties.PURPOSE_DECRYPT)
							.setBlockModes(KeyProperties.BLOCK_MODE_CBC)
							.setUserAuthenticationRequired(true)

// Require that the user has unlocked in the last 30 seconds
						  .setUserAuthenticationValidityDurationSeconds(30)
							.setEncryptionPaddings(KeyProperties.ENCRYPTION_PADDING_PKCS7)
							.build());
keyGenerator.generateKey();
} catch (NoSuchAlgorithmException | NoSuchProviderException
				| InvalidAlgorithmParameterException | KeyStoreException
				| CertificateException | IOException e) {
		 throw new RuntimeException("Failed to create a symmetric key", e);
}

private static final int REQUEST_CODE_CONFIRM_DEVICE_CREDENTIALS = 1; //used as a number to verify whether this is where the activity results from

Intent intent = mKeyguardManager.createConfirmDeviceCredentialIntent(null, null);
if (intent != null) {
	 startActivityForResult(intent, REQUEST_CODE_CONFIRM_DEVICE_CREDENTIALS);
}

@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
		if (requestCode == REQUEST_CODE_CONFIRM_DEVICE_CREDENTIALS) {
// Challenge completed, proceed with using cipher
			if (resultCode == RESULT_OK) {
//use the key for the actual authentication flow
			} else {
// The user canceled or didn’t complete the lock screen
// operation. Go to error/cancellation flow.
			}
		}
	}
```
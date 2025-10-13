---
dg-publish: true
---






# ==Data Sharing via Notifications==

- Search for any usage of the ==**NotificationManager**== class which might be an indication of some form of notification management.
    - If the class is being used, the next step would be to understand how the application is generating the notifications and which data ends up being shown.
- Run the application and start tracing all calls to functions related to the notifications creation, e.g. **==setContentTitle==** or **==setContentText==** from **==NotificationCompat.Builder==**

# ==Testing Backups==

- Check the AndroidManifest.xml file for the following flag:

```Java
android:allowBackup="true"
```

- Cloud:

```Java
android:fullBackupOnly
android:backupAgent
```

## ==Dynamic Analysis==

```Java
adb backup -apk -nosystem <package-name>

adb backup "-apk -nosystem <package-name>"
```

# ==Testing Local Storage==

- Obtaining the key is trivial because it is contained in the source code and identical for all installations of the app. Encrypting data this way is not beneficial.
    - Look for hard-coded API keys/private keys and other valuable data; they pose a similar risk. Encoded/encrypted keys represent another attempt to make it harder but not impossible to get the crown jewels.

```Java
//A more complicated effort to store the XOR'ed halves of a key (instead of the key itself)
private static final String[] myCompositeKey = new String[]{
"oNQavjbaNNSgEqoCkT9Em4imeQQ=","3o8eFOX4ri/F8fgHgiy/BS47"
};
```

- Algorithm for decoding the original key :

```Java
public void useXorStringHiding(String myHiddenMessage) {
	byte[] xorParts0 = Base64.decode(myCompositeKey[0],0);
	byte[] xorParts1 = Base64.decode(myCompositeKey[1],0);
	
	byte[] xorKey = new byte[xorParts0.length];
	for(int i = 0; i < xorParts1.length; i++){
		xorKey[i] = (byte) (xorParts0[i] ^ xorParts1[i]);
	}
	HidingUtil.doHiding(myHiddenMessage.getBytes(), xorKey, false);
}
```

```Java
public class SecureSecretKey implements javax.crypto.SecretKey, Destroyable {
		private byte[] key;
		private final String algorithm;
/** Constructs SecureSecretKey instance out of a copy of the provided key bytes.
* The caller is responsible of clearing the key array provided as input.
* The internal copy of the key can be cleared by calling the destroy() method.
*/
		public SecureSecretKey(final byte[] key, final String algorithm) {
				this.key = key.clone();
				this.algorithm = algorithm;
}
public String getAlgorithm() {
return this.algorithm;
}
public String getFormat() {
return "RAW";
}
/** Returns a copy of the key.
* Make sure to clear the returned byte array when no longer needed.
*/
public byte[] getEncoded() {
if(null == key){
throw new NullPointerException();
}
return key.clone();
}
/** Overwrites the key with dummy data to ensure this copy is no longer present in memory.*/
public void destroy() {
if (isDestroyed()) {
return;
}
byte[] nonSecret = new String("RuntimeException").getBytes("ISO-8859-1");
for (int i = 0; i < key.length; i++) {
key[i] = nonSecret[i % nonSecret.length];
}
FileOutputStream out = new FileOutputStream("/dev/null");
out.write(key);
out.flush();
out.close();
this.key = null;
System.gc();
}
public boolean isDestroyed() {
return key == null;
}
}
```
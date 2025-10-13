---
dg-publish: true
---






# ==Shared Preferences==

- The SharedPreferences API is commonly used to permanently save small collections of key-value pairs. Data stored in a SharedPreferences object is written to a plain-text XML file.

```Java
SharedPreferences sharedPref = getSharedPreferences("key", MODE_WORLD_READABLE);
SharedPreferences.Editor editor = sharedPref.edit();
editor.putString("username", "administrator");
editor.putString("password", "supersecret");
editor.commit();
```

# ==Databases==

## ==SQLite==

- The main package used to manage the databases is android.database.sqlite.

```Java
SQLiteDatabase notSoSecure = openOrCreateDatabase("privateNotSoSecure", MODE_PRIVATE, null);
notSoSecure.execSQL("CREATE TABLE IF NOT EXISTS Accounts(Username VARCHAR, Password VARCHAR);");
notSoSecure.execSQL("INSERT INTO Accounts VALUES('admin','AdminPass');");
notSoSecure.close();
```

- Firebase, Realm are some other databases common among developers today.

# ==Internal Storage==

- The following code snippets would persistently store sensitive data to internal storage.

```Java
FileOutputStream fos = null;
try {
	fos = openFileOutput(FILENAME, Context.MODE_PRIVATE);
	fos.write(test.getBytes());
	fos.close();
} catch (FileNotFoundException e) {
		e.printStackTrace();
} catch (IOException e) {
		e.printStackTrace();
}
```

# ==External Storage==

```Java
File file = new File (Environment.getExternalFilesDir(), "password.txt");
String password = "SecretPassword";
FileOutputStream fos;
		fos = new FileOutputStream(file);
		fos.write(password.getBytes());
		fos.close();
```

# ==KeyStore API==

- The Android KeyStore supports relatively secure credential storage. As of Android 4.3 (API level 18), it provides public APIs for storing and using app-private keys.
    - An app can use a public key to create a new private/public key pair for encrypting application secrets, and it can decrypt the secrets with the private key.
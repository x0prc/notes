---
{"dg-publish":true,"permalink":"/src/site/notes/src/site/notes/src/site/notes/src/site/notes/main/cs/owasp-mastg/platform-ap-is/"}
---






# ==App Permissions==

- **Install-time permissions:** grant limited access to restricted data or let the app perform restricted actions that minimally affect the system or other apps. They are granted automatically at installation time (Android 6.0 (AP Ievel 23) or higher).
    - Protection Level: normal. Grants apps access to isolated application-level features with minimal risk to other apps, the user, and the system. Example: android.permission.INTERNET
    - Protection Level: signature. Granted only to apps signed with the same certificate as the one used to sign the declaring app. Example: android.permission.ACCESS_MOCK_LOCATION
    - Protection Level: systemOrSignature. Reserved for system-embedded apps or those signed with the same certificate as the one used to sign the declaring app. Example: android.permission.ACCESS_DOWNLOAD_-MANAGER. Old synonym for signature|privileged. Deprecated in API level 23.
- **Runtime permissions:** require prompting the user at runtime for explicit approval.
    - Protection Level: dangerous. Grant additional access to restricted data or let the app perform restricted actions that more substantially affect the system and other apps.
- **Special permissions:** require the user to navigate to Settings > Apps > Special app access and give explicit consent.
    - Protection Level: appop. Grant access to system resources that are particularly sensitive such as displaying and drawing over other apps or accessing all storage data.
- **Custom permissions** in order to share their own resources and capabilities with other apps.
    - Protection Level: normal, signature or dangerous.

# ==Testing for Permissions==

## ==Static Analysis==

```Shell
<uses-permission android:name="android.permission.INTERNET" />

$ aapt d permissions app-x86-debug.apk
package: sg.vp.owasp_mobile.omtg_android
uses-permission: name='android.permission.WRITE_EXTERNAL_STORAGE'
uses-permission: name='android.permission.INTERNET'

$ adb shell dumpsys package sg.vp.owasp_mobile.omtg_android | grep permission
requested permissions:
android.permission.WRITE_EXTERNAL_STORAGE
android.permission.INTERNET
android.permission.READ_EXTERNAL_STORAGE
install permissions:
android.permission.INTERNET: granted=true
runtime permissions:
```

## ==Custom Permissions==

```Java
private static final String TAG = "LOG";
int canProcess = checkCallingOrSelfPermission("com.example.perm.READ_INCOMING_MSG");
if (canProcess != PERMISSION_GRANTED)
throw new SecurityException();

if (ContextCompat.checkSelfPermission(secureActivity.this, Manifest.READ_INCOMING_MSG)
					!= PackageManager.PERMISSION_GRANTED) {
						 //!= stands for not equals PERMISSION_GRANTED
					Log.v(TAG, "Permission denied");
					}
```

## ==Requesting Permissions==

```Java
private static final String TAG = "LOG";
// We start by checking the permission of the current Activity
if (ContextCompat.checkSelfPermission(secureActivity.this,
				Manifest.permission.WRITE_EXTERNAL_STORAGE)
				!= PackageManager.PERMISSION_GRANTED) {
// Permission is not granted
// Should we show an explanation?

		if (ActivityCompat.shouldShowRequestPermissionRationale(secureActivity.this,
//Gets whether you should show UI with rationale for requesting permission.
//You should do this only if you do not have permission and the permission requested rationale is not communicated clearly to the user.
				Manifest.permission.WRITE_EXTERNAL_STORAGE)) {
// Asynchronous thread waits for the users response.
// After the user sees the explanation try requesting the permission again.
		} else {
// Request a permission that doesn't need to be explained.
			ActivityCompat.requestPermissions(secureActivity.this,
							new String[]{Manifest.permission.WRITE_EXTERNAL_STORAGE},
							MY_PERMISSIONS_REQUEST_WRITE_EXTERNAL_STORAGE);
// MY_PERMISSIONS_REQUEST_WRITE_EXTERNAL_STORAGE will be the app-defined int constant.
// The callback method gets the result of the request.
		}
} else {
// Permission already granted debug message printed in terminal.
		Log.v(TAG, "Permission already granted.");
}
```
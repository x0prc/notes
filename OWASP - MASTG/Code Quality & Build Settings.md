---
dg-publish: true
---






# ==Debugging Code and Error Logging==

## ==StrictMode==

- StrictMode is a developer tool for detecting violations, e.g. accidental disk or network access on the application’s main thread. It can also be used to check for good coding practices, such as implementing performant code.
    
    - Here is an example of StrictMode with policies enabled for disk and network access to the main thread:
    
    ```Java
    public void onCreate() {
    			if (DEVELOPER_MODE) {
    					StrictMode.setThreadPolicy(new StrictMode.ThreadPolicy.Builder()
    										.detectDiskReads()
    										.detectDiskWrites()
    										.detectNetwork() // or .detectAll() for all detectable problems
    										.penaltyLog()
    										.build());
    					
    					StrictMode.setVmPolicy(new StrictMode.VmPolicy.Builder()
    										.detectLeakedSqlLiteObjects()
    										.detectLeakedClosableObjects()
    										.penaltyLog()
    										.penaltyDeath()
    										.build());
    			}
    			super.onCreate();
    }
    ```
    
    ## ==Exception Handling==
    
    - Exceptions occur when an application gets into an abnormal or error state. Both Java and C++ may throw exceptions.
        - Testing exception handling is about ensuring that the app will handle an exception and transition to a safe state without exposing sensitive information via the UI or the app’s logging mechanisms.

  

# ==Testing for Injection Flaws==

## ==Static Analysis==

- You can use ContentProviders to access database information, and you can probe services to see if they return data.
    - If data is not validated properly, the content provider may be prone to SQL injection while other apps are interacting with it. See the following vulnerable implementation of a ContentProvider.

```XML
<provider
		android:name=".OMTG_CODING_003_SQL_Injection_Content_Provider_Implementation"
		android:authorities="sg.vp.owasp_mobile.provider.College">
</provider>
```

```Java
@Override
public Cursor query(Uri uri, String[] projection, String selection,String[] selectionArgs, String sortOrder) {
		SQLiteQueryBuilder qb = new SQLiteQueryBuilder();
		qb.setTables(STUDENTS_TABLE_NAME);

		switch (uriMatcher.match(uri)) {
				case STUDENTS:
						qb.setProjectionMap(STUDENTS_PROJECTION_MAP);
						break;
				
				case STUDENT_ID:
// SQL Injection when providing an ID
						 qb.appendWhere( _ID + "=" + uri.getPathSegments().get(1));
						 Log.e("appendWhere",uri.getPathSegments().get(1).toString());
						 break;
						 default:
									throw new IllegalArgumentException("Unknown URI " + uri);
}
	
		if (sortOrder == null || sortOrder == ""){
/**
* By default sort on student names
*/
				sortOrder = NAME;
}

		Cursor c = qb.query(db, projection, selection, selectionArgs,null, null, sortOrder);
/**
* register to watch a content URI for changes
*/
		c.setNotificationUri(getContext().getContentResolver(), uri);
		return c;
}
```

# ==Enforced Updating==

- To test for enforced updating you need to check if the app has support for in-app updates and validate if it’s properly enforced so that the user is not able to continue using the app without updating it first.
    - The code sample below shows the example of an app-update:

```Java
//Part 1: check for update
// Creates instance of the manager.
AppUpdateManager appUpdateManager = AppUpdateManagerFactory.create(context);
// Returns an intent object that you use to check for an update.
Task<AppUpdateInfo> appUpdateInfo = appUpdateManager.getAppUpdateInfo();
// Checks that the platform will allow the specified type of update.
if (appUpdateInfo.updateAvailability() == UpdateAvailability.UPDATE_AVAILABLE

// For a flexible update, use AppUpdateType.FLEXIBLE
&& appUpdateInfo.isUpdateTypeAllowed(AppUpdateType.IMMEDIATE)) {
//...Part 2: request update
appUpdateManager.startUpdateFlowForResult(
// Pass the intent that is returned by 'getAppUpdateInfo()'.
appUpdateInfo,
// Or 'AppUpdateType.FLEXIBLE' for flexible updates.
AppUpdateType.IMMEDIATE,
// The current activity making the update request.
this,
// Include a request code to later monitor this update request.
MY_REQUEST_CODE);
//...Part 3: check if update completed successfully
@Override
public void onActivityResult(int requestCode, int resultCode, Intent data) {
if (myRequestCode == MY_REQUEST_CODE) {
if (resultCode != RESULT_OK) {
log("Update flow failed! Result code: " + resultCode);
// If the update is cancelled or fails,
// you can request to start the update again in case of forced updates
}
}
}
//..Part 4:
// Checks that the update is not stalled during 'onResume()'.
// However, you should execute this check at all entry points into the app.
@Override
protected void onResume() {
super.onResume();
appUpdateManager
.getAppUpdateInfo()
.addOnSuccessListener(
appUpdateInfo -> {
...
if (appUpdateInfo.updateAvailability()
== UpdateAvailability.DEVELOPER_TRIGGERED_UPDATE_IN_PROGRESS) {
// If an in-app update is already running, resume the update.
manager.startUpdateFlowForResult(
appUpdateInfo,
IMMEDIATE,
this,
MY_REQUEST_CODE);
}
});
}
}
```

# ==Other Techniques for Testing==

- Memory Corruption Bugs
- Object Persistence
- Implicit Intents
- Weakness in Third Party Libraries
- URL Loading in WebViews
- Page Navigation Handlling Override
- EnableSafeBrowsing Disabled
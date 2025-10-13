---
dg-publish: true
---






# ==SafetyNet==

- SafetyNet is an Android API that provides a set of services and creates profiles of devices according to software and hardware information.
    - This profile is then compared to a list of accepted device models that have passed Android compatibility testing. Google recommends using the feature as “an additional in-depth defense signal as part of an anti-abuse system”.

```JSON
{
"nonce": "R2Rra24fVm5xa2Mg",
"timestampMs": 9860437986543,
"apkPackageName": "com.package.name.of.requesting.app",
"apkCertificateDigestSha256": ["base64 encoded, SHA-256 hash of the
																certificate used to sign requesting app"],

"apkDigestSha256": "base64 encoded, SHA-256 hash of the app's APK",
"ctsProfileMatch": true,
"basicIntegrity": true,
}
```

# ==File Existence Checks==

```Java
public static boolean checkRoot(){
		for(String pathDir : System.getenv("PATH").split(":")){
				if(new File(pathDir, "su").exists()) {
						return true;
				}
		}
		return false;
}
```

# ==Checking running processes==

```Java
public boolean checkRunningProcesses() {
		
		boolean returnValue = false;
// Get currently running application processes
		
		List<RunningServiceInfo> list = manager.getRunningServices(300);
	
		if(list != null){
			String tempName;
			for(int i=0;i<list.size();++i){
					tempName = list.get(i).process;

					if(tempName.contains("supersu") || tempName.contains("superuser")){
						returnValue = true;
					}
			}
	}
	return returnValue;
}
```

# ==Other Techniques==

- Custom Android builds
- Anti-Debugging
- Debuggable Flag in ApplicationInfo
- TracerPid
- File Integrity Checks
- RevEng Detection
- Emulator Detection
- Runtime Integrity Verification
- Root Detection
- Debugging Symbols
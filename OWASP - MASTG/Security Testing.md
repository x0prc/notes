---
{"dg-publish":true,"permalink":"/src/site/notes/src/site/notes/src/site/notes/src/site/notes/main/cs/owasp-mastg/security-testing/"}
---






# ==Exploring App Package==

```Shell
 $apktool d UnCrackable-Level3.apk
 $tree
```

# ==Symbolic Execution==

- Dealing with problems where you need to **find a correct input for reaching a certain block of code.** In this section, we will solve a simple Android crackme by using the Angr binary analysis framework as our symbolic execution engine.
- To demonstrate this technique we’ll use a crackme called Android License Validator. The crackme consists of a single ELF executable file, which can be executed on any Android device by following the instructions below:

```Shell
$ adb push validate /data/local/tmp
$ adb shell chmod 755 /data/local/tmp/validate
$ adb shell /data/local/tmp/validate
$ adb shell /data/local/tmp/validate 12345
```

- Further dump the outputs in Disassembler to further understand this.
- The complete script to test encryption via Base64 is as follows :

```Shell
import angr # Version: 9.2.2
import base64
load_options = {}
b = angr.Project("./validate", load_options = load_options)
## The key validation function starts at 0x401760, so that's where we create the initial state.
## This speeds things up a lot because we're bypassing the Base32-encoder.
options = {
angr.options.SYMBOL_FILL_UNCONSTRAINED_MEMORY,
angr.options.ZERO_FILL_UNCONSTRAINED_REGISTERS,
}
state = b.factory.blank_state(addr=0x401760, add_options=options)
simgr = b.factory.simulation_manager(state)
simgr.explore(find=0x401840, avoid=0x401854)
## 0x401840 = Product activation passed
## 0x401854 = Incorrect serial
found = simgr.found[0]
## Get the solution string from *(R11 - 0x20).
addr = found.memory.load(found.regs.r11 - 0x20, 1, endness="Iend_LE")
concrete_addr = found.solver.eval(addr)
solution = found.solver.eval(found.memory.load(concrete_addr,10), cast_to=bytes)
print(base64.b32encode(solution))
```

# ==Patching==

- Modifying the script for Disabling Certificate Pinning works as follows:

```Java
method public checkServerTrusted([LJava/security/cert/X509Certificate;Ljava/lang/String;)V
	.locals 3
	.param p1, "chain" # [Ljava/security/cert/X509Certificate;
	.param p2, "authType" # Ljava/lang/String;
	
	.prologue
return-void # <-- OUR INSERTED OPCODE!
	.line 102
iget-object v1, p0, Lasdf/t$a;->a:Ljava/util/ArrayList;

invoke-virtual {v1}, Ljava/util/ArrayList;->iterator()Ljava/util/Iterator;

move-result-object v1

	:goto_0
	invoke-interface {v1}, Ljava/util/Iterator;->hasNext()Z
```

- Changing App from Release buid to Debug Build :

```Java
<application android:allowBackup="true" android:debuggable="true" android:icon="@drawable/ic_launcher" android:label="@string/app_name"
↪ android:name="com.xxx.xxx.xxx" android:theme="@style/AppTheme">
```

- React Native Applications :
    - If the React Native framework has been used for developing then the main application code is located in the file assets/index.android.bundle. This file contains the JavaScript code. **Most of the time, the JavaScript code in this file is minified.**
    - By using the tool JStillery a human readable version of the file can be retrieved, allowing code analysis. **The CLI version of JStillery or the local server should be preferred** instead of using the online version as otherwise source code is sent and disclosed to a 3rd party.

# ==Accessing Data Directories==

- Works using the tool callled objection.

```Java
objection -g sg.vp.owasp_mobile.omtg_android explore
```

# ==Dynamic Analysis on Non Rooted==

```PowerShell
## Download the Uncrackable APK
$ wget https://raw.githubusercontent.com/OWASP/owasp-mastg/master/Crackmes/Android/Level_01/UnCrackable-Level1.apk
## Patch the APK with the Frida Gadget
$ objection patchapk --source UnCrackable-Level1.apk
## Install the patched APK on the android phone
$ adb install UnCrackable-Level1.objection.apk
## After running the mobile phone, objection will detect the running frida-server through the APK
$ objection explore
```

# ==Bypassing Certificate Pinning==

- Some applications will implement SSL Pinning, which prevents the application from accepting your intercepting certificate as a valid certificate.
- This means that you will not be able to monitor the traffic between the application and the server.

## ==Methods==

- Cydia Substrate: Install the Android-SSL-TrustKiller package.
- Frida: Use the frida-multiple-unpinning script.
- Objection: Use the android sslpinning disable command.
- Xposed: Install the TrustMeAlready or SSLUnpinning module

# ==Interception Proxy==

- Several tools support the network analysis of applications that rely on the HTTP(S) protocol. The most important tools are the so-called interception proxies; OWASP ZAP and Burp Suite Professional are the most famous.
- An interception proxy gives the tester a man-in-the-middle position. This position is useful for reading and/or modifying all app requests and endpoint responses, which are used for testing Authorization, Session, Management, etc.
- Adding CA certificates on Virtual Device is mandatory before hand.

# ==Bypassing Network Security Config==

## ==Adding the Proxy’s certificate among system trusted CAs using Magisk==

- In order to avoid the obligation of configuring the Network Security Configuration for each application, we must force the device to accept the proxy’s certificate as one of the systems trusted certificates.
- There is a Magisk module that will automatically add all user-installed CA certificates to the list of system trusted CAs.

# ==Proxy Detection==

- Frida script helps to overload the method which verifies the proxy and always return false.

```Java
setTimeout(function(){
		Java.perform(function (){
				console.log("[*] Script loaded")
				
				var Proxy = Java.use("<package-name>.<class-name>")
				
				Proxy.isProxySet.overload().implementation = function() {
							console.log("[*] isProxySet function invoked")
							return false
							}
					});
			 });
```

# ==Other Testing Techniques==

## ==Debugging==

- Release Apps
- With jdb
- With an IDE
- Native Code

## ==JNI Tracing==

- As detailed in section Reviewing Disassembled Native Code, the first argument passed to every JNI function is a JNI interface pointer. **This pointer contains a table of functions that allows native code to access the Android Runtime.**
- Identifying calls to these functions can help with understanding library functionality, such as what strings are created or Java methods are called.
- jnitrace is a Frida based tool similar to frida-trace which specifically targets the usage of Android’s JNI API by native libraries, providing a convenient way to obtain JNI method traces including arguments and return values.

## ==System Logs==

- Logcat

## ==Host-Device Data Transfer==

- Using adb
- Studio Device File Explorer
- Using Objection

## ==Decompiling Java==

- Android decompilers go one step further and attempt to convert **Android bytecode back into Java source code, making it more human-readable.**
- Fortunately, Java decompilers generally handle Android bytecode well. The above mentioned tools embed, and sometimes even combine, popular free decompilers such as:  
    • JD  
    • JAD  
    • jadx  
    • Procyon  
    • CFR  
    
- Alternatively you can use the APKLab extension for Visual Studio Code or run apkx on your APK or use the exported files from the previous tools to open the reversed source code on your preferred IDE.

# ==Process Exploration==

- When testing an app, **process exploration can provide the tester with deep insights into the app process memory.** It can be achieved via runtime instrumentation and allows to perform tasks such as:
    - Retrieving the memory map and loaded libraries.
    - Searching for occurrences of certain data.
    - After doing a search, obtaining the location of a certain offset in the memory map.
    - Performing a memory dump and inspect or reverse engineer the binary data offline.
    - Reverse engineering a native library while it’s running.

# ==Repackaging and Re-Signing==

```Java
cd UnCrackable-Level1
apktool b
zipalign -v 4 dist/UnCrackable-Level1.apk ../UnCrackable-Repackaged.apk
```

- Re-Signing

```Java
keytool -genkey -v -keystore ~/.android/debug.keystore -alias signkey -keyalg RSA -keysize 2048 -validity 20000
```

```Java
apksigner sign --ks ~/.android/debug.keystore --ks-key-alias signkey UnCrackable-Repackaged.apk
```

```Java
jarsigner -verbose -keystore ~/.android/debug.keystore ../UnCrackable-Repackaged.apk signkey
zipalign -v 4 dist/UnCrackable-Level1.apk ../UnCrackable-Repackaged.apk
```

# ==Get Open Connections==

```Java
## cat /proc/7254/net/tcp
sl local_address rem_address st tx_queue rx_queue tr tm->when retrnsmt uid timeout inode
```

# ==Get Loaded Native Libraries==

## ==Process Memory Maps==

- The file /proc/<pid>/maps contains the currently mapped memory regions and their access permissions. Using this file we can get the list of the libraries loaded in the process.

```Shell
## cat /proc/9568/maps
```

## ==Using Frida==

- You can retrieve process related information straight from the Frida CLI by using the Process command.
    - Within the Process command the function enumerateModules lists the libraries loaded into the process memory.

# ==Accessing Device Shell==

- Remote Shell
- Multiple Devices Connection
    - over Wi-Fi
    - via SSH
    - On-device Shell App

## ==Firebase/Google Cloud Messaging (FCM/GCM)==

- Use either XMPP or HTML for communication with Google backend.

# ==Execution Tracing==

- To trace an app right from the start, you can pause the app with the Android “Wait for Debugger” feature or a kill -STOP command and attach jdb to set a deferred method breakpoint on any initialization method.
    - Once the breakpoint is reached, activate method tracing with the trace go methods command and resume execution. jdb will dump all method entries and exits  
        from that point onwards.  
        

```Shell
$adb forward tcp:7777 jdwp:7288
```

# ==Automated Static Analysis==

- There are several open source tools for automated security analysis of an APK :  
    • Androbugs  
    • JAADAS (archived)  
    • MobSF  
    • QARK
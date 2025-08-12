---
{"dg-publish":true,"permalink":"/src/site/notes/src/site/notes/src/site/notes/src/site/notes/main/cs/owasp-mastg/i-os-platform-overview/i-os-platform-overview/"}
---






# ==iOS Security Architecture==

![Untitled 8.png|Untitled 8.png](/img/user/img/Untitled%208.png)

![Untitled 1 2.png|Untitled 1 2.png](/img/user/img/Untitled%201%202.png)

![Untitled 2 2.png|Untitled 2 2.png](/img/user/img/Untitled%202%202.png)

# ==Apps==

- IPA files have a built-in directory structure. The example below shows this structure at a high level:
    - /Payload/ folder contains all the application data. We will come back to the contents of this folder in more detail.
    - /Payload/Application.app contains the application data itself (ARM-compiled code) and associated static resources.
    - /iTunesArtwork is a 512x512 pixel PNG image used as the application’s icon.
    - /iTunesMetadata.plist contains various bits of information, including the developer’s name and ID, the bundle identifier, copyright information, genre, the name of the app, release date, purchase date, etc.
    - /WatchKitSupport/WK is an example of an extension bundle. This specific bundle contains the extension delegate and the controllers for managing the interfaces and responding to user interactions on an Apple Watch.

# ==Security Testing==

## ==Obtaining the UDID==

- Different methods are listed as follows:

```Shell
$ ioreg -p IOUSB -l | grep "USB Serial"

$ brew install ideviceinstaller
$ idevice_id -l

$ system_profiler SPUSBDataType | sed -n -e '/iPad/,/Serial/p;/iPhone/,/Serial/p;/iPod/,/Serial/p' | grep "Serial Number:"

instruments -s devices
```

## ==Method Hooking==

```Python
import sys
import frida
## JavaScript to be injected
frida_code = """
// Obtain a reference to the initWithURL: method of the NSURLRequest class
var URL = ObjC.classes.NSURLRequest["- initWithURL:"];
// Intercept the method
Interceptor.attach(URL.implementation, {
onEnter: function(args) {
// Get a handle on NSString
var NSString = ObjC.classes.NSString;
// Obtain a reference to the NSLog function, and use it to print the URL value
// args[2] refers to the first method argument (NSURL *url)
var NSLog = new NativeFunction(Module.findExportByName('Foundation', 'NSLog'), 'void', ['pointer', '...']);
// We should always initialize an autorelease pool before interacting with Objective-C APIs
var pool = ObjC.classes.NSAutoreleasePool.alloc().init();
try {
// Creates a JS binding given a NativePointer.
var myNSURL = new ObjC.Object(args[2]);
// Create an immutable ObjC string object from a JS string object.
var str_url = NSString.stringWithString_(myNSURL.toString());
// Call the iOS NSLog function to print the URL to the iOS device logs
NSLog(str_url);
// Use Frida's console.log to print the URL to your terminal
console.log(str_url);
} finally {
pool.release();
}
}
});
"""

process = frida.get_usb_device().attach("Safari")
script = process.create_script(frida_code)
script.load()
sys.stdin.read()
```

# ==Other Techniques==

- Sandbox Insppection
- API Usage
- Emulation Based Analysis
- Repackaging Apps
- Library Injection
- Process Exploration
- Memory Dump
- Native Libraries
- Method Tracing
- Runtime Reverse Engineering
- Symbolic Execution
- Cydia Impactor for Jailbreaking
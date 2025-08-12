---
{"dg-publish":true,"permalink":"/src/site/notes/src/site/notes/src/site/notes/src/site/notes/main/cs/owasp-mastg/i-os-data-storage/"}
---






# ==NSData and NSMutableData==

- Used for data storage but are also useful for distributed objects applications.
- The following methods are used to write NSData Objects:
    - NSDataWritingWithoutOverwriting
    - NSDataWritingFileProtectionNone
    - NSDataWritingFileProtectionComplete
    - NSDataWritingFileProtectionCompleteUnlessOpen
    - NSDataWritingFileProtectionCompleteUntilFirstUserAuthentication
    - writeToFile: stores data as part of the NSData class
    - NSSearchPathForDirectoriesInDomains, NSTemporaryDirectory: used to manage file paths
    - NSFileManager

# ==Databases==

- CoreData
- SQLite
- Firebase Real-Time
- Realm
- Couchbase Lite
- Yap

# ==Keyboard Cache==

- Several options, such as autocorrect and spell check, are available to users to simplify keyboard input and are cached by default in .dat files in /private/var/mobile/Library/Keyboard/ and its subdirectories.
    - The UITextInputTraits protocol is used for keyboard caching.
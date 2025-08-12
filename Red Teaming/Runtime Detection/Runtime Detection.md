---
{"dg-publish":true,"permalink":"/src/site/notes/src/site/notes/src/site/notes/src/site/notes/main/cs/red-teaming/runtime-detection/runtime-detection/"}
---






## ==AMSI==

- **A**nti-**M**alware **S**can **I**nterface is a PowerShell security feature that will allow any applications or services to integrate directly into anti-malware products.
- AMSI will determine its actions from a response code as a result of monitoring and scanning. Below is a list of possible response codes:
    - AMSI_RESULT_CLEAN = 0
    - AMSI_RESULT_NOT_DETECTED = 1
    - AMSI_RESULT_BLOCKED_BY_ADMIN_START = 16384
    - AMSI_RESULT_BLOCKED_BY_ADMIN_END = 20479
    - AMSI_RESULT_DETECTED = 32768

## ==AMSI Instrumentation==

- The below diagram depicts how data is dissected as it flows through the layers and what DLLs/API calls are being instrumented.

![35e16d45ce27145fcdf231fdb8dcb35e.png](/img/user/img/35e16d45ce27145fcdf231fdb8dcb35e.png)

## ==PowerShell Downgrade==

- This attack can actively be seen exploited in tools such as [Unicorn](https://github.com/trustedsec/unicorn).
- Since this attack is such low-hanging fruit and simple in technique, there are a plethora of ways for the blue team to detect and mitigate this attack.

## ==PowerShell Reflection==

- Reflection allows a user or administrator to access and interact with .NET assemblies.
- PowerShell reflection can be abused to modify and identify information from valuable DLLs.
- The AMSI utilities for PowerShell are stored in the `AMSIUtils` .NET assembly located in `System.Management.Automation.AmsiUtils`.

## ==Automating for Fun==

### amsi.fail

- [amsi.fail](http://amsi.fail/) will compile and generate a PowerShell bypass from a collection of known bypasses.
- You can attach this bypass at the beginning of your malicious code as with previous bypasses or run it in the same session before executing malicious code.

### AMSITrigger

- [AMSITrigger](https://github.com/RythmStick/AMSITrigger) allows attackers to automatically identify strings that are flagging signatures to modify and break them. This method of bypassing AMSI is more consistent than others because you are making the file itself clean.
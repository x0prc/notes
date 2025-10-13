---
dg-publish: true
---






- Task Manager
    - Process Hacker
    - Process Explorer
- Windows Session Manager
    - smss.exe

## ==**csrss.exe**==

- The user-mode side of the Windows subsystem. This process is always running and is critical to system operation.

## ==wininit.exe==

- The **Windows Initialization Process**, **wininit.exe**, is responsible for launching services.exe (Service Control Manager), lsass.exe (Local Security Authority), and lsaiso.exe within Session 0. It is another critical Windows process that runs in the background, along with its child processes.

### **services.exe**

- **Service Control Manager** (SCM). Its primary responsibility is to handle system services: loading services, interacting with services and starting or ending services. It maintains a database that can be queried using a Windows built-in utility, `sc.exe`.

### svchost.exe

- The **Service Host** (Host Process for Windows Services), or **svchost.exe**, is responsible for hosting and managing Windows services.

## ==LSASS==

- Local Security Authority Subsystem Service (**LSASS**) is a process in Microsoft Windows operating systems that is responsible for enforcing the security policy on the system.
    - It verifies users logging on to a Windows computer or server, handles password changes, and creates access tokens. It also writes to the Windows Security Log.

### winlogon.exe

- The **Windows Logon**, **winlogon.exe**, is responsible for handling the **Secure Attention Sequence** (SAS). It is the ALT+CTRL+DELETE key combination users press to enter their username & password.
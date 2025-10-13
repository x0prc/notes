---
dg-publish: true
---






## ==GUI Based Bypasses==

### msconfig

- This is possible thanks to a feature called auto elevation that allows specific binaries to elevate without requiring the user's interaction.
- If we could force msconfig to spawn a shell for us, the shell would inherit the same access token used by msconfig and therefore be run as a high IL process. By navigating to the Tools tab, we can find an option to do just that:
- If we click Launch, we will obtain a high IL command prompt without interacting with UAC in any way.

### azman.msc

- As with msconfig, azman.msc will auto elevate without requiring user interaction. If we can find a way to spawn a shell from within that process, we will bypass UAC. Note that, unlike msconfig, azman.msc has no intended built-in way to spawn a shell. We can easily overcome this with a bit of creativity.
- This will once again bypass UAC and give us access to a high integrity command prompt. You can check the process tree in Process Hacker to see how the high integrity token is passed from mmc (Microsoft Management Console, launched through the Azman), all the way to cmd.exe

## ==Auto Elevating Processes==

### AutoElevate

- For an application, some requirements need to be met to auto-elevate:
    - The executable must be signed by the Windows Publisher
    - The executable must be contained in a trusted directory, like `%SystemRoot%/System32/` or `%ProgramFiles%/`

### Fodhelper

- Fodhelper.exe is one of Windows default executables in charge of managing Windows optional features, including additional languages, applications not installed by default, or other operating system characteristics.

## ==**Clearing our tracks**==

As a result of executing this exploit, some artefacts were created on the target system, such as registry keys. To avoid detection, we need to clean up after ourselves with the following commands:

```Plain
reg delete "HKCU\Software\Classes\.thm\" /f
reg delete "HKCU\Software\Classes\ms-settings\" /f
```

## ==Env Var Expansion==

### **Case study: Disk Cleanup Scheduled Task**

- The task can be run on-demand, executing the following command when invoked:

`%windir%\system32\cleanmgr.exe /autoclean /d %systemdrive%`

- Since the command depends on environment variables, we might be able to inject commands through them and get them executed by starting the DiskCleanup task manually.

## ==Automating UAC Bypasses==

- Refer to UACMe
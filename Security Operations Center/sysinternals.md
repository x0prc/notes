---
{"dg-publish":true,"permalink":"/src/site/notes/src/site/notes/src/site/notes/src/site/notes/main/cs/security-operations-center/sysinternals/"}
---






## Sigcheck

- A command-line utility that shows file version number, timestamp information, and digital signature details, including certificate chains.

`sigcheck -u -e C:\Windows\System32`

## Streams

- Alternate Data Streams (ADS) is a file attribute specific to Windows NTFS (New Technology File System). Every file has at least one data stream ($DATA) and ADS allows files to contain more than one stream of data.
    - Natively Window Explorer doesn't display ADS to the user. There are 3rd party executables that can be used to view this data, but Powershell gives you the ability to view ADS for files.

## SDelete

- A command line utility that takes a number of options. In any given use, it allows you to delete one or more files and/or directories, or to cleanse the free space on a logical disk.

## TCPView

- A Windows program that will show you detailed listings of all TCP and UDP endpoints on your system, including the local and remote addresses and state of TCP connections.

## Autoruns

- What programs are configured to run during system bootup or login, and when you start various built-in Windows applications like Internet Explorer, Explorer and media players.

## ProcDump

- A command-line utility whose primary purpose is monitoring an application for CPU spikes and generating crash dumps during a spike that an administrator or developer can use to determine the cause of the spike.

## BgInfo

- It automatically displays relevant information about a Windows computer on the desktop's background, such as the computer name, IP address, service pack version, and more.
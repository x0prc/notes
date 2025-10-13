---
dg-publish: true
---






## ==Processes==

- Maintains and represents the execution of a program, containing one or more processes.
- Potential Attack Vectors attackers use :
    - Process Injection (T1055)
    - Process Hollowing (T1055.012)
    - Process Masquerading (T1055.013)

## ==Threads==

- Executable unit deployed by a process and scheduled based on device factors.

## ==Virtual Memory==

- Allow other internal components to interact with memory as if it was physical memory without the risk of collisions between applications.
- Refer to Address Windowing Extensions for more.

## ==Dynamic Link Libraries==

- A library containing code that can be used by more than one program at the same time.
- Potential attack vectors attackers use :
    - DLL Hijacking (T1574.001)
    - DLL Side-Loading (T1574.002)
    - DLL Injection (T1055.001)

## ==Portable Executable Formats==

- Contains hex dump of an exe.
- Portable Executable (PE) and COFF (Common Object File Format) make up the PEFs.
---
dg-publish: true
permalink:
---






- TCP and UDP both use logical ports to multiplex connections between machines, **==permitting one host to serve many different services to many hosts.==**
    - When a network service like a web server starts **==it attaches, or binds,==** to one or more logical ports.
- A logical port is a number ==**between 0 and 65,535, for a total of 65,536 ports.**==

## ==Port Numbers Assigned by Default==

- Email services run on TCP ports 25 and 587.
- Web requests use TCP port 80,
- and SSL web requests use TCP port 443.
- UDP port 514 is used for log messages,
- while TCP port 514 is assigned to remote shell.

## ==The Services File==

- The services file /etc/services lists services commonly used on the machine and the logical TCP or UDP port they normally use.
    - Some programs usethis file to see what port they should bind to or query on.

## ==Sockets==

- A socket is a communication endpoint for a process. It’s a virtual construction for plugging communication into.
- Both Windows and Unix have ==**local sockets**==, which are system entities on the filesystem or in memory that accept connections from other programs.
- **==Inter-process communication (IPC)==** is another common socket protocol, but it’s contained entirely in memory.
- A socket waiting for a connection is said to be an **==open socket or listening.==**

## ==Network Daemons and the Root User==

- Privileged ports for ports below 1024 are normally assigned to the ==**most popular or important Internet services such as web servers and email.**==
- Some software starts as root but then drops privilege **==(privilege separation).==**
- Some operating systems give **==specific unprivileged users permission to listen to specific privileged ports.==**
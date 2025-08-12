---
dg-publish: true
permalink:
---






- With a netcat listener on one host, and netcat on another, you can send data, files, or anything from one host to another across any TCP/IP port.

## ==TCP listeners==

- Use the –l flag to tell netcat to listen. Here is shown how you can create a network socket on TCP port 9999.
    - **nc –l 9999**

## ==UDP Listeners==

- Here’s a netcat listener on UDP port 8888.
    - **nc –ul 8888**
- Netcat displays exactly what it receives. Real applications that use UDP implement their own error correction.

## ==Sending Files with Netcat==

- The contents of any data stream sent to TCP port 9999 will get sent to the specified file.
    - **nc –l 9999 > received_file**
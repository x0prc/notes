---
dg-publish: true
permalink:
---






## ==Three-Way Handshake==

1. First Stage : a SYN request or **==SYN_SENT==**, is when a client requests a TCP connection from a server. (SYN stands for “synchronization request.”)
2. At the second stage, **==SYN-ACK==**, the server responds to the SYN request. (ACK - Acknowledged)
3. The third stage, **==ACK==**, is when the client acknowledges the server’s synchronization request. **==One SYN and one ACK in each direction.==**

- When the servers finish exchanging data, both sides request and acknowledge teardown. **==This is where you get states like CLOSE_WAIT, TIME_WAIT, FIN_WAIT_2, and LAST_ACK.==**
- The whole three-way handshake ==**should take milliseconds, or possibly a second or two on slow, laggy, or overloaded links.**==

## ==TCP Failures==

- If the client or server has a problem during the connection, **==they might send a TCP reset message.==**
- While this can be caused by a firewall or a network issue, it’s most ==**commonly a server-side error.**==
- Some network security devices send **==TCP resets to disrupt undesirable traffic.==**

## ==lsof==

- lsof -i
    - for all network ports in use.
- lsof -n -i
    - to turn off DNS resolution.

## ==netstat usage (windows only)==

- netstat -na -p tcp
    - for only TCP communications
- netstat -na -p tcpv6
    - for only IPv6 communications
- netstat -na -p udp and udpv6
    - for UDPv6 communications
- netstat -na | findstr LISTEN
    - for only sockets which were listening
- netstat -na -b
    - Prints te name of the program using a connection or creating a socket.
- netstat -na -bo
    - If netstat cant figure out who owns the process.

## ==netstat usage (linux/unix only)==

- netstat -a
    - For every socket that’s open on the system.
    - Add -n to disable DNS lookups.
    - Add -f inet and -f inet6 for IPv4 and IPv6 respectively.
- netstat -t
    - For only TCP connections.
    - And -u to show UDP connections.
- netstat -l
    - For sockets that are waiting for a connection.
    - -ln4 for IPv4
- netstat -ptln
    - for taking a look at exactly what’s listening on the port.
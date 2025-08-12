---
dg-publish: true
permalink:
---






- TCP/IP refers to the whole family of protocols related to TCP and IP:
    - **==ICMP, UDP, and TCP itself==**, as well as less common protocols like **==SCTP and ESP and AH and dozens of others.==**
- While TCP on IPv4 is not identical to TCP running on IPv6, **==concepts like port numbers and connection states remain unchanged.==**

## ==ICMP==

- Internet Control Message Protocol (ICMP) ==**transmits availability, routing, and status messages.**==
- ICMP for IPv4 and IPv6 transmit similar types of messages, **==but internally they’re completely different.==**

## ==UDP==

- User Datagram Protocol, or UDP, is the most minimal transport protocol available in TCP/IP
- It is used for applications that do their own data flow error management.
- If the network drops a UDP packet, ==**neither the sending nor receiving UDP layers in the operating system ever know.**==
    - An application that’s expecting a packet **==might notice and ask the sender to resend, but that’s the application’s responsibility.==**
- The packets have no defined order. Each is **==complete in and of itself and is called connectionless.==**
- **==Almost all VPNs use UDP,==** although some use special VPN-specific protocols like IPSec.
    - The protocols running over the VPN manage all necessary error correction, **==so the VPN doesn’t need to handle those itself.==**

## ==TCP==

- The Transport Control Protocol (TCP) includes **==much of the error correction that UDP lacks.==**
    - The receiver acknowledges **==every single packet it receives==**. The sender **==retransmits any packet that isn’t acknowledged.==**
    - Applications that run over TCP expect the ==**operating system to deliver exactly the traffic that was sent.**==
- A chunk of application data **==can be broken into several TCP packets and streamed across the network as a single entity.==**
- One host requests a connection.
    - The destination host either accepts, rejects, or ignores the request.
    - If the destination accepts the request, it sends back information on how to connect.
    - When the first host acknowledges the receipt of that information, it can start transmitting actual data.
    - **==This setup process is called the==** _**==three-way handshake.==**_
- Once both hosts finish with the connection they must go through a little dance to tear it down, ==**the four-way handshake.**==
- VoIP does not work over TCP due to two-minute long gaps between packets sent/or not sent.
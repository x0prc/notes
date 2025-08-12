---
dg-publish: true
permalink:
---






- A _packet sniffer_ ==**displays packets as they cross a network interface.**==
    - The sniffer can capture and display everything that **==arrives from the network and==**  
        **everything that leaves the server.**  
        
- Packet sniffers have sophisticated filters that let you select **==exactly what traffic you capture and display, so you can narrow in on what you’re looking for.==**
- tcpdump and Wireshark are the most practical network sniffers.

## ==Packet Sinffer Interfaces==

- Packet sniffers have sophisticated filters that let you select exactly **==what traffic you capture and display, so you can narrow in on what you’re looking for.==**
- Some packet sniffers can ==**capture traffic on USB ports or weird logical interfaces**====**.**==

## ==Using tcpdump==

- _tcpdump -D_
    - To see which interfaces thinks it can capture on
- _tcpdump -i 1_
    - Specify an interface with -i, such as -i em0 or -i 1.

## ==Reading UDP Packets==

- **==The first field==**, 14:59:50.351940, is a timestamp.
- **==The second field==**, IP, shows that this is an IP packet.
- **==The third field==** is the IP address or hostname that is the source of the packet.
    - The source port, appears after the hostname or IP address, separated by a period.
- **==The arrow==** indicates that this packet is moving on to another host.

## ==Reading TCP Packets==

- TCP packet shown in tcpdump resembles a UDP packet, but has additional information that represents the connection state and the packet’s role in the data stream.
- A TCP packet can and often should have multiple flags set. The flags are:
    - An _S_ means that this is a ==**SYN packet.**== It’s part of the initial three-way  
        handshake, either from the client or from the server.  
        
    - A period (_._) is an **==ACK, or an acknowledgement.==** This packet contains  
        information acknowledging receipt of other packets.  
        
    - An **==_R_== ==is a TCP reset.==** The connection is forcibly terminated. If no  
        connection exists yet, this translates to “connection refused.”  
        
    - An **==_F_== ==in a FIN packet,==** part of the four-way connection teardown  
        handshake.  
        
    - **==_U_== ==(urgent),== ==_W_== ==and== ==_E_== ==(for congestion control), or== ==_P_== ==(push)==**. These flags are important for more complicated debugging.

## ==Reading ARP (Lower Level Problems)==

- As with all tcpdump entries, **==each packet starts with a timestamp.==**
- **==The second field==** shows that these are not IP packets, but rather ARP frames.
    - The first frame is an ARP request.
    - The second line is an ARP response, giving the physical (MAC) address that claims ownership of the IP address.

## ==Filtering Captures==

- **==Filter Format==**
    - **tcpdump –n –i** _**interface**_ _**filter-expressions**_
- **==Capturing ARP Traffic==**
    - **tcpdump -ni 1 arp**
    - **tcpdump -ni 1 ether host 9C:B6:54:1C:D4:E3**
        - For only MAC Address
- **==Filtering by IP Addresses==**
    - **tcpdump -ni 1 ip**
    - **tcpdump -ni 1 ip host mail.google.com**
    - **tcpdump -ni 1 ip host 203.0.113.64 and \(ip host 203.0.113.26 or 203.0.113.15\)**
- **==Filtering by TCP and UDP Ports==**
    - **tcpdump –ni 1 udp**
    - **tcpdump -ni 1 tcp port 822**

## ==Capturing a File==

- **./WinDump -w web.pcap -ni 1 ip host www and `(port 80 or 443`)**
- **==Reading a Capture File==**
    
    - **tcpdump -r web.pcap**  
          
        
    - **tcpdump -nr web.pcap (Disable DNS Lookups)**
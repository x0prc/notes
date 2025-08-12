---
dg-publish: true
permalink:
---






## ==Windows==

- _**==ipconfig.exe==**_
    - Can add /all tag for even more information about a host’s network interfaces.

## ==Unix==

- _**==ifconfig==**_
    - -a can be added to show all interfaces.
    - **==_eth0 and lo._==**
        - The lo interface is the local loopback interface, present on every computer. It has no hardware, but is a logical interface the host uses to talk to itself.
        - eth0, the network-facing interface. This is an Ethernet interface and gives its hardware (MAC) address. Below that is the IP address, the top (unusable) address for the subnet this IP is on, and the netmask.
- **_==route==_**
    - -rn flags display the system’s routing table.
    - Routes are usually displayed by address and netmask. The default gateway  
        is identified by the word default or something like 0.0.0.0/0.
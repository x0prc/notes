---
dg-publish: true
permalink:
---





- Every device on ethernet needs a unique identifer called a ==**MAC Address or Ethernet Address.**==
    - MAC Address is 48 bits long, written as six pairs of colon-separated hexadecimal numbers. (23:34:00:3f:2b:12). Windows systems use dashes instead of colons.
    - First six numbers of the MAC adress identifies the Ethernet card manufacturer.
    - If the switch knows that the MAC address 52:54:00:3b:2b:25 is connected to switch port 87, ==**it sends traffic for that MAC address exclusively to that port.**==
- Category 5, “cat5” cable, is the usual lowest common denominator these days. ==**It has a maximum throughput of 100Mbs.**==
- A cat5e cable can **==handle gigabit speeds.==**
- Datacenters might use cat6 cable, **==which can handle 10Gbps.==**
- If you’re involved in the initial wiring of a new facility, you might consider **==cat7 cable, which can handle 40Gbs.==**

## ==Speed & Duplex==

- Duplex refers to how each end **==handles transmitting and receiving data.==**
- An interface running at half duplex **==can either receive or transmit data at any instance==**, but not both.
- A full duplex connection **==can simultaneously send and receive.==**
- Gigabit and faster Ethernet connections negotiate much more than speed and duplex, and **==autonegotiation is a mandatory part of the protocol.==**
    
    - Some network cards let the sysadmin **==hard-code gigabit speed and full duplex.==**
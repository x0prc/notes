---
dg-publish: true
permalink:
---






- IPv6 uses **==128-bit addresses==**, shown as eight colon-separated **==groups of four hexadecimal characters==**, such as 2a03:2880:2130:cf05:face:b00c:0:1.
- At the datalink layer IPv6 uses **==Neighbor Discovery (ND)==** rather than ARP.

## ==Essentials==

- One interesting difference between IPv4 and IPv6 is that in many operating systems, the last part of the host’s **==IPv6 address can be computed from the network card’s physical address (MAC address).==**
    - This behavior has gradually been replaced with **==non-reversible ways to generate IPv6 addresses, and there’s discussion of obsoleting the reversible method.==**
- In addition to the primary address, a host can have many temporary IPv6 addresses.
    - This partially addresses the **==privacy issues of tying an IP address to a piece of physical hardware.==**

## ==Writing IPv6 Addresses==

- The way that IPv6 manages and assigns subnets leads to addresses with long strings of zeroes. You **==can drop==** ==**leading zeroes from any four-hex section.**==
- When an IPv6 address includes multiple blocks of zeroes, **==you can replace the longest string with two colons.==**
    - The address 2001:0db8:000c:0000:0000:0000:000d:0001 usually appears as 2001:db8:c::d:1.
    - Only do the double-colon replacement once per **==IP address, however, because otherwise it’s ambiguous.==**

## ==IPv6 Netmasks==

- IPv6 is normally subnetted only at colon boundaries. ==**Colons appear every 16 bits, so the natural IPv6 subnets are /16, /32, /48, and /64.**==
- The IPv6 standards recommend using **==/64 as the standard network on a small network==**  
    **like an office LAN or your home.**  
    - A /64 contains 264 IP addresses, more than enough for any Ethernet broadcast domain. IPv6 netmasks almost always appear in slash notation, but sometimes you’ll see the words **==prefix length==** instead.

## ==IPv6 Autoconfiguration==

- Servers that require ==**static addresses should be careful with IPv6 autoconfiguration.**==
- An IPv6 host can support **==multiple addresses through IP aliases, just like an IPv4 host, and can be multihomed.==**

## ==Link-Local Addresses==

- All addresses beginning with **==fe8==** are link-local addresses, valid only on that specific interface’s broadcast domain.
- IPv6 hosts on that Ethernet network can find each other and **==communicate via the link-local address.==**
    - Link-local networks ==**are always /64 networks.**==
- The operating system attaches the interface name to the **==link-local address so it can tell them apart.==**
    - A link-local address usually appears with a **==percent sign and the interface name or number at the end of the address.==**
- Link-local addresses have many theoretical advantages, but for the practical-minded, **==they make standalone IPv6 networks self-configuring.==**

## ==Usage==

- route –rn –A inet6 (Linux) or route –rn –f inet6 (BSD).

## ==Tunnels==

- Organizations like Hurricane Electric offer IPv6 tunnels, **==allowing a network or organization to get IPv6 connectivity over an IPv4 connection==**. These ==**tunnels let you test IPv6 in your environment before your ISP offers it.**==
- Even if your organization has lots of Internet bandwidth, a **==tunneled IPv6 connection must traverse your IPv4 connection, go to the tunnel provider, and then out to the Internet.==**

## ==IPv4 versus IPv6==

- If a host uses both IPv4 and IPv6, **==incoming connection requests get processed via the protocol that they arrive on.==**
- Outgoing connections can use either **==IPv6 or IPv4, depending on the operating system.==**
    
    - Microsoft **==Windows Vista and later prefer IPv6 if configured.==** Microsoft offers patches that control IPv6 and IPv4 preferences.
    - OpenBSD and some Linux variants, rely upon ==**DNS to decide if they’re going to use IPv4 or IPv6.**==
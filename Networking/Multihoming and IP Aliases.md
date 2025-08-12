---
dg-publish: true
permalink:
---






- A host can have two (or more) network interfaces, each with its own IP address, **==each in a different broadcast domain with different IP networks.==**
    - Interface 1 might be on a public network and have an IP address of 192.0.2.2/28, while interface 2 might be on the private network and have an IP of 172.16.99.9/24.
    - Such a host is called ==_**multihomed**_==.
- A multihomed host automatically connects directly to hosts on subnets it’s attached to, **==using its IP address on that subnet.==**
- A host can have multiple IP addresses on one network interface through **==IP aliasing==**.
    - The interface has a primary IP address, but it also answers ARP requests for the aliased IP addresses.
    - Aliases are one way for a single host to communicate with **==multiple IP subnets on one physical Ethernet.==**
    - The host initiates connections from **==whichever IP address it has on that subnet.==**
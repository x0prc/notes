---
dg-publish: true
permalink:
---






- A netmask indicates the size of a subnet.
    - Like an IP address, a netmask is ==**a 32-bit number usually expressed as four decimal numbers**==, often called a dotted quad.
    - Unlike an IP, a netmask is defined by its length in bits. **==The common 255.255.255.0 netmask is 24 bits long.==**
        - A 24-bit netmask has the first **==24 bits set to 1 and the remaining bits set to 0.==**
- Hosts on the network can use any value between 1 and 254 for the last number, but if they change any of the earlier numbers they **==lose access to other hosts on that network.==**
- When combined with an IP address, a netmask is usually represented by a slash (/) and its bit length.
    - That is, the IP 192.0.2.1 with a 24-bit netmask is written as 192.0.2.1/24. **==This is called CIDR (Classless Inter-Domain Routing) notation.==**

## ==Unusable IPv4 Addresses==

- The first and last IP addresses in a subnet are unusable for protocol design reasons.
    - The **==bottom number is the network address==**, the **==top is the broadcast address==**.

## ==Routers & the Default Gateway==

- A router is a device that sends traffic from one IP subnet to another. ==**It might also convert one physical layer to another.**==
- If a host needs to get to a system that’s not on the local network, it sends the packets to the default gateway. **==That’s generally the router on the local network.==**
- The default router on an IPv4 network needs an IPv4 address. The default router on an IPv6 router needs an IPv6 address. **==These addresses might be on the same device, or not.==**
- Normally the main router sends an **==ICMP redirect message==** when the client tries to reach a host behind a secondary router,
    
    - Telling the client to go to the secondary router for that host.
    - The client automatically sends all traffic **==for that destination address to the proper router.==**
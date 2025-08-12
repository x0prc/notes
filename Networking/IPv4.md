---
dg-publish: true
permalink:
---






- Hosts meant for end users, like desktops, laptops, and tablets, normally get their configuration via the ==**Dynamic Host Configuration Protocol (DHCP).**==
- To connect a host to a network it needs a valid IP address and a subnet mask.
    - If it needs to communicate with hosts beyond the local network, it needs a default gateway. **==Knowing the addresses of your DNS servers is a definite plus.==**
- IPv4 address is a **==32-bit number assigned==** to a specific network device, globally unique to network.
- Rather than a single large number, IP addresses are usually expressed as **==four eight-bit decimal==** numbers, such as 203.0.113.1. This **==“dotted quad==**==”== notation is easier.
- A block of IP addresses is called a **==network or subnet==**. Organization’s Internet Service Provider (ISP) allocates a subnet to the organization.
    - Strictly speaking, all the IP addresses on the Internet are one network. Every smaller **==allocation is a subnet, or a subnet of a subnet.==**
- Hosts can only communicate directly with hosts on the same IP subnet. To communicate with hosts on a **==different network, they must go through a router—even if they’re on the same Ethernet.==**
    
    - Each subnet contains a number of **==addresses equal to a power of 2.==**
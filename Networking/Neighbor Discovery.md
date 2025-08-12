---
dg-publish: true
permalink:
---






- Neighbor discovery (ND) is the IPv6 datalink protocol, ==**replacing the Address Resolution Protocol used in IPv4 Ethernet.**==
    - Neighbor discovery is supposed to work on all datalink protocols, not just Ethernet, but Ethernet is still the most common.
- Neighbor discovery is extremely similar to ARP. The **==IP addresses are larger, and the state table has a few more entries.==**
- Unlike ARP, where entries are either present or missing, neighbor cache entries can have a few different states :
    1. _==Reachable addresses==_ are currently live on the network.
    2. _==Stale addresses==_ were live, but have since expired from the cache.
    3. _==Permanent addresses==_ are either local on the machine, or special-purpose addresses that are always present.
    4. _==Failed addresses==_ are neighbors the host has looked for but not found.

## ==Windows ND==

```Shell
netsh interface ipv6 show neighbors
```

## ==Unix ND==

```Shell
netstat -pn -f inet6 (Solaris)

ip -6 neighbor show (Linux)
```
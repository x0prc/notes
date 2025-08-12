---
dg-publish: true
permalink:
---






- The Address Resolution Protocol, maps **==Ethernet addresses to IPv4 addresses and back.==**
- A host that needs to transmit data to another host on the local Ethernet first broadcasts an Ethernet request asking “Which MAC address is responsible for this IP address?” These ==**broadcasts go to all hosts attached to that Ethernet network.**==

## ==ARP Cache==

- When a host maps a MAC address to an IP address, it caches that information in the ARP table for a few minutes.
    - Once the cache entry expires, it re-queries the network via ARP.
- The better failover implementations send an unrequested gratuitous ==**ARP message to announce the new MAC address for an IP address.**==
- Command to view a host’s ARP table :

```Shell
arp -a
```

- If a host doesn’t have an ARP entry, your host either **==hasn’t communicated with that host before==**, or the **==target host’s ARP cache entry has expired.==**
- If only address filter is requested, the IP address can be added after arp -a.
---
dg-publish: true
permalink:
---






- A local area network, or LAN, is an Ethernet broadcast domain. All the hosts on the LAN can see each other.
    - But sometimes you need a special-purpose host on multiple LANs **==that’s where the virtual LAN comes in handy==**
- VLAN, is an extra tag on Ethernet frames indicating that they belong on a different LAN than the default.
- Each VLAN is identified by a number from **==1 to 4096.==**
- For a VLAN to function, the switch **==port your hosts connect to needs a VLAN configuration.==**
    - Some switches auto-configure requested VLANs, while others require manual intervention.
- VLANs are sometimes described as 802.1Q.

## ==VLAN Terminology==

- A ==_network trunk_== combines multiple physical layers into one datalink layer.
    - Your server gets two network cables, and you **==configure the server to group them together into one connection.==**
    - This creates redundancy, so that a failure of one switch or one cable or one network card doesn’t **==disconnect the server from the network.==**
    - These kinds of trunks are very useful and popular.
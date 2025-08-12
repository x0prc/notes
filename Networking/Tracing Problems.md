---
dg-publish: true
permalink:
---






- The traceroute program lets you follow packets as they travel between hosts, viewing what hosts they pass through to reach their destination.
- **traceroute www.google.com**
    - **==Each following line==** is a separate host (router or router-like device, such as a firewall) along the way. The number at the start of the line is the hop number. Typically 7 Hops.
    - **==The time stamp==** is how long it takes for a packet to reach that hop and return.
    - ==**The asterisk**== indicates a lost packet. Either the request did not reach the device, this device did not respond to this packet, or the response did not make it back to the client.
    - Hop 7 and 8 are in the domain. These are both **==Internet== ==_backbone carriers_====, really big long-distance Internet Service Providers.==**

## ==Traceroute Errors==

### ==Slow Traces==

- Traceroute might run very, very slowly. A common cause of this is DNS lookups. It does a reverse DNS check of every hop along the way.

### ==Time Spikes==

- If a particular hop loses packets or has high response times, but the following hops look better, the router with the high times has decided to not spend any energy processing your traceroute request.

### ==Time Jumps==

- A traceroute all the way around the Earth, at the equator, on good fiber, takes about 400 milliseconds.
- If you see a sudden time increase intermixed with asterisks, it can indicate problems starting at the first troubled router.

### ==Multiple Hosts at One Hop==

- Networks can load balance traffic just as servers can. A busy connection might have multiple routers. Each will return its own traceroute timestamp to the client.

### ==! Errors==

- Rather than a hostname or timestamp, sometimes a traceroute ends in an error code like !H or !X
    - **==!H==** means that the next host is unreachable.
    - **==the !N==** error means that the entire destination network is unreachable.
    - ==**!A, !X, or !Z**== means that further communication is administratively prohibited.
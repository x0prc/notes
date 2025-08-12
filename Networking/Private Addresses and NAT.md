---
dg-publish: true
permalink:
---






- Some addresses are reserved for special purposes, and trying to use them as regular network addresses breaks applications.
    - If an organization runs an internal private network, they should use ==**these dedicated addresses.**==
- The networks 10.0.0.0/8, 172.16.0.0/12, and 192.168.0.0/16 are freely usable by organizations only (within).

## ==Proxy Server==

- If a host only has private addresses, how do you access the Internet? Use either a proxy server or NAT.
- A ==**proxy server**== accepts requests for Internet resources.
    - Take a web browser set to use a proxy server. When you try to get a web page, the browser contacts the proxy.
    - The proxy asks the web browser to hold on for a moment, then requests that page on the browser’s behalf.
- A proxy server **==can be very secure, but it limits the Internet activity users can perform==**. Not all network protocols can go through a proxy.

## ==Network Address Translation==

- NAT rewrites packets in flight. When a host with a private IP address sends traffic through a NAT device, the ==**NAT device rewrites the outbound traffic so that it appears to be coming from the NAT device’s public IP address.**==
    - When the remote site answers, the **==NAT device rewrites the response so that it goes to the original client.==**
    - The NAT device maintains a table of connections, **==and tracks the state of each connection so that it can properly open and close connections as needed.==**

## ==Firewall==

- A firewall is most often some combination of ==**packet filter, proxy server and NAT.**==
- Some firewalls are glorified NATs, others are proxies, and some offer **==both feature sets, with varying degrees of reliability and security.==**
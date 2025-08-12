---
dg-publish: true
permalink:
---






- DNS provides a map between human-friendly hostnames (like [www.mwl.io](http://www.mwl.io/)) and IP addresses like 192.0.2.8.
    - Without DNS, you’d browse the web ==**with IP addresses instead of hostnames.**==
- DNS runs on TCP and UDP, **==using port 53 on both.==**

## ==Principles==

- A nameserver is a piece of software that **==searches for and collects address and hostname mappings.==**
    - The nameserver checks its ==**local cache to see if it already has an answer.**==
- You must always specify **==DNS servers by IP address, not hostname==**. A host can’t look up hostnames until it can use DNS.

### ==Domains & Zones==

- Every top level domain like **==.com and .net is a zone.==**
    - All of the top level domains are contained in the ==**all-encompassing**== ==**_root zone_**====**.**==
- A zone inside another zone is called **==a== ==_child zone_====.==**
    - The zone [google.com](http://google.com/) is a child zone of the .com zone.
- A zone that holds other zones **==is a== ==_parent zone_====.==**
    - The .com and top level domains are parent zones.
- A complete collection of data for a zone **==is called a== ==_zone file_====.==**

### ==Authoritative & Recursive DNS==

- _Authoritative nameservers_ ==**contain the information for specific domains.**==
    - Anyone in the world who wants to perform DNS queries on google.com domains gets an authoritative answer from google’s servers.
- _Recursive nameservers_ **==provide DNS lookups for clients==**.
    - When you browse to cnn.com, your computer asks a recursive nameserver for the IP address to connect to.
    - The recursive nameserver finds the authoritative nameserver for  
        **==the destination site, queries it, and returns the answer to your computer.==**
- Best practice says that authoritative and recursive **==nameservers should be on different machines.==**

### ==Forward & Reverse DNS==

- ==**Forward DNS maps hostnames to IP addresses.**== The client requests the IP for [mwlucas.org](http://mwlucas.org/) and gets an answer like 203.0.113.99.
- **==Reverse DNS maps IP addresses to hostnames.==** The client requests the hostname assigned to the IP address at 203.0.113.99 and gets an answer like [www.ignoredsince1993.net](http://www.ignoredsince1993.net/).
- A forward DNS query can return more than one answer. A reverse DNS query should only return one hostname, however.

### ==DNS Record Types==

- An _A_ (address) record contains an IPv4 address. If you have a hostname and want to find its **==IP address, your query should return an A record.==**
- an _AAAA_ record contains an IPv6 address. If your client wants a ==**host’s IPv6 record, it will ask the nameserver for its AAAA record.**==
- A _PTR_ (pointer) record contains a hostname. When you have an **==IP address and want to know the hostname tied to it, the client requests a PTR record.==**
- An _SOA_ (Start of Authority) record gives timing and **==responsibility information for the zone you’re searching.==**
- A CNAME (canonical name) **==is a DNS alias, redirecting one name to another.==**
- An MX (mail exchanger) **==record identifies one of the mail servers for a zone.==**

### ==DNS Caching==

- Recursive DNS servers cache collected answers until a per-DNS-record timer expires. Once the answer expires, **==the recursive DNS server throws the data away.==**
- Some operating systems run local DNS response caches. Windows, for example, automatically remembers recent DNS requests.
    - Various Unixes might use a name service caching **==daemon like nscd for local name caching.==**
    - You can flush local caches by restarting the **==Unix name caching daemon or running ifconfig /flushdns on Windows.==**

### ==Running DNS Queries==

- Windows provides the ==**nslookup**== command for DNS debugging. On Unix systems, use ==**host**==.
    - Add -v for additional details.
- DNS queries most often return three response codes: **==NOERROR, NXDOMAIN, and SERVFAIL.==**
    - NXDOMAIN means that the DNS protocol worked, **==but that the DNS doesn’t contain any records of the name you’re looking for.==**
    - SERVFAIL means that **==something went wrong, and you can’t get an answer.==**

## ==Hosts File==

- The Domain Name Service is not the only source of information on  
    hostname-to-IP mappings. You can manually create these mappings **==on an==**  
    **individual machine by using the hosts file.**  
    - Unix uses the file _/etc/hosts_
    - Windows uses _C:\\Windows\System32\drivers\etc\hosts_.
- Format : ==_ipaddress hostname aliases_==
    - List any desired aliases after that entry.
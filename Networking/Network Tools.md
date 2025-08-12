---
dg-publish: true
permalink:
---






```Shell
ifconfig, route and ipconfig
```

- A host’s network configuration includes its IP addresses and gateway.
    - On Unix, use the route and ifconfig commands to view the system’s network configuration.
    - Windows systems put all of these in the ==_ifconfig_== command.

```Shell
grep and findstr
```

- The ==_grep_== (Unix) and _==findstr==_ (Windows) commands let you search for a specific string within a pile of output.

```Shell
netstat
```

- The ==_netstat_== command displays a system’s established network connections, what connections the system can receive, and network statistics.

```Shell
lsof
```

- The ==_lsof_== command lets you see hat processes open which files.

```Shell
route
```

- The ==_route_== command both displays where the system send traffic and gives you the ability to change how the system delivers traffic.

```Shell
tcpdump
```

- The _==tcpdump==_ command displays traffic to and from a server, even when the server rejects that traffic.

```Shell
netcat
```

- The _==netcat==_ program lets you listen to the network on a specific port, and lets you send arbitrary network traffic.

```Shell
traceroute
```

- The _==traceroute==_ program (tracert in Windows) shows you the route that traffic takes and where these links break.

```Shell
host and nslookup
```

- The _==host==_ (Unix) and _==nslookup==_ (Windows) commands let you peek at the Domain Name Service, which maps host names to IP addresses.
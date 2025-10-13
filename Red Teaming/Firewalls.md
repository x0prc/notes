---
dg-publish: true
---






## ==Controlling the MAC/IP/Port for Evasion==

### Decoy(s)

- Using decoys makes your IP address mix with other “decoy” IP addresses. Consequently, it will be difficult for the firewall and target host to know where the port scan is coming from.
- Using the `-D` option, you can add decoy source IP addresses to confuse the target.

### Proxy

- Use an HTTP/SOCKS4 proxy. Relaying the port scan via a proxy helps keep your IP address unknown to the target host.
- This technique allows you to keep your IP address hidden while the target logs the IP address of the proxy server. You can go this route using the Nmap option `--proxies PROXY_URL`.

### Spoofed MAC Address

- Spoof the source MAC address. Nmap allows you to spoof your MAC address using the option `--spoof-mac MAC_ADDRESS`.
- This technique is tricky; spoofing the MAC address works only if your system is on the same network segment as the target host.

### Spoofed IP Address

- Spoof the source IP address. Nmap lets you spoof your IP address using`-S IP_ADDRESS`.
- Spoofing the IP address is useful if your system is on the same subnetwork as the target host; otherwise, you won’t be able to read the replies sent back.

### Fixed Source Port Number

- Use a specific source port number. Scanning from one particular source port number can be helpful if you discover that the firewalls allow incoming packets from particular source port numbers, such as port 53 or 80.
- Without inspecting the packet contents, packets from source TCP port 80 or 443 look like packets from a web server, while packets from UDP port 53 look like responses to DNS queries.
- You can set your port number using `-g` or `--source-port` options.

## ==Packets with Specific Length==

- Fragment IP data into 8 bytes

```Plain
-f
```

- Fragment IP data into 16 bytes

```Plain
-ff
```

- Fragment packets with given MTU

```Plain
--mtu VALUE
```

- Specify packet length

```Plain
--data-length NUM
```

## ==Port Hopping==

- You can use the command `ncat -lvnp PORT_NUMBER` to listen on a certain TCP port.

## ==Port Tunnelling==

- ncat -lvnp 443 -c "ncat TARGET_SERVER 25”

## ==Non-Standard Ports==

- `ncat -lvnp PORT_NUMBER -e /bin/bash` will create a backdoor via the specified port number that lets you interact with the Bash shell.
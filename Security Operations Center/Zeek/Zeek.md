---
{"dg-publish":true,"permalink":"/src/site/notes/src/site/notes/src/site/notes/src/site/notes/main/cs/security-operations-center/zeek/zeek/"}
---






- Zeek (formerly Bro) is an open-source and commercial passive Network Monitoring tool (traffic analysis framework) developed by Lawrence Berkeley Labs.

## Architecture

![Untitled 5.png|Untitled 5.png](/img/user/img/Untitled%205.png)

## Frameworks

|   |   |   |   |   |
|---|---|---|---|---|
|Logging|Notice|Input|Configuration|Intelligence|
|Cluster|Broker Communication|Supervisor|GeoLocation|File Analysis|
|Signature|Summary|NetControl|Packet Analysis|TLS Decryption|

## Working

|   |   |
|---|---|
|**Parameter**|**Description**|
|**-r**|Reading option, read/process a pcap file.|
|**-C**|Ignoring checksum errors.|
|**-v**|Version information.|
|**zeekctl**|ZeekControl module.|

## Logs

|   |   |   |
|---|---|---|
|Category|Description|**Log Files**|
|Network|Network protocol logs.|_conn.log, dce_rpc.log, dhcp.log, dnp3.log, dns.log, ftp.log, http.log, irc.log, kerberos.log, modbus.log, modbus_register_change.log, mysql.log, ntlm.log, ntp.log, radius.log, rdp.log, rfb.log, sip.log, smb_cmd.log, smb_files.log, smb_mapping.log, smtp.log, snmp.log, socks.log, ssh.log, ssl.log, syslog.log, tunnel.log._|
|Files|File analysis result logs.|_files.log, ocsp.log, pe.log, x509.log._|
|NetControl|Network control and flow logs.|_netcontrol.log, netcontrol_drop.log, netcontrol_shunt.log, netcontrol_catch_release.log, openflow.log._|
|Detection|Detection and possible indicator logs.|_intel.log, notice.log, notice_alarm.log, signatures.log, traceroute.log._|
|Network Observations|Network flow logs.|_known_certs.log, known_hosts.log, known_modbus.log, known_services.log, software.log._|
|Miscellaneous|Additional logs cover external alerts, inputs and failures.|_barnyard2.log, dpd.log, unified2.log, unknown_protocols.log, weird.log, weird_stats.log._|
|Zeek Diagnostic|Zeek diagnostic logs cover system messages, actions and some statistics.|_broker.log, capture_loss.log, cluster.log, config.log, loaded_scripts.log, packet_filter.log, print.log, prof.log, reporter.log, stats.log, stderr.log, stdout.log._|

## Processing Zeek Logs

|   |   |   |   |
|---|---|---|---|
|Category|Command Purpose and Usage|Category|Command Purpose and Usage|
|Basics|View the command history:`ubuntu@ubuntu$ history`  <br>  <br>Execute the 10th command in history:  <br>  <br>`ubuntu@ubuntu$ !10`  <br>  <br>Execute the previous command:`ubuntu@ubuntu$ !!`|**Read File**|Read sample.txt file:  <br>  <br>`ubuntu@ubuntu$ cat sample.txt`  <br>  <br>  <br>  <br>Read the first 10 lines of the file:  <br>  <br>`ubuntu@ubuntu$ head sample.txt`  <br>  <br>  <br>  <br>Read the last 10 lines of the file:  <br>  <br>`ubuntu@ubuntu$ tail sample.txt`|
|Find&Filter|Cut the 1st field:  <br>  <br>`ubuntu@ubuntu$ cat test.txt \| cut -f 1`  <br>  <br>  <br>  <br>Cut the 1st column:  <br>  <br>`ubuntu@ubuntu$ cat test.txt \| cut -c1`  <br>  <br>  <br>  <br>Filter specific keywords:  <br>  <br>`ubuntu@ubuntu$ cat test.txt \| grep 'keywords'`  <br>  <br>  <br>  <br>Sort outputs alphabetically:  <br>  <br>`ubuntu@ubuntu$ cat test.txt \| sort`  <br>  <br>Sort outputs numerically:  <br>  <br>`ubuntu@ubuntu$ cat test.txt \| sort -n`  <br>  <br>Eliminate duplicate lines:  <br>  <br>`ubuntu@ubuntu$ cat test.txt \| uniq`  <br>  <br>  <br>  <br>Count line numbers:  <br>  <br>`ubuntu@ubuntu$ cat test.txt \| wc -l`  <br>  <br>  <br>  <br>Show line numbers  <br>  <br>`ubuntu@ubuntu$ cat test.txt \| nl`|Advanced|Print line 11:`ubuntu@ubuntu$ cat test.txt \| sed -n '11p'`  <br>  <br>Print lines between 10-15:`ubuntu@ubuntu$ cat test.txt \| sed -n '10,15p'`  <br>  <br>Print lines below 11:  <br>  <br>`ubuntu@ubuntu$ cat test.txt \| awk 'NR < 11 {print $0}'`  <br>  <br>  <br>  <br>Print line 11:  <br>  <br>`ubuntu@ubuntu$ cat test.txt \| awk 'NR == 11 {print $0}'`|

|   |   |
|---|---|
|**Special**|Filter specific fields of Zeek logs:`ubuntu@ubuntu$ cat signatures.log \| zeek-cut uid src_addr dst_addr`|

|   |   |
|---|---|
|**Use Case**|**Description**|
|`sort \| uniq`|Remove duplicate values.|
|`sort \| uniq -c`|Remove duplicates and count the number of occurrences for each value.|
|`sort -nr`|Sort values numerically and recursively.|
|`rev`|Reverse string characters.|
|`cut -f 1`|Cut field 1.|
|`cut -d '.' -f 1-2`|Split the string on every dot and print keep the first two fields.|
|`grep -v 'test'`|Display lines that  don't match the "test" string.|
|`grep -v -e 'test1' -e 'test2'`|Display lines that don't match one or both "test1" and "test2" strings.|
|`file`|View file information.|
|`grep -rin Testvalue1 * \| column -t \| less -S`|Search the "Testvalue1" string everywhere, organise column spaces and view the output with less.|

## Signatures

|   |   |
|---|---|
|**Condition Field**|**Available Filters**|
|Header|src-ip: Source IP.dst-ip: Destination IP.src-port: Source port.dst-port: Destination port.ip-proto: Target protocol. Supported protocols; TCP, UDP, ICMP, ICMP6, IP, IP6|
|Content|**payload:** Packet payload.**http-request:** Decoded HTTP requests.**http-request-header:** Client-side HTTP headers.**http-request-body:** Client-side HTTP request bodys.**http-reply-header:** Server-side HTTP headers.**http-reply-body:** Server-side HTTP request bodys.**ftp:** Command line input of FTP sessions.|
|Context|**same-ip:** Filtering the source and destination addresses for duplication.|
|Action|**event:** Signature match message.|
|Comparison Operators|**==**, **!=**, **<**, **<=**, **>**, **>=**|

## Cleartext Submission of Password

```JavaScript
signature http-password {
     ip-proto == tcp
     dst_port == 80
     payload /.*password.*/
     event "Cleartext Password Found!"
}

# signature: Signature name.
# ip-proto: Filtering TCP connection.
# dst-port: Filtering destination port 80.
# payload: Filtering the "password" phrase.
# event: Signature match message.
```

## FTP Brute-force

```JavaScript
signature ftp-admin {
     ip-proto == tcp
     ftp /.*USER.*dmin.*/
     event "FTP Admin Login Attempt!"
}
```

## Scripts 101

- Basic Scripting

```JavaScript
event zeek_init()
    {
     print ("Started Zeek!");
    }
event zeek_done()
    {
    print ("Stopped Zeek!");
    }

# zeek_init: Do actions once Zeek starts its process.
# zeek_done: Do activities once Zeek finishes its process.
# print: Prompt a message on the terminal.
```

```JavaScript
event new_connection(c: connection)
{
	print ("###########################################################");
	print ("");
	print ("New Connection Found!");
	print ("");
	print fmt ("Source Host: %s # %s --->", c$id$orig_h, c$id$orig_p);
	print fmt ("Destination Host: resp: %s # %s <---", c$id$resp_h, c$id$resp_p);
	print ("");
}

# %s: Identifies string output for the source.
# c$id: Source reference field for the identifier.
```

- Running these scripts
    - zeek -C -r sample.pcap 103.zeek
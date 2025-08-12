---
{"dg-publish":true,"permalink":"/src/site/notes/src/site/notes/src/site/notes/src/site/notes/main/cs/security-operations-center/snort/snort/"}
---






## ==Sniffing with parameter "-i"==

- Start the Snort instance in **verbose mode (-v)** and **use the interface (-i)** "eth0"; `sudo snort -v-i eth0`

## ==**Sniffing with parameter "-v"**==

- Start the Snort instance in **verbose mode (-v)**; `sudo snort -v`

## ==**Sniffing with parameter "-d"**==

- Start the Snort instance in **dumping packet data mode (-d)**; `sudo snort -d`

## ==**Sniffing with parameter "-de"**==

- Start the Snort instance in **dump (-d)** and **link-layer header grabbing (-e)** mode; `snort -d -e`

## ==**Sniffing with parameter "-X"**==

- Start the Snort instance in **full packet dump mode (-X)**; `sudo snort -X`

  

> _Can open these files with Wireshark as well_

## ==Snort in IDS/IPS Mode==

NIDS mode parameters are explained in the table below;

|   |   |
|---|---|
|**Parameter**|**Description**|
|-c|Defining the configuration file.|
|-T|Testing the configuration file.|
|**-N**|Disable logging.|
|**-D**|Background mode.|
|**-A**|Alert modes;  <br>**full:** Full alert mode, providing all possible information about the alert. This one also is the default mode; once you use -A and don't specify any mode, snort uses this mode.  <br>  <br>  <br>**fast:**  Fast mode shows the alert message, timestamp, source and destination IP, along with port numbers.  <br>  <br>console: Provides fast style alerts on the console screen.  <br>**cmg:** CMG style, basic header details with payload in hex and text format.  <br>**none:** Disabling alerting.|

## ==Snort Rules==

  

![Untitled 3.png|Untitled 3.png](/img/user/img/Untitled%203.png)
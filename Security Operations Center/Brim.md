---
{"dg-publish":true,"permalink":"/src/site/notes/src/site/notes/src/site/notes/src/site/notes/main/cs/security-operations-center/brim/"}
---






- An open-source desktop application that processes pcap files and logs files. Its primary focus is providing search and analytics.

## **Brim Query Reference**

|   |   |   |
|---|---|---|
|**Purpose**|**Syntax**|**Example Query**|
|Basic search|You can search any string and numeric value.|Find logs containing an IP address or any value.`10.0.0.1`|
|Logical operators|Or, And, Not.|Find logs contain three digits of an IP AND NTP keyword.`192 and` `NTP`|
|Filter values|"field name" == "value"|Filter source IP.`id.orig_h==192.168.121.40`|
|List specific log file contents|_path=="log name"|List the contents of the conn log file.`_path=="conn"`|
|Count field values|count () by "field"|Count the number of the available log files.`count () by _path`|
|Sort findings|sort|Count the number of the available log files and sort recursively.`count () by _path \| sort -r`|
---
{"dg-publish":true,"permalink":"/src/site/notes/src/site/notes/src/site/notes/src/site/notes/main/cs/security-operations-center/sysmon/"}
---






## ==Event IDs==

**Event ID 1: Process Creation**

**Event ID 3: Network Connection**

**Event ID 7: Image Loaded**

**Event ID 8: CreateRemoteThread**

**Event ID 11: File Created**

**Event ID 12 / 13 / 14: Registry Event**

**Event ID 15: FileCreateStreamHash**

**Event ID 22: DNS Event**

## ==**Filtering Events with PowerShell**==

- Filter by Event ID: `*/System/EventID=<ID>`
- Filter by XML Attribute/Name: `*/EventData/Data[@Name="<XML Attribute/Name>"]`
- Filter by Event Data: `*/EventData/Data=<Data>`
    - We can put these filters together with various attributes and data to get the most control out of our logs. Look below for an example of using `Get-WinEvent` to look for network connections coming from port 4444.

## ==Hunting Network Connections==

- We will first be looking at a modified Ion-Security configuration to detect the creation of new network connections.
    - The code snippet below will use event ID 3 along with the destination port to identify active connections specifically connections on port `4444` and `5555`.
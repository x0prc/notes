---
{"dg-publish":true,"permalink":"/src/site/notes/src/site/notes/src/site/notes/src/site/notes/main/cs/security-operations-center/splunk/"}
---






Splunk has three main components, namely Forwarder, Indexer, and Search Head.

## Forwarder

- Splunk Forwarder is a lightweight agent installed on the endpoint intended to be monitored, and its main task is to collect the data and send it to the Splunk instance. It does not affect the endpoint's performance as it takes very few resources to process. Some of the key data sources are:
    - Web server generating web traffic.
    - Windows machine generating Windows Event Logs, PowerShell, and Sysmon data.
    - Linux host generating host-centric logs.
    - Database generating DB connection requests, responses, and errors.

## Indexer

- Splunk Indexer plays the main role in processing the data it receives from forwarders. It takes the data, normalizes it into field-value pairs, determines the datatype of the data, and stores them as events. Processed data is easy to search and analyze.

## Head

- Splunk Search Head is the place within the Search & Reporting App where users can search the indexed logs as shown below. When the user searches for a term or uses a Search language known as Splunk Search Processing Language, the request is sent to the indexer and the relevant events are returned in the form of field-value pairs.

## Incident Handling

1. Preparation
2. Detection and Analysis
3. Containment, Eradication and Recovery
4. Post-Incident Activity

## Cyber Kill Chain

- Reconnaissance
- Weaponisation
- Delivery
- Exploitation
- Installation
- Command & Control
- Actions on Objectives
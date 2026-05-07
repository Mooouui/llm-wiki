---
title: "MID Server"
type: entity
tags: [ServiceNow, Discovery, infrastructure, security]
sources: [ingest-data-into-the-cmdb]
last_updated: 2026-04-27
---

# MID Server

The Management, Instrumentation, and Discovery (MID) Server is a [[ServiceNow]] component that acts as a secure bridge between the ServiceNow instance and an organization's internal network. It is critical for [[ServiceNowDiscovery]] in environments where direct communication is restricted by firewalls or network segmentation.

## How It Works

1. ServiceNow sends probes (information requests) to the MID Server
2. The MID Server executes probes against target systems within the internal network
3. Probes use protocols appropriate to the target: WMI for Windows, SSH for Unix/Linux, SNMP for network devices
4. Sensors on the ServiceNow side process the returned data and update the [[CMDB]]

## Security Model

- Operates within the organization's trusted network — sensitive data and credentials never leave organizational boundaries
- Uses encrypted communication between MID Server and ServiceNow instance
- No permanent software installed on target devices (agentless)

## Sources

- [[ingest-data-into-the-cmdb|Ingest Data into the CMDB]] — MID Server role in Discovery

---
title: "ServiceNow Discovery"
type: entity
tags: [ServiceNow, CMDB, Discovery, ITOM, agentless]
sources: [ingest-data-into-the-cmdb]
last_updated: 2026-04-27
---

# ServiceNow Discovery

ServiceNow Discovery (also known as horizontal discovery, agentless discovery, or IP-based discovery) is an automated network scanning solution that detects and catalogs all IP-enabled devices and applications within an IT infrastructure on a scheduled basis. It is part of the [[ServiceNow]] ITOM Visibility product suite.

## Key Characteristics

- **Agentless** — uses the [[MIDServer]] to probe devices via WMI (Windows), SSH (Unix/Linux), and SNMP (network devices) without installing permanent software
- **Schedule-based** — not real-time; for real-time discovery use [[AgentClientCollector]]
- **Four discovery phases**: Scan → Classification → Identification → Exploration
- Supports Windows, Linux, macOS, and cloud environments
- All collected data routes through the [[IRE]] to prevent duplicates

## Discovery Phases

1. **Scan** — sweeps IP ranges to detect live hosts
2. **Classification** — uses probes and sensors to determine device type (server, router, switch, printer)
3. **Identification** — gathers unique identifiers (serial number, MAC, hostname) to match or create CIs
4. **Exploration** — collects detailed data (installed software, hardware configs, running processes)

## Limiting Discovery

Start with small IP ranges to avoid data overload. Maximum recommended range: /16 (65,000 IPs). Use the Discovery Configuration Console to exclude specific device classes and focus on priority CIs.

## Discoverable vs. Non-Discoverable Data

Discovery collects [[DiscoverableData|discoverable data]] (hardware, software, network details, cloud resources). [[NonDiscoverableData|Non-discoverable data]] like group assignments and location must be supplemented manually after discovery.

## Sources

- [[ingest-data-into-the-cmdb|Ingest Data into the CMDB]] — full product overview and configuration

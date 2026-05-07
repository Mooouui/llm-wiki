---
title: "Discoverable Data"
type: concept
tags: [ServiceNow, CMDB, Discovery, automation]
sources: [ingest-data-into-the-cmdb]
last_updated: 2026-04-27
---

# Discoverable Data

Discoverable data refers to hardware, software, network, and cloud resource information that can be automatically collected by [[ServiceNowDiscovery]], [[ServiceMapping]], and [[ServiceGraphConnectors]] and populated into the [[CMDB]].

## Examples

- **Hardware details** — CPU, memory, storage
- **Software details** — installed applications and operating systems
- **Network details** — IP addresses, MAC addresses, network topology
- **Cloud resources** — AWS, Azure, Google Cloud instances and services
- **Discovery source** — set to "ServiceNow" when discovered; previously set to "SNAssetManagement" for asset-created records until discovery overrides it

## Contrast

Unlike [[NonDiscoverableData]], discoverable data can be fully automated. 90% of CMDB data should be automatically populated, with the remaining 10% requiring manual governance for non-discoverable attributes.

## Sources

- [[ingest-data-into-the-cmdb|Ingest Data into the CMDB]] — discoverable vs. non-discoverable data distinction

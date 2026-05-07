---
title: "Ingest Data into the CMDB"
type: source
tags: [ServiceNow, CMDB, Ingest, Discovery, ServiceMapping, ACC, IntegrationHubETL, ServiceGraphConnectors]
date: 2026-04-27
source_file: raw/articles/Ingest Data into the CMDB.md
---

## Summary
ServiceNow training material covering the full spectrum of tools for populating and maintaining CMDB data. Details six ingestion methods — Discovery (horizontal/agentless), Service Mapping (top-down), Agent Client Collector (ACC, agent-based), Service Graph Connectors (third-party integrations), IntegrationHub ETL (modern ETL interface), and legacy Import Sets/Transform Maps. Concludes with methods for populating non-discoverable foundation data (group assignments, location) via CI Class Manager and technology management offerings within the CSDM framework.

## Key Claims
- 90% of CMDB data should be automatically populated; only 10% manually updated after governance
- ServiceNow Discovery is schedule-based, not real-time; ACC provides real-time agent-based discovery
- The MID Server acts as a secure bridge for Discovery in firewalled/segmented networks
- IntegrationHub ETL is the modern replacement for legacy Import Sets/Transform Maps, offering a simplified UI with native IRE integration
- Non-discoverable data (group assignments, location) is critical for incident and change routing and must be supplemented after automated discovery
- CI Class Manager handles Managed By Group; technology management offerings handle Managed By, Support, and Change groups with higher priority
- Service Graph Connectors are CSDM-conformant and leverage IntegrationHub ETL under the hood
- All data ingestion routes through the IRE to prevent duplicates and maintain integrity
- Discovery should start with small IP ranges to avoid data overload; /16 is the maximum recommended range

## Key Quotes
> "After ingesting data, a substantial amount of valuable CI data is available in the ServiceNow CMDB. As a crucial next step that is often forgotten, ServiceNow strongly recommends that the CMDB team supplement the discovered data collected by the automated discovery tools with non-discoverable data."
> "The most effective CMDB's are populated using automation with tools like Service Mapping Discovery. 90% of the data in your CMDB should be automatically populated, leaving the other 10% to be updated manually after proper governance."
> "ServiceNow Discovery is schedule based; therefore, it is not considered a real-time discovery solution. For true real-time discovery, ServiceNow offers Agent Client Collector."

## Connections
- [[ServiceNow]] — the platform providing all these ingestion tools
- [[ServiceNowDiscovery]] — horizontal/agentless discovery product
- [[ServiceMapping]] — top-down service dependency mapping
- [[AgentClientCollector]] — agent-based real-time discovery
- [[ServiceGraphConnectors]] — third-party connector ecosystem
- [[IntegrationHubETL]] — modern ETL data integration
- [[MIDServer]] — secure bridge for internal network discovery
- [[CSDM]] — Common Service Data Model governing service modeling
- [[CMDB]] — the target database for all ingestion methods
- [[IRE]] — all ingestion routes through IRE for data integrity
- [[configure-the-cmdb|Configure the CMDB]] — companion source on CMDB governance

## Contradictions
- None detected with existing wiki content. Complements [[configure-the-cmdb|Configure the CMDB]] by covering the "how data gets in" side, while the earlier source covers the "how CMDB is governed" side.

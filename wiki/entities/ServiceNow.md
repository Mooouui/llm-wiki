---
title: "ServiceNow"
type: entity
tags: [platform, enterprise, ITSM, CMDB]
sources: [configure-the-cmdb]
last_updated: 2026-04-22
---

# ServiceNow

ServiceNow is an enterprise cloud platform for IT service management (ITSM), IT operations management (ITOM), and business workflow automation. Within the context of this wiki, it is the platform that provides the [[CMDB]] and associated configuration management tooling.

## Key Products and Features

- **CI Class Manager** — centralized tree-view for managing CMDB class hierarchies, identification rules, reconciliation rules, and health settings
- **Discovery** — automated tool for populating the CMDB by scanning the network
- **Service Mapping** — maps dependencies between CIs to model business services
- **Service Graph Connectors** — integrations with third-party data sources for CMDB population
- **IntegrationHub ETL** — extract-transform-load capabilities for CMDB data ingestion
- **CMDB Workspace** — modern interface for viewing and managing CMDB data

## CMDB Configuration Roles

Only users with the following roles can create new CMDB classes:
- `sn_cmdb_admin` and `personalize_dictionary`
- `admin`

## Sources

- [[configure-the-cmdb|Configure the CMDB]] — detailed configuration guide

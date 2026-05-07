---
title: "ServiceNow"
type: entity
tags: [platform, enterprise, ITSM, CMDB]
sources: [configure-the-cmdb, ingest-data-into-the-cmdb, govern-the-cmdb]
last_updated: 2026-05-07
---

# ServiceNow

ServiceNow is an enterprise cloud platform for IT service management (ITSM), IT operations management (ITOM), and business workflow automation. Within the context of this wiki, it is the platform that provides the [[CMDB]] and associated configuration management tooling.

## Key Products and Features

### Data Ingestion
- **[[ServiceNowDiscovery|Discovery]]** — agentless/horizontal IP-based network scanning; schedule-based, not real-time; uses [[MIDServer]] for secure internal network access
- **[[ServiceMapping|Service Mapping]]** — top-down service dependency discovery and modeling; builds application service maps aligned with [[CSDM]]
- **[[AgentClientCollector|ACC]]** — agent-based real-time discovery; collects software utilization data for SAM; suited for intermittently connected or secured endpoints
- **[[ServiceGraphConnectors]]** — pre-built integrations with AWS, Azure, SCCM, Jamf, and other third-party tools; CSDM-conformant, routes through [[IRE]]
- **[[IntegrationHubETL]]** — modern ETL interface replacing legacy Import Sets; uses Robust Transform Engine to generate IRE payloads; supports non-CMDB tables

### CMDB Governance
- **[[CMDBHealth|CMDB Health Dashboard]]** — monitors data quality via Completeness, Compliance, and Correctness scorecards; generates remediation tasks for failing CIs
- **Duplicate CI Remediator** — wizard-driven tool for one-at-a-time duplicate reconciliation (merge or delete)
- **De-Duplication Templates** — bulk duplicate resolution with pre-configured, schedulable merge/delete rules per class
- **Now Assist for CMDB** — generative AI for automated duplicate CI detection, resolution, and CI summarization
- **CMDB Data Manager** — policy-driven [[LifeCycleManagement|lifecycle management]]: Retire, Archive, Delete, Attestation, and Certification policies; workflow-based UI in CMDB Workspace
- **CMDB Workspace** — modern interface for CMDB data management, de-duplication dashboard, and Data Manager access

### Configuration
- **CI Class Manager** — centralized tree-view for managing CMDB class hierarchies, identification rules, reconciliation rules, and health settings
- **[[IRE|Identification & Reconciliation Engine]]** — gatekeeper processing all CMDB writes; handles identification, reconciliation, deduplication, and reclassification
- **[[MultisourceCMDB|CMDB 360]]** — attribute-level data provenance tracking across multiple discovery sources

## CMDB Configuration Roles

Only users with the following roles can create new CMDB classes:
- `sn_cmdb_admin` and `personalize_dictionary`
- `admin`

Data Manager roles:
- `data_manager_admin` — full policy management access
- `data_manager_user` — limited access

## Sources

- [[configure-the-cmdb|Configure the CMDB]] — detailed configuration guide
- [[ingest-data-into-the-cmdb|Ingest Data into the CMDB]] — data ingestion methods and tools
- [[govern-the-cmdb|Govern the CMDB]] — governance tools, health dashboard, lifecycle management

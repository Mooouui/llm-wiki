---
title: "CMDB"
type: concept
tags: [ITSM, configuration-management, data-integrity, governance]
sources: [configure-the-cmdb, ingest-data-into-the-cmdb, govern-the-cmdb]
last_updated: 2026-05-07
---

# CMDB (Configuration Management Database)

A Configuration Management Database (CMDB) is a centralized repository that stores information about configuration items (CIs) — hardware, software, network assets, and their relationships — within an organization's IT environment.

## Core Principles

- **Start simple, grow incrementally** — building a comprehensive CMDB immediately is a common mistake; begin with core use cases and expand
- **Data integrity is paramount** — inaccurate CMDB data causes downstream reports and processes to fail
- **Multiple sources require governance** — when Discovery, import sets, and third-party tools all write to the CMDB, the risk of duplicates and inconsistencies increases sharply
- **Governance completes the lifecycle** — after configuration and ingestion, ongoing health monitoring, duplicate remediation, and lifecycle management keep the CMDB trustworthy

## Three-Phase Lifecycle

### 1. Configuration
Setting up CI classes, identification rules, reconciliation rules, and data sources via [[ServiceNow|CI Class Manager]].

### 2. Ingestion
Populating the CMDB via six methods:

1. **[[ServiceNowDiscovery|Discovery]]** — agentless, schedule-based network scanning
2. **[[ServiceMapping|Service Mapping]]** — top-down service dependency modeling
3. **[[AgentClientCollector|ACC]]** — agent-based real-time discovery with software utilization
4. **[[ServiceGraphConnectors]]** — pre-built third-party integrations (AWS, Azure, SCCM, etc.)
5. **[[IntegrationHubETL]]** — modern ETL interface for custom data imports
6. **Import Sets & Transform Maps** — legacy method, superseded by IntegrationHub ETL

All methods route data through the [[IRE]] to prevent duplicates. Ingested data falls into two categories: [[DiscoverableData]] (auto-collected hardware/software/network details) and [[NonDiscoverableData]] (group assignments, location — must be manually populated).

### 3. Governance
Maintaining data quality over time through [[CMDBHealth|CMDB Health]] monitoring, duplicate remediation, CI reclassification control, and [[LifeCycleManagement|lifecycle management]] via Data Manager policies.

## Key Components

- **CI Classes** — hierarchical taxonomy of configuration items (e.g., Server → Linux Server → specific subclass). Extend existing classes rather than creating new ones to avoid license, governance, and interoperability issues.
- **CI Attributes** — properties of a CI (serial number, host name, IP address, RAM, etc.)
- **Relationships** — connections between CIs (dependency, containment, etc.)
- **Identification Rules** — define how CIs are uniquely identified using stable attributes
- **Reconciliation Rules** — determine which data source is authoritative for each class/attribute

## Key Tools

### Configuration & Ingestion
- [[ServiceNow|CI Class Manager]] — centralized management interface
- [[IRE|Identification & Reconciliation Engine]] — processes all data before it enters the CMDB
- [[MultisourceCMDB|CMDB 360]] — tracks all discovery source values at the attribute level

### Governance
- [[CMDBHealth|CMDB Health Dashboard]] — three scorecards (Completeness, Compliance, Correctness) with health inclusion rules, remediation workflows, and scheduled jobs
- **Duplicate CI Remediator** — wizard-driven tool for reconciling duplicate CIs one at a time
- **De-Duplication Templates** — bulk duplicate resolution via pre-configured merge/delete rules per class, schedulable for regular maintenance
- **Now Assist for CMDB** — AI-driven duplicate detection and resolution using generative AI
- **CMDB Data Manager** — policy-driven framework for CI lifecycle (retire, archive, delete, attest, certify), accessible from CMDB Workspace
- **CI Reclassification** — IRE-controlled upgrade/downgrade/switch of CIs between classes, with restriction rules for class-level granularity
- **Life Cycle Fields** — [[CSDM]]-standardized Life Cycle Stage and Life Cycle Stage Status replacing legacy fields, with automatic CI-Asset synchronization

## Sources

- [[configure-the-cmdb|Configure the CMDB]] — comprehensive configuration guide
- [[ingest-data-into-the-cmdb|Ingest Data into the CMDB]] — data ingestion methods and tools
- [[govern-the-cmdb|Govern the CMDB]] — governance, health, and lifecycle management

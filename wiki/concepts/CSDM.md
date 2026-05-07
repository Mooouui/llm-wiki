---
title: "Common Service Data Model"
type: concept
tags: [ServiceNow, CMDB, service-modeling, standards, governance, lifecycle]
sources: [ingest-data-into-the-cmdb, govern-the-cmdb]
last_updated: 2026-05-07
---

# Common Service Data Model (CSDM)

The Common Service Data Model (CSDM) is a standardized framework of terms, definitions, and prescriptive guidelines for service modeling within the [[ServiceNow]] [[CMDB]]. It provides the foundation for consistent service reporting across all ServiceNow products on the platform.

## Key Concepts

- Standardizes how IT services, applications, infrastructure, and their relationships are represented
- Defines domains including Service Delivery for application service modeling
- All [[ServiceGraphConnectors]] are reviewed for CSDM conformance
- [[ServiceMapping]] supports CSDM by automating discovery and maintenance of application services within the CSDM framework

## CSDM & Foundation Data

CSDM defines technology management services (formerly technical services) and technology management offerings (formerly technical service offerings) as essential components for managing foundation data — including group assignments (Managed By, Support, Change groups) — across the IT landscape.

## CSDM Life Cycle Fields

CSDM introduced standardized lifecycle fields to replace multiple legacy status fields that had accumulated across products:

### Legacy Fields (still widely used)
- CI: Operational Status, Install Status, Hardware Status, Substatus
- Asset: State, Substate

### CSDM Standard Fields (CI and Asset)
- **Life Cycle Stage** — the lifecycle phase (e.g., Operational, Retired, Archived)
- **Life Cycle Stage Status** — the detailed status within a stage

The `life_cycle_mapping` table provides pre-populated mappings from legacy status values to CSDM life cycle pairs. Enabling life cycle sync performs a one-time migration and then maintains bidirectional synchronization between legacy and CSDM fields — and between CI and Asset records. Not all legacy fields should be managed simultaneously (e.g., choose between Install Status and Hardware Status, not both).

## Value

- Enables consistent service reporting
- Provides prescriptive guidance for service modeling
- Aligns CMDB structure with industry best practices
- Standardizes lifecycle tracking across CI and Asset records

## Sources

- [[ingest-data-into-the-cmdb|Ingest Data into the CMDB]] — CSDM role in service mapping and data ingestion
- [[govern-the-cmdb|Govern the CMDB]] — CSDM life cycle fields and CI-Asset synchronization

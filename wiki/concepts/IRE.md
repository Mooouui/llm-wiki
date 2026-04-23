---
title: "Identification & Reconciliation Engine"
type: concept
tags: [CMDB, data-integrity, ServiceNow]
sources: [configure-the-cmdb]
last_updated: 2026-04-22
---

# Identification & Reconciliation Engine (IRE)

The IRE is the central framework in [[ServiceNow]] that processes all data payloads before they enter the [[CMDB]]. It ensures no data source writes directly to the CMDB — all sources call IRE APIs first to prevent duplicates and unauthorized updates.

## Four Core Functions

1. **Identification** — uniquely identifies CIs to determine if a CI already exists or is new, using identification rules with stable, unique attributes (serial number, host name, install directory — never ephemeral attributes like IP address)
2. **Reconciliation** — allows only designated authoritative data sources to update CI records at the table and attribute level, using reconciliation rules and data refresh rules
3. **Deduplication** — groups duplicate CIs into de-duplication tasks for review and remediation via de-duplication wizard and templates
4. **Reclassification** — handles cases where a matched CI needs to be upgraded, downgraded, or switched to another class; generates reclassification tasks if automatic reclassification is disabled

## Process Flow

Data sources (Discovery, AWS, SCCM, Service Graph Connectors, REST integrations) → IRE APIs → Identification → Reconciliation → CMDB update

## IRE Support for Non-CMDB Tables

IRE also supports specific non-CMDB tables in the base system: Location, Department, Cost Center, Building, User, and Group. These require direct table management (not CI Class Manager).

## Key Warnings

- **Duplicate CIs** occur when identification rules don't ensure unique, stable identifiers
- **Overloaded CIs** occur when different CIs are incorrectly identified as the same CI
- ServiceNow provides no baseline reconciliation rules — customers must configure them per environment

## Sources

- [[configure-the-cmdb|Configure the CMDB]] — IRE overview and configuration details

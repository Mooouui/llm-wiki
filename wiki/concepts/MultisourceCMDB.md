---
title: "Multisource CMDB / CMDB 360"
type: concept
tags: [CMDB, data-provenance, ServiceNow]
sources: [configure-the-cmdb]
last_updated: 2026-04-22
---

# Multisource CMDB / CMDB 360

Introduced in the ServiceNow Paris release, CMDB 360 (also called Multisource CMDB) retains complete history about discovery sources and proposed values involved in updates of [[CMDB]] CI attributes. Without it, details about lower-priority discovery sources whose values were rejected are permanently lost.

## What It Solves

- **Data provenance** — track how the CMDB is populated by various discovery sources at the CI attribute level
- **Source auditability** — revert CI updates from a specific discovery source
- **Rule recomputation** — recompute attribute values using updated reconciliation rules without re-discovery
- **Data gap analysis** — compare values reported by different sources (e.g., SCCM vs. ServiceNow Discovery)

## Storage

All data is stored in the **CMDB MultiSource Data `[cmdb_multisource_data]`** table. This table retains raw details for every discovery source — both selected and rejected.

## Activation Steps

1. Activate ITOM Discovery License plugin (`com.snc.itom.vis.license`)
2. Set system property `glide.identification_engine.multisource_enabled` to `true`

## Dynamic Reconciliation Rules

Dynamic reconciliation rules are only available when Multisource CMDB is enabled. They use multisource data to select values by:
- **First Reported** — earliest value wins
- **Most Reported** — most common value wins
- **Last Reported** — most recent value wins
- **Largest / Smallest Value** — numeric comparison only

When both static and dynamic rules apply to the same CI attribute, **dynamic rules take precedence**.

## Visibility

CMDB 360 data can be accessed from: CI Class Manager, CMDB 360 Data Preview link, Multisource Data related list, and CMDB Workspace. Dashboard analytics populate daily via the Multisource Dashboard Analytics Population scheduled job.

## Sources

- [[configure-the-cmdb|Configure the CMDB]] — Multisource CMDB configuration and dynamic reconciliation

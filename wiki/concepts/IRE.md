---
title: "Identification & Reconciliation Engine"
type: concept
tags: [CMDB, data-integrity, ServiceNow, reclassification]
sources: [configure-the-cmdb, ingest-data-into-the-cmdb, govern-the-cmdb]
last_updated: 2026-05-07
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

## Deduplication in Detail

IRE identifies duplicates when two or more CIs match based on the identification rules for the CI's class. Key behaviors:

- The oldest CI by creation date is treated as the non-duplicate; newer CIs are flagged via the *Duplicate Of* field
- CIs with a populated *Discovery Source* field are NOT flagged as duplicates by the Correctness scorecard (IRE assumes they've already been processed) — but if rediscovered later, they will be flagged
- Two system properties govern duplicate handling: `glide.identification_engine.skip_duplicates` (default: `true`) and `glide.identification_engine.skip_duplicates.threshold` (default: `5`)
- De-duplication tasks can be resolved via the **Duplicate CI Remediator** wizard (one at a time) or **De-Duplication Templates** (bulk, per class, schedulable)

### De-Duplication Templates

Pre-configured rules per class that automate bulk duplicate resolution:
- Configure matching rules (class, location, manufacturer, model, etc.)
- Choose merge or delete action
- Schedule for regular execution
- Thorough testing before publishing is recommended since duplicates are handled automatically

## CI Reclassification

During identification, the IRE can reclassify a CI from one class to another. Three types:

### Upgrade
CI moves to a derived child class with additional attributes. Example: `Server [cmdb_ci_server]` → `Windows Server [cmdb_ci_win_server]`. Safe — no data loss.

### Downgrade
CI moves to a parent class with fewer attributes. Example: `Windows Server [cmdb_ci_win_server]` → `Server [cmdb_ci_server]`. **Can cause data loss** — child-class-only attributes and their values are dropped.

### Switch
CI moves to a different branch in the hierarchy with a different attribute set. Example: `Linux Server [cmdb_ci_linux_server]` → `Windows Server [cmdb_ci_win_server]`. **Can cause data loss** — attributes not in the target class are lost.

### Reclassification Control

**Global properties** (base system defaults: all `true`, meaning automatic):
- `glide.class.upgrade.enabled`
- `glide.class.downgrade.enabled`
- `glide.class.switch.enabled`

When disabled, reclassification tasks are generated instead of automatic reclassification.

**Advanced global properties** (base system defaults: all `false`): When set to `true`, these allow CI attribute updates to proceed *without* the reclassification taking effect:
- `glide.identification_engine.update_without_switch_enabled`
- `glide.identification_engine.update_without_downgrade_enabled`
- `glide.identification_engine.update_without_upgrade_enabled`

For example, if `glide.class.downgrade.enabled=true` AND `glide.identification_engine.update_without_downgrade_enabled=true`, a Linux Server discovered as a Server will NOT be downgraded, but its attributes WILL still be updated.

### Reclassification Restriction Rules

For class-level granularity beyond global properties. Configured at `cmdb_ire_reclassification_restriction.list`. Rules specify:
- **Type**: downgrade or switch (upgrade is always safe)
- **Source table** and **Target table** (with optional inheritance to child classes)
- Only blocks the reclassification — CI attribute updates still proceed

## IRE Support for Non-CMDB Tables

IRE also supports specific non-CMDB tables in the base system: Location, Department, Cost Center, Building, User, and Group. These require direct table management (not CI Class Manager).

## Key Warnings

- **Duplicate CIs** occur when identification rules don't ensure unique, stable identifiers
- **Overloaded CIs** occur when different CIs are incorrectly identified as the same CI
- ServiceNow provides no baseline reconciliation rules — customers must configure them per environment
- Downgrade and switch reclassification can cause permanent data loss

## IntegrationHub ETL and IRE

In the [[IntegrationHubETL]] flow, the Robust Transform Engine (RTE) transforms staging table data into IRE payloads, which IRE then processes for reconciliation before writing to the CMDB. All [[ServiceGraphConnectors]] leverage this RTE → IRE pipeline.

## Sources

- [[configure-the-cmdb|Configure the CMDB]] — IRE overview and configuration details
- [[ingest-data-into-the-cmdb|Ingest Data into the CMDB]] — IRE role in IntegrationHub ETL pipeline
- [[govern-the-cmdb|Govern the CMDB]] — duplicate management, CI reclassification, and restriction rules

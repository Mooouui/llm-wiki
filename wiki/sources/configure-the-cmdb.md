---
title: "Configure the CMDB"
type: source
tags: [ServiceNow, CMDB, configuration-management, IRE, reconciliation]
date: 2026-04-22
source_file: raw/articles/Configure the CMDB.md
---

## Summary

A comprehensive guide to configuring the ServiceNow Configuration Management Database (CMDB), covering the CI Class Manager for centralized class management, the Identification and Reconciliation Engine (IRE) for maintaining data integrity across multiple sources, and CMDB 360/Multisource CMDB for tracking attribute-level data provenance. Also covers dynamic reconciliation rules for complex multi-source scenarios.

## Key Claims

- The CI Class Manager provides centralized management of the CMDB class hierarchy, identification rules, reconciliation rules, and health settings in a tree-view format
- Creating new CMDB classes should be done with extreme caution — prefer extending existing classes or installing the CMDB CI Class Models store application first
- The IRE is the central component for ingesting healthy data, preventing duplicates and controlling updates from multiple discovery sources
- Identification rules uniquely identify CIs using stable, unique attributes (e.g., serial number, host name) — never attributes that change over time (e.g., IP address)
- Reconciliation rules determine which data sources are authoritative for specific CI classes and attributes; ServiceNow provides no baseline reconciliation rules
- Data Refresh Rules allow lower-priority data sources to update a CI class when a higher-priority source hasn't updated within a configured interval
- CMDB 360/Multisource CMDB (Paris release) retains complete history of all discovery source values, including rejected ones, enabling auditability and recomputation
- Dynamic reconciliation rules use Multisource CMDB data to select values by criteria (first/most/last reported, largest/smallest value) and take precedence over static rules

## Key Quotes

> "Maintaining the integrity of your CMDB during implementation is crucial, and leveraging proven tools and processes is key." — opening premise

> "Building a comprehensive CMDB immediately is a common mistake. Instead, begin with a simple approach and make incremental improvements as your configuration management capabilities grow." — leading practice for CMDB implementation

> "When properly configured, reconciliation rules can manage 90% of the process to determine which data sources are trusted and identify the ultimate authoritative source of truth for a specific class, set of classes, and/or CI attributes." — on the power of reconciliation rules

> "Without a CMDB 360/Multisource CMDB, details about the lower-priority discovery sources whose values were rejected, are discarded and lost." — on why Multisource CMDB matters

## Connections

- [[ServiceNow]] — the platform providing all CMDB tooling described
- [[CMDB]] — the core concept; this source is a deep configuration guide
- [[IRE|Identification & Reconciliation Engine]] — central framework for CMDB data integrity
- [[MultisourceCMDB|Multisource CMDB / CMDB 360]] — attribute-level data provenance tracking

## Contradictions

- None found with existing wiki content (first ServiceNow/CMDB-related source)

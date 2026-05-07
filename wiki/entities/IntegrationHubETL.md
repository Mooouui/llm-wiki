---
title: "IntegrationHub ETL"
type: entity
tags: [ServiceNow, CMDB, ETL, data-integration, IRE]
sources: [ingest-data-into-the-cmdb]
last_updated: 2026-04-27
---

# IntegrationHub ETL

IntegrationHub ETL (Extract, Transform, Load) is a [[ServiceNow]] Store application that provides a modern, user-friendly interface for importing and integrating third-party data into the [[CMDB]] and supported non-CMDB tables. It is the recommended replacement for legacy Import Sets and Transform Maps.

## Architecture

### Key Components

- **Robust Transform Engine (RTE)** — transforms raw source data from staging tables into IRE payloads using ETL transform maps
- **[[IRE|Identification and Reconciliation Engine]]** — receives RTE payloads, performs reconciliation to prevent duplicates, and ensures target table integrity

### Process Flow

External source → Import Sets (staging tables) → RTE + ETL transform maps → IRE payloads → IRE processing → CMDB (system of record)

## Key Terms

- **CMDB Application** — the third-party vendor (e.g., SCCM) with a configured discovery source
- **ETL Transform Map** — the output defining how source data maps to target tables
- **Data Source** — the specific source feed (e.g., SCCM Computer Identity) from which raw data is imported

## Non-CMDB Table Support

Supports ingestion into non-CMDB tables: Location, Department, Cost Center, Building, User, and Group (`sys_user_group`).

## Why Use IntegrationHub ETL

- Routes data through IRE for data integrity
- Consistent, efficient transformation and mapping
- Test with small sample data sets, review results, and iterate before production runs

## Sources

- [[ingest-data-into-the-cmdb|Ingest Data into the CMDB]] — IntegrationHub ETL architecture and workflow

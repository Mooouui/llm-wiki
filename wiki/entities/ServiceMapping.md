---
title: "Service Mapping"
type: entity
tags: [ServiceNow, CMDB, service-modeling, ITOM, CSDM]
sources: [ingest-data-into-the-cmdb]
last_updated: 2026-04-27
---

# Service Mapping

Service Mapping (also known as top-down discovery, tag-based discovery, or ML-powered mapping) is a [[ServiceNow]] ITOM product that automatically discovers and models the relationships and dependencies between CIs that compose a business service, populating this information into the [[CMDB]].

## Key Characteristics

- **Top-down approach** — starts from the business service and maps down to supporting infrastructure, complementing the bottom-up approach of [[ServiceNowDiscovery]]
- **Dynamic updates** — automatically refreshes service maps as the environment changes
- **CSDM-aligned** — supports the [[CSDM|Common Service Data Model]] Service Delivery domain

## Application Services

An application service (`[cmdb_ci_service_auto]`) is an operational CI representing a deployed system or product stack, unique per instance/version, and may be created per environment (Dev/Test/QA/Prod), geographic region (AMS/EMEA/APJ), or line of business (HR/Marketing/Sales).

## Value

- Bridges the gap between IT operations (technology domains) and business users (service consumers)
- Enables instant visibility into which CIs support critical services for incident, problem, and change management
- Provides the service context needed for impact analysis and dependency management

## Sources

- [[ingest-data-into-the-cmdb|Ingest Data into the CMDB]] — product overview and CSDM alignment

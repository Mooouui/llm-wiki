---
title: "Non-Discoverable Data"
type: concept
tags: [ServiceNow, CMDB, governance, ITSM]
sources: [ingest-data-into-the-cmdb, govern-the-cmdb]
last_updated: 2026-05-07
---

# Non-Discoverable Data

Non-discoverable data is CMDB information that cannot be automatically collected by discovery tools and must be manually supplemented. It is essential for IT service management processes like incident routing and change management.

## Key Fields

- **Assigned to** — individual responsible for the CI
- **Owned by** — organizational owner
- **Support Group** — maps to Incident Assignment Group for incident routing
- **Change Group** — maps to Change Assignment Group for change routing
- **Managed By Group** — used for Data Manager task assignment (attestation, life cycle, certification policies)

## Population Methods

ServiceNow provides two methods for auto-populating group fields within the [[CSDM]] framework:

1. **CI Class Manager** — sets Managed By Group at the class level; applies to CIs not associated with a technology management offering
2. **Technology Management Offerings** — sets Managed By, Support, and Change groups directly; takes precedence over CI Class Manager settings (Priority 1 vs. Priority 2)

## Governance and Verification

Since these fields cannot be verified automatically, [[ServiceNow]] provides two Data Manager policy types for ongoing validation:

- **Certification Policies** — periodically verify that non-discoverable attributes (owner, support group, change group) contain correct values. Distinct from [[CMDBHealth|CMDB Health]] Desired State audits, which only check that the fields are populated (not whether the values are right).
- **Attestation Policies** — verify the physical existence of IT infrastructure and applications through manual checklist-based tasks on a defined schedule.

Both policy types generate tasks assigned to the CI's Managed By Group.

## Completeness Scorecard Integration

The [[CMDBHealth|CMDB Health Dashboard]] Completeness Scorecard tracks non-discoverable fields as **Recommended** (not Required) to avoid breaking discovery jobs. Making non-discoverable fields required can cause integrations and discovery tools to fail when creating CIs, since they cannot populate these values.

## Importance

Groups are essential when incidents are opened against CIs or when changes need to be made. After automated discovery populates [[DiscoverableData|discoverable data]], supplementing non-discoverable group and location data is a critical next step that is often forgotten.

## Sources

- [[ingest-data-into-the-cmdb|Ingest Data into the CMDB]] — non-discoverable data types and population methods
- [[govern-the-cmdb|Govern the CMDB]] — certification, attestation, and completeness scorecard integration

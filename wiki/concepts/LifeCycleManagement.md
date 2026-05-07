---
title: "Life Cycle Management"
type: concept
tags: [ServiceNow, CMDB, governance, lifecycle, data-quality]
sources: [govern-the-cmdb]
last_updated: 2026-05-07
---

# Life Cycle Management

Life Cycle Management in [[ServiceNow]] [[CMDB]] covers the end-to-end management of configuration items through operational, retired, archived, and deleted stages. It is implemented through the CMDB Data Manager — a policy-driven framework for bulk CI lifecycle operations — and the [[CSDM]] life cycle field model.

## Lifecycle Stages

CIs progress through an ordered end-of-life sequence:

1. **Retire** — CI is no longer in use; marked as end-of-life but still present in the CMDB
2. **Archive** — CI is removed from active use but retained for historical/compliance reasons
3. **Delete** — CI is permanently removed per data retention policies

A CI must be retired (in an end-of-life stage) before it can be archived or deleted.

## Data Manager Policies

CMDB Data Manager provides five policy types for automated lifecycle governance:

- **Retire Policy** — e.g., "retire all computers without owners created more than a year ago"
- **Archive Policy** — e.g., "archive all Linux servers in Seattle DC not updated for 6 months"
- **Delete Policy** — e.g., "delete all containers not discovered in the past week"
- **Attestation Policy** — verifies the physical existence of IT infrastructure; generates tasks for periodic manual verification
- **Certification Policy** — verifies non-discoverable attributes (owner, support group, change group) are correct; distinct from CMDB Health Desired State audits which check that these fields are populated, not that the values are correct

### Prerequisites

- **Life Cycle Mappings** must be reviewed and activated — the `life_cycle_mapping` table maps legacy status values to CSDM life cycle values
- **Managed By Group** should be populated on CIs for correct task assignment; use CI Class Manager or technology management offerings to auto-populate
- Some policy types (Retire, Archive, Delete) require an active life cycle rule for each targeted class

### Roles

- `data_manager_admin` — full access to create and manage policies
- `data_manager_user` — limited access

### Legacy vs. New Data Manager

The legacy Data Manager (navigated via **Configuration > CMDB Data Manager**) is deprecated as of the Yokohama release. The new Data Manager, built on UI Builder and accessible from CMDB Workspace, uses a workflow-based interface. Policies created in the legacy tool are compatible with the new one.

## CSDM Life Cycle Fields

CSDM introduced standardized lifecycle fields to replace multiple legacy status fields:

### Legacy CI Status Fields
- Operational status
- Install Status
- Hardware Status
- Substatus

### Legacy Asset Status Fields
- State
- Substate

### New CSDM Fields (CI and Asset)
- **Life Cycle Stage** — the lifecycle phase (e.g., Operational, Retired, Archived)
- **Life Cycle Stage Status** — the detailed status within a stage

It is not recommended to manage all legacy fields simultaneously — choose between Install Status and Hardware Status, not both.

## CI-Asset Synchronization

CI and Asset records automatically synchronize in both directions:

- **Shared fields** — Asset tag, Department, Location, Support Group, Company, Serial Number, Model ID, Assigned to
- **Legacy field sync** — Asset `State` ↔ CI `Install Status`; Asset `Substate` ↔ CI `Substatus` (CI `Hardware Status` is NOT synced)
- **CSDM field sync** — Life Cycle Stage and Life Cycle Stage Status sync directly between CI and Asset, plus with the asset's install base item (IBI)

The `Asset CI Field Mappings` table tracks all synchronized fields and can be customized.

## Sources

- [[govern-the-cmdb|Govern the CMDB]] — full lifecycle management and Data Manager coverage

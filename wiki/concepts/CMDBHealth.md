---
title: "CMDB Health"
type: concept
tags: [ServiceNow, CMDB, governance, data-quality]
sources: [govern-the-cmdb]
last_updated: 2026-05-07
---

# CMDB Health

CMDB Health is a measurable framework in [[ServiceNow]] for assessing and maintaining the quality of [[CMDB]] data across three dimensions: Completeness, Compliance, and Correctness. The CMDB Health Dashboard is the primary visualization and management tool, with scheduled jobs that calculate metrics and generate remediation tasks.

## Three Scorecards

### Completeness

Measures whether CIs have all essential data populated. Composed of two metrics:

- **Required fields** — marked as mandatory in the system dictionary. Enforced at the database level — records cannot be created without them. Should be used sparingly, as missing required fields can cause discovery jobs or imports to fail. Examples: Serial Number, Name, MAC Address.
- **Recommended fields** — marked via CI Class Manager for visibility only. No enforcement — records can be created without them. Safe starting point for tracking data gaps without disruption. Examples: Support Group, Change Group, Managed By Group, Location.

The system property `glide.required_attribute.enabled` (default: `true`) enforces mandatory fields. Setting it to `false` or configuring the IRE property *Enforce the rule that required entities cannot be identified and reconciled* can override this for integrations.

### Compliance

Validates that CIs conform to established standards via Desired State audits. Each audit requires three components:

1. **Certification Filter** — defines the scope (e.g., "all UNIX servers in a datacenter")
2. **Certification Template** — defines expected conditions on attributes, relationships, and reference fields
3. **Audit** — executes the filter against the template; can auto-create follow-on remediation tasks

Two audit types feed the Compliance scorecard: Desired State audits (template-based) and Scripted Audits (script-based for conditions too complex for templates). Distinguish from Data Manager **certification policies**, which are for manually verifying non-discoverable attributes (owner, support group) on a schedule.

### Correctness

Validates that CMDB data is accurate and reflects reality. Three metrics:

- **Duplicate** — CIs matching the same identification rules. Measured as the percentage of duplicate CIs. The oldest CI (by creation date) is treated as the non-duplicate; newer ones are flagged via the *Duplicate Of* field. Only independent CIs (non-application, e.g., hardware) are evaluated.
- **Orphan** — CIs missing required relationships. No base system orphan rules exist; admins must define rules per class (e.g., "Application must have Runs on relationship to a Server"). One orphan rule allowed per class.
- **Stale** — CIs not updated within a configurable period. Base system: one rule at `cmdb_ci` level with a 60-day threshold, determined by `sys_updated_on`. Additional class-level rules can be added for different discovery cadences (e.g., network devices scanned every 14 days might use a 21-day threshold).

The overall Correctness score reflects the percentage of CIs passing **all defined metrics** — not an average of individual metric scores.

## Health Inclusion Rules

Configuration settings that scope which CI classes contribute to health metrics. Key capabilities:

- Selective class tracking (e.g., exclude classes the org isn't accountable for)
- Per-metric granularity (e.g., apply to Correctness but not Completeness)
- Operator-based rules (e.g., "is a" to include all Hardware subclasses)
- CMDB Group Health Dashboard provides aggregated views filtered by group

## Remediation Workflows

The health dashboard can auto-generate remediation tasks when CIs fail health tests. The flow:

1. **Enable Task** — configure the health metric to generate remediation tasks
2. **Workflow** — build Flow Designer workflow for the remediation action
3. **CMDB Remediation Rule** — link the workflow to a remediation rule
4. **Remediation Task** — execute the workflow from the generated task

De-duplication tasks and compliance audit tasks follow different paths (IRR generates dedup tasks automatically; audit tasks are configured through Compliance Manager).

## Scheduled Jobs

Three jobs power the health dashboard (none active by default):
- CMDB Health Dashboard - Completeness Score Calculation
- CMDB Health Dashboard - Compliance Score Calculation
- CMDB Health Dashboard - Correctness Score Calculation (also handles staleness, orphan, and duplicate detection)

Jobs should run under an admin user; non-admin users may produce inaccurate results due to ACL restrictions.

## Sources

- [[govern-the-cmdb|Govern the CMDB]] — full health dashboard and governance framework

---
title: "Govern the CMDB"
type: source
tags: [ServiceNow, CMDB, governance, health, lifecycle, reclassification]
date: 2026-05-07
source_file: raw/articles/Govern the CMDB.md
---

## Summary

Comprehensive ServiceNow training module covering CMDB governance tools and practices. Covers the CMDB Health Dashboard with its three scorecards (Completeness, Compliance, Correctness), duplicate CI management via IRE and de-duplication workflows, CI reclassification mechanics and restriction rules, remediation capabilities with automated workflows, and full lifecycle management through Data Manager policies (retire, archive, delete, attest, certify). Also details the CSDM life cycle field model and CI-Asset synchronization.

## Key Claims

- CMDB Health Dashboard provides a measurable framework for CMDB quality across three dimensions: completeness (required/recommended fields), compliance (desired state audits), and correctness (duplicate/orphan/stale metrics)
- Health Inclusion Rules allow admins to scope health tracking to only those CI classes the organization is accountable for
- The Completeness Scorecard tracks Required fields (mandatory, enforced at dictionary level) and Recommended fields (visibility-only, no enforcement) — starting with Recommended is safer to avoid breaking discovery jobs
- The Compliance Scorecard uses Desired State audits (template-based or scripted) to verify CIs match expected configurations; distinct from Data Manager certification policies which verify non-discoverable attributes manually
- The Correctness Scorecard tracks Duplicate CIs (via IRE identification rules), Orphan CIs (missing required relationships), and Stale CIs (not updated within a configurable time window)
- IRE determines duplicates when 2+ CIs match identification rules; the oldest CI by creation date is treated as the non-duplicate
- De-duplication tasks can be resolved one-by-one via the Duplicate CI Remediator wizard or in bulk via De-Duplication Templates with pre-configured merge/delete rules
- CI reclassification (upgrade, downgrade, switch) is automatic by default but can cause data loss during downgrade/switch; restriction rules provide class-level granularity beyond global properties
- Remediation workflows can auto-generate tasks for failing health metrics and execute automated remediation (e.g., re-discovering stale CIs)
- Data Manager provides policy-driven lifecycle management: Retire → Archive → Delete progression, plus Attestation (verify physical existence) and Certification (verify non-discoverable attributes)
- CSDM introduced Life Cycle Stage and Life Cycle Stage Status as standardized replacements for legacy fields (Operational status, Install Status, Hardware Status, State, Substate)
- CI and Asset records share fields and automatically synchronize lifecycle status in both directions

## Key Quotes

> "You can't manage what you can't measure." — Peter Drucker, cited in the CMDB Health section

> "Setting an attribute as required/mandatory can cause ServiceNow Discovery jobs or imports to fail."

> "If two or more CIs in the CMDB are duplicates and have a populated Discovery Source field, the CMDB Health Dashboard Correctness scorecard will not flag them as duplicates."

> "When automatic CI reclassification is enabled (which is the default), be aware that CI class downgrade and CI class switch operations can lead to data loss."

## Connections

- [[CMDB]] — governance is the third pillar after configuration and ingestion
- [[CMDBHealth]] — the full health dashboard framework
- [[IRE]] — central to duplicate detection and CI reclassification
- [[CSDM]] — provides lifecycle stage standards and foundation data model
- [[LifeCycleManagement]] — policy-driven retire/archive/delete/attest/certify framework
- [[NonDiscoverableData]] — certification and attestation policies verify these fields
- [[ServiceNow]] — platform providing all governance tools

## Contradictions

- None identified with existing wiki content. This source extends prior CMDB and IRE coverage into governance and lifecycle management, filling a gap rather than contradicting.

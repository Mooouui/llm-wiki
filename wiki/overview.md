---
title: "Overview"
type: synthesis
tags: []
sources: [llm-wiki-complete-guide, configure-the-cmdb, ingest-data-into-the-cmdb, govern-the-cmdb]
last_updated: 2026-05-07
---

# Overview

*This page is maintained by the LLM. It is updated on every ingest to reflect the current synthesis across all sources.*

## What is LLM Wiki?

LLM Wiki is a pattern (not a product) proposed by [[AndrejKarpathy|Andrej Karpathy]] in April 2026 for building personal knowledge bases where an LLM agent continuously writes, links, and maintains structured Markdown files. It inverts the traditional [[RAG]] paradigm: instead of re-processing sources on every query, sources are "compiled" once at ingestion time into a persistent, compounding wiki.

## The Architecture

Three layers of pure text — no vector databases needed at small-to-medium scale:

1. **Raw Sources** (`raw/`) — immutable originals; LLM reads but never modifies
2. **The Wiki** (`wiki/`) — LLM-generated and maintained; humans read, LLM writes
3. **The Schema** (`CLAUDE.md`) — control protocol defining how the LLM maintains the wiki

Two index files (`index.md` for spatial navigation, `log.md` for temporal tracking) serve as the navigation backbone.

## Core Operations

- **Ingest**: Add a source → LLM creates summary, updates entities/concepts, builds cross-links
- **Query**: Ask a question → LLM searches wiki, synthesizes with citations, optionally archives answer
- **Lint**: Health check → detect orphans, broken links, contradictions, stale content, gaps

## Key Tension: Automation vs. Understanding

The deepest critique comes from [[ExtendedBrain|Extended Brain]], drawing on [[NiklasLuhmann|Niklas Luhmann]]'s [[Zettelkasten]] and the concept of [[Hormesis|cognitive friction]]. The argument: LLM Wiki produces excellent maps, but the user never walks the territory. The struggle of expressing ideas in your own words — when language breaks down and reveals understanding gaps — is not a bug but the mechanism of learning itself.

The recommended hybrid: use LLM for scaffolding (linking, indexing, gap-finding), but keep synthesis in your own hands.

## CMDB & Configuration Management

The wiki also covers enterprise IT configuration management through the lens of [[ServiceNow]]'s [[CMDB]] platform. Three phases form a complete lifecycle:

1. **Configuration** — CI Class Manager, IRE, reconciliation rules, Multisource CMDB
2. **Ingestion** — Discovery, Service Mapping, ACC, Service Graph Connectors, IntegrationHub ETL
3. **Governance** — Health monitoring, duplicate remediation, reclassification, lifecycle management

### Data Ingestion Ecosystem

ServiceNow provides a layered ingestion toolkit, each method suited to different environments:

- [[ServiceNowDiscovery|Discovery]] (horizontal/agentless) — scheduled network scanning via the [[MIDServer]] using WMI, SSH, and SNMP probes
- [[ServiceMapping|Service Mapping]] (top-down) — discovers and models application service dependencies, aligned with [[CSDM]]
- [[AgentClientCollector|ACC]] (agent-based) — real-time discovery with software utilization data for SAM
- [[ServiceGraphConnectors]] — pre-built integrations (AWS, Azure, SCCM, Jamf) routing through [[IRE]]
- [[IntegrationHubETL]] — modern ETL interface replacing legacy Import Sets, with the Robust Transform Engine feeding IRE payloads

### Data Integrity Layer

The [[IRE|Identification & Reconciliation Engine]] acts as a gatekeeper — no source writes directly to the CMDB. It handles identification (unique CI matching), reconciliation (authoritative source selection), deduplication, and reclassification. For deeper auditability, [[MultisourceCMDB|CMDB 360]] retains every proposed value from every source — including rejected ones.

### Governance Layer

Once data is ingested, maintaining quality requires active governance. The [[CMDBHealth|CMDB Health Dashboard]] measures data quality across three dimensions:

- **Completeness** — are required and recommended fields populated?
- **Compliance** — do CIs match desired state configurations via audits?
- **Correctness** — are there duplicates, orphans, or stale CIs?

The health dashboard generates remediation tasks that can trigger automated workflows — e.g., re-discovering a stale CI. [[LifeCycleManagement|Life Cycle Management]] via Data Manager policies governs end-of-life for CIs (retire → archive → delete) and periodic attestation/certification of non-discoverable attributes. CI reclassification (upgrade/downgrade/switch) is handled by IRE with class-level restriction rules to prevent data loss.

### The Human Layer: Non-Discoverable Data

Automation handles ~90% of data: hardware, software, network details ([[DiscoverableData]]). But critical governance attributes — support group, change group, managed by group — are [[NonDiscoverableData|non-discoverable]] and must be manually populated via CI Class Manager or technology management offerings within the [[CSDM]] framework. These group assignments drive incident routing, change routing, and Data Manager certification/attestation policies.

## Historical Lineage

[[VannevarBush|Vannevar Bush]]'s 1945 [[Memex]] envisioned a personal knowledge machine with associative trails. His unsolved problem — who does the maintenance? — is answered by LLMs. The web became public and chaotic; LLM Wiki returns to Bush's original vision of private, curated knowledge.

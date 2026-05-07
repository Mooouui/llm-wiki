# Wiki Index

This file is maintained by the LLM. Updated on every ingest.

## Overview
- [Overview](overview.md) — living synthesis across all sources

## Sources
- [LLM Wiki：让大模型替你打理知识库的完整指南](sources/llm-wiki-complete-guide.md) — comprehensive guide to Karpathy's LLM Wiki concept, architecture, and critique
- [Configure the CMDB](sources/configure-the-cmdb.md) — ServiceNow CMDB configuration: CI Class Manager, IRE, reconciliation, Multisource CMDB
- [Ingest Data into the CMDB](sources/ingest-data-into-the-cmdb.md) — ServiceNow data ingestion: Discovery, Service Mapping, ACC, Service Graph Connectors, IntegrationHub ETL
- [Govern the CMDB](sources/govern-the-cmdb.md) — CMDB governance: Health Dashboard, duplicate remediation, reclassification, lifecycle management, Data Manager

## Entities
- [Andrej Karpathy](entities/AndrejKarpathy.md) — AI researcher, originated LLM Wiki concept (April 2026)
- [Niklas Luhmann](entities/NiklasLuhmann.md) — German sociologist, Zettelkasten method creator (90K cards)
- [Vannevar Bush](entities/VannevarBush.md) — 1945 Memex visionary
- [Tobi Lutke](entities/TobiLutke.md) — Shopify CEO, developer of qmd search tool
- [Extended Brain](entities/ExtendedBrain.md) — publication offering deepest critique of LLM Wiki
- [Obsidian](entities/Obsidian.md) — Markdown editor serving as wiki frontend IDE
- [Claude Code](entities/ClaudeCode.md) — Anthropic CLI agent, primary wiki maintenance engine
- [NotebookLM](entities/NotebookLM.md) — Google's AI notebook product, contrasted with LLM Wiki
- [ServiceNow](entities/ServiceNow.md) — enterprise ITSM/ITOM platform providing CMDB and configuration management tooling
- [ServiceNow Discovery](entities/ServiceNowDiscovery.md) — agentless/horizontal IP-based network discovery
- [Service Mapping](entities/ServiceMapping.md) — top-down service dependency mapping and modeling
- [Agent Client Collector](entities/AgentClientCollector.md) — agent-based real-time discovery and monitoring
- [Service Graph Connectors](entities/ServiceGraphConnectors.md) — pre-built third-party integrations for CMDB population
- [IntegrationHub ETL](entities/IntegrationHubETL.md) — modern ETL interface for importing data into the CMDB
- [MID Server](entities/MIDServer.md) — secure bridge between ServiceNow and internal networks

## Concepts
- [LLM Wiki](concepts/LLMWiki.md) — pattern for LLM-maintained Markdown knowledge bases
- [RAG](concepts/RAG.md) — retrieval-augmented generation, the approach LLM Wiki supersedes
- [Zettelkasten](concepts/Zettelkasten.md) — slip-box method by Luhmann, historical contrast
- [Hormesis](concepts/Hormesis.md) — cognitive friction concept, critique of frictionless knowledge
- [Memex](concepts/Memex.md) — Bush's 1945 personal knowledge machine vision
- [Schema](concepts/Schema.md) — control protocol layer (CLAUDE.md/AGENTS.md)
- [CMDB](concepts/CMDB.md) — Configuration Management Database for IT asset tracking and governance
- [CMDB Health](concepts/CMDBHealth.md) — measurable framework for CMDB data quality across Completeness, Compliance, and Correctness scorecards
- [IRE](concepts/IRE.md) — Identification & Reconciliation Engine, ServiceNow's CMDB data integrity framework
- [Multisource CMDB](concepts/MultisourceCMDB.md) — CMDB 360 attribute-level data provenance and dynamic reconciliation
- [CSDM](concepts/CSDM.md) — Common Service Data Model, standardized service modeling and lifecycle framework
- [Life Cycle Management](concepts/LifeCycleManagement.md) — policy-driven CI lifecycle: retire, archive, delete, attest, certify
- [Discoverable Data](concepts/DiscoverableData.md) — hardware, software, network data that can be auto-collected
- [Non-Discoverable Data](concepts/NonDiscoverableData.md) — group, location data requiring manual population

## Syntheses
- [CI 配置完整流程](syntheses/ci-configuration-full-process.md) — 从零到治理的完整 CI 配置生命周期：Configuration → Ingestion → Governance
- [CMDB Governance 学习指南](syntheses/cmdb-governance-guide.md) — CMDB 治理完整学习指南：Health Dashboard、重复管理、生命周期、CSDM
- [LLM Wiki 最佳实践](syntheses/llm-wiki-best-practices.md) — 架构、摄入、查询、Lint、规模化、混合方案、工具配置
- [Reconciliation Rules Explained](syntheses/reconciliation-rules-explained.md) — 对账规则的作用、核心机制、静态与动态对比概览
- [Static vs. Dynamic Reconciliation](syntheses/static-vs-dynamic-reconciliation.md) — 静态与动态对账规则深度对比：机制、策略、适用场景
- [ServiceNow CMDB 数据摄入解决方案](syntheses/servicenow-discovery-solutions.md) — 六种数据摄入方案：Discovery、Service Mapping、ACC、Connectors、ETL、Import Sets
- [ACC 与 Service Graph Connectors](syntheses/acc-and-service-graph-connectors.md) — ACC 与 Service Graph Connectors 的详细对比和架构定位
- [支持第三方导入的方案](syntheses/third-party-data-import-solutions.md) — 哪些方案支持从第三方系统导入数据

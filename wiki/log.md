# Wiki Log

Append-only chronological record of all operations.

Format: `## [YYYY-MM-DD] <operation> | <title>`

## [2026-05-07] query | CMDB Governance 学习指南

## [2026-05-07] query | CI 配置完整流程

Parse recent entries: `grep "^## \[" wiki/log.md | tail -10`

---

## [2026-04-09] ingest | LLM Wiki：让大模型替你打理知识库的完整指南
- Source: `raw/articles/LLM Wiki：让大模型替你打理知识库的完整指南.md`
- Created: 1 source page, 8 entity pages, 6 concept pages
- Updated: index.md, overview.md
- First wiki ingest

## [2026-04-22] ingest | Configure the CMDB
- Source: `raw/articles/Configure the CMDB.md`
- Created: 1 source page, 1 entity page (ServiceNow), 3 concept pages (CMDB, IRE, MultisourceCMDB)
- Updated: index.md, overview.md
- New domain: enterprise IT configuration management

## [2026-04-27] ingest | Ingest Data into the CMDB
- Source: `raw/articles/Ingest Data into the CMDB.md`
- Created: 1 source page, 6 entity pages (ServiceNowDiscovery, ServiceMapping, AgentClientCollector, ServiceGraphConnectors, IntegrationHubETL, MIDServer), 3 concept pages (CSDM, DiscoverableData, NonDiscoverableData)
- Updated: index.md, overview.md, ServiceNow.md, IRE.md, CMDB.md
- Expands CMDB domain with full ingestion ecosystem: six methods from Discovery to IntegrationHub ETL, plus foundation data population via CSDM framework

## [2026-04-27] query | ServiceNow CMDB 数据摄入解决方案
- Question: "servicenow discovery 有哪些solution"
- Filed: `wiki/syntheses/servicenow-discovery-solutions.md`
- Covers all six ingestion methods with selection guide

## [2026-04-27] query | ACC 与 Service Graph Connectors + 三方导入方案
- Questions: "详细介绍一下ACC 和 service graph connectors" + "哪些solution支持三方导入"
- Filed: `wiki/syntheses/acc-and-service-graph-connectors.md`, `wiki/syntheses/third-party-data-import-solutions.md`
- Detailed ACC vs Discovery comparison, Service Graph Connectors architecture, and third-party import classification

## [2026-05-07] ingest | Govern the CMDB
- Source: `raw/articles/Govern the CMDB.md`
- Created: 1 source page, 2 concept pages (CMDBHealth, LifeCycleManagement)
- Updated: index.md, overview.md, CMDB.md, IRE.md, CSDM.md, ServiceNow.md, NonDiscoverableData.md
- Adds full governance dimension: CMDB Health Dashboard (3 scorecards), duplicate remediation, CI reclassification/restriction rules, remediation workflows, lifecycle management via Data Manager, CSDM life cycle fields and CI-Asset sync

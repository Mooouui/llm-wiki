---
title: "支持第三方数据导入的 ServiceNow 方案"
type: synthesis
tags: [ServiceNow, CMDB, integration, ServiceGraphConnectors, IntegrationHubETL, ImportSets]
sources: [ingest-data-into-the-cmdb]
last_updated: 2026-04-27
---

# 支持第三方数据导入的 ServiceNow 方案

ServiceNow 六种 CMDB 数据摄入方案中，支持从**第三方系统导入数据**的有 3 个：

## 专门做三方导入的方案

**1. [[ServiceGraphConnectors]]** — 预置连接器，开箱即用同步 AWS、Azure、SCCM、Intune、Jamf 等第三方平台数据。底层走 [[IntegrationHubETL]] → [[IRE]] 管道。

**2. [[IntegrationHubETL]]** — 通用 ETL 框架，可以对接任意第三方数据源（数据库、API、文件），自定义 Transform Map 做字段映射和规范化。是旧版 Import Sets 的现代替代品。

**3. Import Sets & Transform Maps** — 遗留方案，从 CSV、Excel、数据库或 API 提取数据暂存到 Staging Table，再通过 Transform Map 写入 CMDB。仍可用，但 ServiceNow 推荐迁移到 IntegrationHub ETL。

## 不做三方导入（ServiceNow 原生发现）

- [[ServiceNowDiscovery|Discovery]] — ServiceNow 自己的网络扫描引擎
- [[ServiceMapping|Service Mapping]] — ServiceNow 自己的服务依赖建模
- [[AgentClientCollector|ACC]] — ServiceNow 自己的端点代理

这三者都是 ServiceNow 自己去"发现"数据，而非从第三方系统同步已有数据。

## 简单记忆

**Connectors 是预置的三方桥，ETL 是自建的三方桥，Import Sets 是老的三方桥**。三者都最终汇入 [[IRE]]。

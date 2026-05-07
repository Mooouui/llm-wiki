---
title: "ServiceNow CMDB 数据摄入解决方案总览"
type: synthesis
tags: [ServiceNow, CMDB, Discovery, ServiceMapping, ACC, IntegrationHubETL, ServiceGraphConnectors]
sources: [ingest-data-into-the-cmdb]
last_updated: 2026-04-27
---

# ServiceNow CMDB 数据摄入解决方案总览

ServiceNow 提供了 **6 种**将数据导入 [[CMDB]] 的方案，按自动化程度和适用场景分为不同层级，所有方案的数据最终都经过 [[IRE|IRE（识别与对账引擎）]]处理，以防止重复和不一致。

## 1. [[ServiceNowDiscovery|ServiceNow Discovery（水平发现）]]

**无代理 · 计划性 · IP 扫描**

- 通过 [[MIDServer]] 以 WMI（Windows）、SSH（Unix/Linux）、SNMP（网络设备）探测目标，无需安装永久软件
- 四个阶段：Scan（端口扫描）→ Classification（设备分类）→ Identification（唯一标识）→ Exploration（深度采集）
- **非实时**，按计划调度执行；建议初始使用小范围 IP，最大不超过 /16（65,000 个 IP）
- 又称：Horizontal Discovery、Agentless Discovery、IP-based Discovery

## 2. [[ServiceMapping|Service Mapping（顶级发现）]]

**自上而下 · 服务建模 · 动态更新**

- 从业务服务出发，向下映射到支撑该服务的所有基础设施和应用依赖关系
- 自动构建 Application Service（`cmdb_ci_service_auto`），可按环境（Dev/Test/Prod）、地区（AMS/EMEA/APJ）、业务线（HR/Marketing）划分
- 与 [[CSDM|CSDM（通用服务数据模型）]]对齐，填补 IT 运维与业务用户之间的鸿沟
- 又称：Top-down Discovery、Tag-based Discovery、ML-powered Mapping

## 3. [[AgentClientCollector|Agent Client Collector (ACC)]]

**有代理 · 实时 · 软件使用率**

- 需要在每个目标主机上安装轻量代理，提供**实时**可见性
- 唯一能采集**软件使用率数据**的方案，支撑软件资产管理（SAM）
- 适用场景：间歇联网的工作站、安全策略禁止外部发现方案访问的网络
- 与 [[ServiceNowDiscovery|Discovery]] 的关键区别：Discovery 是计划性的、无代理的；ACC 是实时的、有代理的

## 4. [[ServiceGraphConnectors|Service Graph Connectors]]

**预置集成 · 开箱即用 · CSDM 合规**

- 覆盖七大类第三方系统：云平台（AWS、Azure）、端点管理（SCCM、Intune、Jamf）、监控工具、安全方案、OT 应用等
- 每个连接器都经过 [[CSDM]] 合规审核，底层使用 [[IntegrationHubETL]] 的 Transform Map
- 需要 ITOM Visibility 许可（SCCM 除外）

## 5. [[IntegrationHubETL|IntegrationHub ETL]]

**现代 ETL · 可视化映射 · 替代旧方案**

- ServiceNow Store 应用，提供友好的引导式界面，是旧版 Import Sets 的**推荐替代方案**
- 双引擎架构：**RTE（鲁棒转换引擎）**将源数据转换为 IRE 负载 → [[IRE]] 执行对账和去重
- 支持先用小样本数据测试、审查、回滚，满意后再上线
- 额外支持非 CMDB 表：Location、Department、Cost Center、Building、User、Group

## 6. Import Sets & Transform Maps（旧版）

**遗留方案 · 仍可用但不推荐**

- ServiceNow 最早的数据导入方式，通过 Import Set 暂存数据，Transform Map 定义字段映射，支持 Transform Script 处理复杂逻辑
- 无需额外付费许可，从 System Import Sets 应用即可访问
- 已被 [[IntegrationHubETL]] 取代，后者提供了更现代化的界面和原生 IRE 集成

## 补充：非可发现数据的填充

自动化工具采集的是 [[DiscoverableData|可发现数据]]（硬件、软件、网络、云资源），约占 CMDB 数据的 90%。但关键的治理属性——Support Group、Change Group、Managed By Group——属于 [[NonDiscoverableData|非可发现数据]]，需要通过以下两种方式手动填充：

1. **CI Class Manager** — 按 CI 类别设置 Managed By Group（优先级 2）
2. **Technology Management Offerings** — 同时设置 Support、Change、Managed By Group（优先级 1，覆盖 CI Class Manager 的设置）

## 方案选择速览

| 方案 | 模式 | 实时性 | 适用场景 |
|---|---|---|---|
| [[ServiceNowDiscovery\|Discovery]] | 无代理扫描 | 计划性 | 全网设备和应用发现 |
| [[ServiceMapping\|Service Mapping]] | 自上而下 | 动态更新 | 业务服务依赖建模 |
| [[AgentClientCollector\|ACC]] | 有代理 | 实时 | 端点监控、SAM、安全受限网络 |
| [[ServiceGraphConnectors]] | 预置集成 | 按计划 | 第三方工具数据同步 |
| [[IntegrationHubETL]] | ETL 映射 | 按计划 | 自定义数据源导入 |

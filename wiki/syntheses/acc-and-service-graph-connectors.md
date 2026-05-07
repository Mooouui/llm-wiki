---
title: "ACC 与 Service Graph Connectors 详细介绍"
type: synthesis
tags: [ServiceNow, CMDB, ACC, ServiceGraphConnectors, IRE, CSDM]
sources: [ingest-data-into-the-cmdb]
last_updated: 2026-04-27
---

# ACC 与 Service Graph Connectors 详细介绍

## [[AgentClientCollector|Agent Client Collector (ACC)]]

### 定位

ACC 是 [[ServiceNow]] ITOM 套件中的**有代理、实时**发现方案。与 [[ServiceNowDiscovery|Discovery]] 的无代理、计划性扫描形成互补——Discovery 回答"网络里有什么"，ACC 回答"每个端点现在是什么状态"。

### 核心特征

**实时性**：不同于 Discovery 的按计划调度，ACC 通过安装在各主机上的轻量代理提供持续可见性，能第一时间感知配置变更。

**软件使用率采集**：这是 ACC 独有的能力——无代理方案无法获知软件是否真的被使用。ACC 能采集软件的实际使用指标，直接支撑 Software Asset Management（SAM）用例，帮组织优化软件许可成本。

**安全受限场景**：两类场景下 ACC 几乎是唯一选择：

- **间歇联网设备** — 员工笔记本电脑、移动工作站等不常在线的主机，Discovery 的计划扫描窗口可能永远碰不到它们
- **安全隔离网络** — 安全团队不允许外部发现方案（如 MID Server）远程连接的网络，只能通过在内部安装 ACC 代理来采集数据

### 覆盖的 ITOM 用例

ACC 作为 ServiceNow 的统一代理，一个代理支撑多个场景：Visibility & Monitoring、Software Asset Management、Security Incident Response、Service Management 等。

### 与 Discovery 的关键区别

| | [[ServiceNowDiscovery\|Discovery]] | [[AgentClientCollector\|ACC]] |
|---|---|---|
| 代理 | 无 | 有（需安装） |
| 实时性 | 计划性 | 实时 |
| 软件使用率 | 不支持 | 支持 |
| 网络要求 | MID Server 可达 | 出站互联网即可 |

## [[ServiceGraphConnectors|Service Graph Connectors]]

### 定位

Service Graph Connectors 是 ServiceNow 提供的**预置集成方案**，用于从第三方系统导入和同步数据到 [[CMDB]]。它不是自己去"发现"数据，而是从已有的外部管理工具中拉取数据并规范化。ServiceNow 将其定位为"获取全运维资产可见性的最快方式"。

### 连接器分类（七大类）

1. **云平台** — AWS、Azure 等
2. **端点/IT 资产管理** — SCCM、Intune、Jamf
3. **监控与可观测性** — 各类 APM 和监控工具
4. **安全方案** — 安全扫描器、漏洞管理平台
5. **软件/服务器/网络应用** — 网络管理、数据中心工具
6. **OT 应用** — 运营技术（Operational Technology）系统
7. **合作伙伴自建** — 第三方按规范自行开发的连接器

### 三条设计原则

**IRE 原生**：所有连接器的数据都通过 [[IRE]] 处理——不会有连接器绕过 IRE 直接写 CMDB。

**CSDM 合规**：每个连接器都经过了 [[CSDM|CSDM（通用服务数据模型）]] 合规审查，确保导入的数据结构和关系符合 CSDM 规范。

**基于 IntegrationHub ETL**：连接器底层使用 [[IntegrationHubETL]] 的 Transform Map 机制。CMDB 管理员可以直接在 IntegrationHub ETL 界面中查看和调整字段映射。

### 许可

需要 ITOM Visibility 许可才能使用（SCCM 连接器除外）。

## 两者在架构中的位置

```
外部系统（AWS/SCCM/Jamf/...）
        │
        ▼
Service Graph Connectors ──→ IntegrationHub ETL (RTE + Transform Map)
        │                              │
        │                              ▼
        │                          IRE (识别/对账/去重)
        │                              │
        ▼                              ▼
           CMDB（系统记录）
```

ACC 和 Service Graph Connectors 是互补关系：ACC 直接采集端点实时数据（"一手数据"），Connectors 从已有管理系统同步数据（"二手数据"，经过外部系统治理）。两者数据都经 [[IRE]] 汇入 CMDB，IRE 通过 Reconciliation Rules 决定属性级别的数据源优先级。

## 非可发现数据的填充

自动化采集的都是 [[DiscoverableData|可发现数据]]。Critical 的治理字段——Support Group、Change Group、Managed By Group——属于 [[NonDiscoverableData|非可发现数据]]，需通过 CI Class Manager 或 Technology Management Offerings 手动填充。

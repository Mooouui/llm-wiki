---
title: "CI 配置完整流程"
type: synthesis
tags: [CMDB, ServiceNow, CI, configuration, ingestion, governance, IRE]
sources: [configure-the-cmdb, ingest-data-into-the-cmdb, govern-the-cmdb]
last_updated: 2026-05-07
---

# 配置一个 CI 的完整流程 — 从零到治理

配置一个 CI（Configuration Item）不是一个单步操作，而是跨三个阶段的完整生命周期。

## 三阶段总览

```
┌──────────────┐      ┌──────────────┐      ┌──────────────┐
│  Phase 1      │ ──▶ │  Phase 2      │ ──▶ │  Phase 3      │
│  Configuration│      │  Ingestion    │      │  Governance   │
│  设计模型     │      │  填入数据     │      │  长期维护     │
└──────────────┘      └──────────────┘      └──────────────┘
```

---

## Phase 1：Configuration（配置阶段）— "这个 CI 长什么样？谁来管？"

### Step 1.1：确定 CI 类（Class）

所有 CI 在 [[CMDB]] 中按层级分类，根类是 `cmdb_ci`。核心原则：**优先扩展现有类，不要轻易新建。** 新建 CI 类需要 `sn_cmdb_admin` + `personalize_dictionary`（或 `admin`）角色，且会带来许可、治理和互操作性问题。如果确实需要新类，建议先安装 **CMDB CI Class Models** Store 应用获取行业标准模板。

操作入口：[[ServiceNow|CI Class Manager]]，提供树状视图集中管理类层级、identification rules、reconciliation rules 和 health 设置。

### Step 1.2：定义 Identification Rules（识别规则）

这是配置 CI 最关键的一步。[[IRE|IRE]] 使用 identification rules 来判断一条新数据是创建新 CI 还是更新已有 CI。

规则设计原则：
- 使用稳定、唯一的属性 — 如 Serial Number、Host Name、MAC Address、Install Directory
- 绝不使用会变化的属性 — 如 IP Address（动态分配）、CPU 型号（会升级）

错误的识别规则会导致两种问题：

| 问题 | 原因 | 后果 |
|------|------|------|
| Duplicate CI（重复 CI） | 规则不够精确，同一实体被识别为新 CI | 同一个服务器出现多次 |
| Overloaded CI（过载 CI） | 规则过于宽泛，不同实体被误判为同一个 CI | 多个不同的服务器被合并成一个 |

### Step 1.3：配置 Reconciliation Rules（对账规则）

当多个数据源同时向 CMDB 写入数据时，reconciliation rules 决定谁的值算数。ServiceNow 不提供任何默认对账规则——必须自行配置。

**Static Reconciliation Rules（静态对账规则）**：按数据源优先级排序。例如 Discovery（优先级 1） > SCCM（优先级 2） > REST API（优先级 3）。Data Refresh Rule 是静态规则的补充：如果高优先级源在配置的时间窗口内没有更新某个 CI 类，临时允许低优先级源接管。

**Dynamic Reconciliation Rules（动态对账规则）**：不盲目信任某个数据源，而是根据 [[MultisourceCMDB|CMDB 360]] 保存的历史数据，按策略选值。五种策略：First Reported、Most Reported、Last Reported、Largest Value、Smallest Value。前提是必须开启 CMDB 360。优先级关系：动态规则 > 静态规则。

配置得当的对账规则可以自动化处理 90% 的数据源权威性决策。

### Step 1.4：配置 CMDB 360 / Multisource CMDB

[[MultisourceCMDB|CMDB 360]]（Paris 版本引入）在属性级别追踪所有数据源的历史值——包括被对账规则拒绝的值。核心价值：审计追溯、支撑动态对账、修改规则后可重新计算已有数据。

---

## Phase 2：Ingestion（摄入阶段）— "数据怎么进来？"

所有摄入方案的数据最终都经过 [[IRE]] 处理。ServiceNow 提供 6 种摄入方式：

### 自动摄入方案

| 方案 | 模式 | 实时性 | 典型场景 |
|------|------|--------|----------|
| [[ServiceNowDiscovery]] | 无代理 IP 扫描 | 计划性 | 全网设备发现 |
| [[ServiceMapping|Service Mapping]] | 自上而下服务建模 | 动态更新 | 业务服务依赖映射 |
| [[AgentClientCollector\|ACC]] | 有代理 | 实时 | 端点监控、SAM |
| [[ServiceGraphConnectors]] | 预置第三方集成 | 按计划 | AWS/Azure/SCCM/Jamf |
| [[IntegrationHubETL]] | 现代 ETL | 按计划 | 自定义数据源导入 |

### IntegrationHub ETL 详细流程

源数据 → Staging Table → Robust Transform Engine（RTE）→ IRE Payload → IRE APIs → CMDB 写入。支持小样本测试 → 审查 → 回滚 → 再上线。

### 自动 vs 手动数据

- [[DiscoverableData|可发现数据]]（90%）：硬件、软件、网络、云资源 → 自动采集
- [[NonDiscoverableData|非可发现数据]]（10%）：Support Group、Change Group、Managed By Group → 手动填充

填充非可发现数据的两种方式：CI Class Manager（优先级 2）和 Technology Management Offerings（优先级 1，覆盖前者）。

---

## Phase 3：Governance（治理阶段）— "数据长期可信吗？"

### CMDB Health Dashboard

[[CMDBHealth|CMDB Health Dashboard]] 通过三个计分卡持续监控：

- **Completeness（完整性）**：Required 字段（强制）和 Recommended 字段（仅标记）
- **Compliance（合规性）**：通过 Desired State Audit 验证 CI 是否符合预期配置
- **Correctness（正确性）**：Duplicate（重复）、Orphan（孤儿，缺少必要关系）、Stale（陈旧，默认 60 天未更新）

通过 Health Inclusion Rules 精选哪些 CI 类参与度量。

### 重复 CI 处理

三种方式：Duplicate CI Remediator（逐条 wizard）、De-Duplication Templates（批量、可调度）、Now Assist for CMDB（AI 驱动）。

### CI Reclassification（重分类）

- Upgrade：安全，无数据丢失
- Downgrade / Switch：可能导致数据丢失

通过 Reclassification Restriction Rules 实现类级别的精细控制。

### Life Cycle Management

[[LifeCycleManagement|CMDB Data Manager]] 单向流程：Retire → Archive → Delete。五种策略：Retire、Archive、Delete、Attestation（验证物理存在）、Certification（验证非可发现属性正确性）。

### CSDM 生命周期字段

[[CSDM]] 用 Life Cycle Stage 和 Life Cycle Stage Status 取代多个遗留字段，CI 和 Asset 之间自动双向同步。

### Remediation Workflows

Health Metric 不通过 → 生成 Remediation Task → Flow Designer 工作流自动修复（如重新发现 Stale CI）。

---

## 完整流程总结

1. 选择/扩展 CI Class（CI Class Manager）
2. 定义 Identification Rules（用稳定唯一属性）
3. 配置 Reconciliation Rules（静态/动态 + Data Refresh Rules）
4. 开启 CMDB 360（属性级溯源）
5. 选择摄入方案（Discovery / Connectors / ETL 等）
6. 数据经 IRE（Identification → Reconciliation）写入 CMDB
7. 填充 Non-Discoverable Data（Group 字段、Location）
8. 激活 CMDB Health Dashboard（三个计分卡）
9. 处理 Duplicate / Orphan / Stale CI
10. 配置 CI Reclassification Restriction Rules
11. 建立 Data Manager 生命周期策略（Retire → Archive → Delete）
12. 配置 Certification / Attestation 策略
13. 构建 Remediation Workflows 实现自动修复

核心指导思想：从小范围开始，逐步扩展。先覆盖核心 CI 类，让 identification rules 和 reconciliation rules 在实战中验证，再逐步扩大范围。

## Sources

- [[configure-the-cmdb|Configure the CMDB]] — Phase 1 配置：CI Class Manager、IRE、对账规则、CMDB 360
- [[ingest-data-into-the-cmdb|Ingest Data into the CMDB]] — Phase 2 摄入：六种方案详解
- [[govern-the-cmdb|Govern the CMDB]] — Phase 3 治理：Health Dashboard、生命周期、重分类
- [[IRE|Identification & Reconciliation Engine]] — IRE 四功能详解
- [[CMDBHealth|CMDB Health]] — 三大计分卡和修复工作流
- [[LifeCycleManagement|Life Cycle Management]] — Data Manager 策略详解
- [[CSDM|Common Service Data Model]] — CSDM 生命周期字段标准
- [[DiscoverableData|Discoverable Data]] — 可自动采集数据
- [[NonDiscoverableData|Non-Discoverable Data]] — 需人工填充数据
- [[reconciliation-rules-explained|Reconciliation Rules Explained]] — 对账规则核心机制
- [[static-vs-dynamic-reconciliation|Static vs. Dynamic Reconciliation]] — 动静对账深度对比
- [[servicenow-discovery-solutions|ServiceNow CMDB 数据摄入解决方案]] — 六种摄入方案总览

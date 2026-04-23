---
title: "Reconciliation Rules Explained"
type: synthesis
tags: [CMDB, ServiceNow, reconciliation, IRE]
sources: [configure-the-cmdb]
last_updated: 2026-04-22
---

# Reconciliation Rule 的作用

Reconciliation Rule（对账规则）是 [[ServiceNow]] [[CMDB]] 中保障数据准确性的核心机制，由 [[IRE|Identification & Reconciliation Engine (IRE)]] 执行。它解决的根本问题是：**当多个数据源（Discovery、SCCM、Service Graph Connectors、REST 集成等）同时向 CMDB 写入数据时，谁的值才算数？**

## 核心作用

1. **确定权威数据源** — 为每个 CI 类甚至每个属性指定哪个数据源是权威的。例如，可以规定服务器的主机名只信任 Discovery 的值，而 RAM 信息信任 SCCM 的值。

2. **防止数据覆盖冲突** — 没有对账规则时，多个数据源会互相覆盖同一属性的值（"flop back and forth"），导致数据不稳定、不可信。

3. **数据优先级排序** — 当多个数据源提供同一 CI 的同一属性时，对账规则按优先级决定谁胜出。

4. **阻断非法写入** — 管理员可以配置 IRE Data Source Rules 来阻止特定数据源的插入操作，进一步精细化控制。

## 静态 vs. 动态对账规则

| 类型 | 说明 |
|------|------|
| **静态对账规则** | 按数据源优先级决定谁有权更新，是基本模式 |
| **动态对账规则** | 基于 [[MultisourceCMDB|CMDB 360]] 的历史数据，按"首次上报/最多上报/最后上报/最大值/最小值"等策略选值。动态规则优先级高于静态规则 |

## 关键细节

- **ServiceNow 不提供任何默认的对账规则** — 每个客户环境的数据源配置不同，必须自行配置
- **对账发生在识别之后、写入之前** — 先用 Identification Rule 确认 CI 是否已存在，再决定是否允许更新
- **对账只管更新，不管创建** — 新 CI 的创建不经过对账流程
- **Data Refresh Rule** — 可配置时间窗口，如果高优先级数据源在指定时间内没有更新，则允许低优先级源接管
- 配置得当的对账规则可以处理 **90%** 的数据源信任决策

## 举例

假设一台 Linux 服务器同时被 Discovery 和 SCCM 发现：
- Discovery 报告 RAM = 32GB，SCCM 报告 RAM = 16GB
- 如果对账规则指定 Discovery 为 RAM 属性的权威源 → CMDB 中保留 32GB
- 如果没有对账规则 → 值会在 32GB 和 16GB 之间反复跳动，取决于谁最后写入

## Sources

- [[configure-the-cmdb|Configure the CMDB]]
- [[IRE|Identification & Reconciliation Engine]]
- [[MultisourceCMDB|Multisource CMDB / CMDB 360]]
- [[CMDB]]

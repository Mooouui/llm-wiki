---
title: "CMDB Governance 学习指南"
type: synthesis
tags: [CMDB, governance, ServiceNow, health, lifecycle, reclassification]
sources: [govern-the-cmdb]
last_updated: 2026-05-07
---

# CMDB Governance 学习指南

CMDB Governance（治理）是 CMDB 生命周期的第三阶段，排在 Configuration（配置）和 Ingestion（摄入）之后。一句话概括：配置是设计数据模型，摄入是往里填数据，而治理是确保数据长期保持可信。

Governance 的核心思想来自 Peter Drucker 的名言："你无法管理你不能衡量的东西。" ServiceNow 通过一套可量化、可自动化的框架来实施 CMDB 治理。

## CMDB Health Dashboard — 治理的核心度量框架

[[CMDBHealth|CMDB Health Dashboard]] 是治理的仪表盘，通过三个计分卡（Scorecards）衡量数据质量：

### 1. Completeness（完整性）

衡量 CI 的必要字段是否已填写。包含两个层级：

| 类型 | 说明 | 风险 |
|------|------|------|
| Required 字段 | 字典级别强制，记录无法不填就创建 | 可能导致 Discovery 或导入任务失败 |
| Recommended 字段 | 仅标记不强制，用于发现数据缺口 | 安全起点，不会中断现有流程 |

建议：从 Recommended 开始，逐步推进到 Required。

### 2. Compliance（合规性）

通过 Desired State Audit（期望状态审计）验证 CI 是否匹配预期配置。每个审计需要三个组件：Certification Filter（范围）、Certification Template（期望条件）、Audit（执行审计并生成修复任务）。

支持 Template-based 和 Scripted 两种审计类型。与 Data Manager 的 Certification Policy 区分：后者是人工验证不可自动发现的属性，而非检查字段是否填写。

### 3. Correctness（正确性）

三个指标：Duplicate（重复 CI）、Orphan（孤儿 CI，缺少必要关系）、Stale（陈旧 CI，超期未更新）。

Correctness 总分是通过所有定义指标的 CI 百分比，而非各指标分数的平均值。

Health Inclusion Rules 可以精选哪些 CI 类参与健康度量，支持按类、按指标粒度配置。

## 重复 CI 管理

[[IRE|IRE]] 在识别阶段判定重复：当 2+ 个 CI 匹配相同的 identification rules 时，最老的 CI（按创建日期）被视为非重复项。

三种解决方式：Duplicate CI Remediator（逐条）、De-Duplication Templates（批量、可调度）、Now Assist for CMDB（AI 驱动）。

## CI Reclassification（CI 重分类）

IRE 控制 CI 在类之间的移动：Upgrade、Downgrade、Switch。默认启用自动重分类，但 downgrade 和 switch 会导致数据丢失。通过 Restriction Rules 可做到类级别的精细控制。

## Life Cycle Management（生命周期管理）

[[LifeCycleManagement|CMDB Data Manager]] 提供五种策略：Retire、Archive、Delete、Attestation（验证物理存在）、Certification（验证不可自动发现的属性）。

生命周期是单向的：Retire → Archive → Delete，必须退休后才能归档或删除。旧版 Data Manager 在 Yokohama 版本起弃用，新版本从 CMDB Workspace 访问。

## CSDM 生命周期字段

[[CSDM]] 用 Life Cycle Stage 和 Life Cycle Stage Status 取代多个遗留字段（Operational Status、Install Status、Hardware Status、State、Substate 等）。CI 和 Asset 的生命周期字段自动双向同步。

## CI-Asset 同步

CI 和 Asset 共享一组字段并自动同步，包括遗留字段映射（Asset State ↔ CI Install Status）和 CSDM 字段同步。Hardware Status 不在同步范围内。

## Remediation Workflows

修复工作流路径：Enable Task → Flow Designer 构建工作流 → CMDB Remediation Rule 绑定 → Remediation Task 执行。去重任务和合规审计任务走不同的生成路径。

## 总结

CMDB Governance 的本质是：通过 Health Dashboard 量化数据质量 → 通过 IRE + De-Dup 机制清理重复 → 通过 Data Manager 策略管理 CI 生命周期 → 通过 CSDM 标准字段统一生命周期追踪。这是一套从度量到修复再到长期维护的闭环治理体系。

## Sources

- [[govern-the-cmdb|Govern the CMDB]] — 主要来源，完整治理框架
- [[CMDBHealth|CMDB Health]] — Health Dashboard 三大计分卡详解
- [[LifeCycleManagement|Life Cycle Management]] — Data Manager 策略和生命周期阶段
- [[CSDM|Common Service Data Model]] — CSDM 生命周期字段和标准化
- [[CMDB|CMDB]] — 三阶段生命周期总览和治理工具索引
- [[ServiceNow|ServiceNow]] — 平台级治理产品列表

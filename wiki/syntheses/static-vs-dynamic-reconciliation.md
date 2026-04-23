---
title: "Static vs. Dynamic Reconciliation Rules"
type: synthesis
tags: [CMDB, ServiceNow, reconciliation, IRE]
sources: [configure-the-cmdb]
last_updated: 2026-04-22
---

# Static vs. Dynamic Reconciliation Rule 深度对比

## Static Reconciliation Rule（静态对账规则）

静态规则的核心逻辑是 **"信任谁"** — 按数据源的优先级决定哪个源有权更新某个 CI 类或属性。

**工作机制：**
- 管理员为某个 CI 类配置一条静态规则，指定哪些数据源可以更新、按什么优先级排序
- 当 [[IRE]] 处理 payload 时，只允许优先级最高的数据源写入
- 低优先级源的值被直接丢弃（除非启用了 [[MultisourceCMDB|CMDB 360]]，否则永久丢失）

**举例：**
- 规则：Discovery (优先级 1) > SCCM (优先级 2) > REST API (优先级 3)
- Discovery 报告某服务器 `ram = 32GB` → 写入 CMDB
- SCCM 报告同一服务器 `ram = 16GB` → 被拒绝
- 即使 Discovery 的值实际是错的，静态规则也盲目信任优先级

**局限性：** 只看"谁说的"，不看"说得对不对"。无法根据数据本身的特征做判断。

**补充机制 — Data Refresh Rule：**
可以给静态规则附加一个时间窗口。如果高优先级源在 N 天内没有更新某个类，就临时允许低优先级源接管更新，防止数据过期。

## Dynamic Reconciliation Rule（动态对账规则）

动态规则的核心逻辑是 **"哪个值更可信"** — 不盲目信任某个数据源，而是根据 [[MultisourceCMDB|CMDB 360]] 保存的历史数据，按策略选值。

**前提条件：** 必须启用 CMDB 360 / Multisource CMDB（Paris 版本引入），因为动态规则需要访问所有数据源上报过的历史值。

**五种策略：**

| 策略 | 逻辑 | 适用场景 |
|------|------|----------|
| **First Reported** | 谁先报就用谁的值 | 信任最早发现该 CI 属性的源 |
| **Most Reported** | 哪个值被报的次数最多 | 多数源一致时大概率正确 |
| **Last Reported** | 用最新的上报值 | 信任最新数据 |
| **Largest Value** | 取最大值 | 仅适用于数值型字段 |
| **Smallest Value** | 取最小值 | 仅适用于数值型字段 |

**工作机制：**
1. [[IRE]] 先处理当前 payload
2. 然后查阅 [[MultisourceCMDB]] 中该 CI 属性的所有历史值
3. 按选定策略从所有值中选出最合适的
4. 如果无法简单判定（比如两个值被报的次数相同），会进一步参考 last reported / last discovered / last updated 等时间戳来裁决

**举例：**
- Discovery 报告 `disk_size = 500GB`
- SCCM 报告 `disk_size = 512GB`
- AWS Connector 报告 `disk_size = 500GB`
- 动态规则设为 "Most Reported" → 500GB 胜出（2 票 vs 1 票）
- 即使 Discovery 不是最高优先级源，它的值也可能因为被多个源交叉验证而胜出

## 关键对比

| | Static | Dynamic |
|---|---|---|
| **决策依据** | 数据源优先级 | 历史数据中的值特征 |
| **需要 CMDB 360** | 否 | 是 |
| **配置复杂度** | 低（排优先级即可） | 中（需选策略 + 选属性） |
| **适用属性类型** | 所有类型 | Largest/Smallest 仅限数值型 |
| **优先级关系** | 基准规则 | **动态规则优先级更高**，两者同时存在时动态胜出 |
| **能否重新计算** | 改规则后需等新数据 | 改规则后可立即 recompute 已有数据 |

## 什么时候用哪个？

- **静态规则**：有明确的权威数据源（比如 Discovery 是网络设备唯一可信源），用静态规则简单高效
- **动态规则**：多个数据源可靠性参差不齐，需要根据数据本身特征（谁报得多、谁先报、值的大小）来决策时使用。典型场景：不同源对同一属性报告的值不一致，且没有哪个源明显更可靠

## Sources

- [[configure-the-cmdb|Configure the CMDB]]
- [[IRE|Identification & Reconciliation Engine]]
- [[MultisourceCMDB|Multisource CMDB / CMDB 360]]

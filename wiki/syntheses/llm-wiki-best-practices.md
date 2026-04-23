---
title: "LLM Wiki 最佳实践"
type: synthesis
tags: [best-practices, llm-wiki, workflow]
sources: [llm-wiki-complete-guide]
last_updated: 2026-04-09
---

## LLM Wiki 的最佳实践

### 1. 架构实践：严格保持三层分离

- **Raw 层不可变**：`raw/` 目录是"真理之源"，LLM 只读不写。这保证你始终可以追溯到原始数据进行验证 ([[LLMWiki|LLM Wiki]])
- **Wiki 层交给 LLM**：`wiki/` 层由 LLM 完全控制——你读它，LLM 写它。不要手动编辑 Wiki 页面，否则会破坏 LLM 的维护一致性 ([[LLMWiki|LLM Wiki]])
- **Schema 层持续演化**：`CLAUDE.md` 是让人和 LLM 共同维护的"控制协议"。发现什么好用、什么不好用就立刻更新它 ([[Schema]])

### 2. Ingest 实践：一次一个，全程参与

- [[AndrejKarpathy|Andrej Karpathy]] 个人偏好一次摄入一个来源，全程参与——阅读摘要、检查更新、引导 LLM 该强调什么
- 也可以批量摄入减少人工介入，但关键是**找到适合自己的节奏，并记录在 Schema 里**
- 每次摄入后立刻 `git commit`，保留清晰的版本历史

### 3. Query 实践：好答案不要留在聊天记录里

- 当一次查询产生有价值的洞察时，**让它归档为新的 Wiki 页面**
- 这形成复利循环：来源被摄入 → 提问产生新洞察 → 洞察归档为新页面 → Wiki 从外部来源和内部探索双向增长 ([[LLMWiki|LLM Wiki]])

### 4. Lint 实践：每周一次健康检查

定期让 LLM 执行"代码审查"级别的检查：
- 检测自相矛盾的结论（新旧来源冲突）
- 找出没有入链的"孤岛页面"
- 发现被多次提及但没有独立页面的概念
- 标记被新来源取代的过时结论
- 建议值得调查的新问题

### 5. 规模化实践：递进式升级工具链

| 阶段 | 来源数 | 搜索方案 |
|------|--------|----------|
| 启动期 | 1–10 | `index.md` 足够 |
| 成长期 | 10–50 | 查询开始，依赖结构化索引 |
| 扩展期 | 50–100 | `index.md` + `log.md` 双索引 |
| 规模期 | 100+ | 引入 [[TobiLutke|Tobi Lutke]] 的 qmd（BM25 + 向量 + LLM 重排序） |

### 6. 最重要的实践：混合方案（地图 ≠ 领地）

[[ExtendedBrain|Extended Brain]] 借助 [[NiklasLuhmann|Niklas Luhmann]] 的 [[Zettelkasten]] 和 [[Hormesis|认知摩擦]] 概念提出了最有深度的警告：LLM 写出流畅的综合文章，没有挣扎、没有语言暴露理解缺口的时刻。读这些文章的人可能觉得自己理解了主题，但没做过建构理解的认知工作。

**最佳实践是混合方案**：
- 用 LLM 做**脚手架层**：构建互联图谱、发现缺口、维护索引、识别跨来源的意外连接——这是 LLM 比任何人都擅长的事
- 把**综合层留给自己**：当 LLM 告诉你两个想法有关联时，不要读它的综合文章——自己写。用自己的话去挣扎
- 重新定位 Lint：让 LLM **发现矛盾然后停下来**，而不是替你解决矛盾。"这里有三个东西似乎存在张力"——张力本身就是礼物

> 用机器构建地图，然后坚持自己走过那片土地。

### 7. 工具配置实践

- **本地化图片**：在 [[Obsidian]] 中把附件路径指向 `raw/assets/`，绑定快捷键下载图片，让 LLM 不依赖可能失效的 URL
- **Web Clipper**：一键剪藏网页为 Markdown 直接进入 `raw/`
- **Graph View**：定期观察 Wiki 形态——枢纽页面、孤岛一目了然
- **Git**：`git diff` 看每次摄入改了什么，`git revert` 回滚糟糕的编译

## Sources

- [[LLMWiki|LLM Wiki]]
- [[Schema]]
- [[Hormesis]]
- [[Zettelkasten]]
- [[Overview]]

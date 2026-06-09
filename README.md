<!-- BADGE BAR -->
[![License](https://img.shields.io/badge/license-MIT-blue)](./LICENSE)
[![Claude Code](https://img.shields.io/badge/Claude%20Code-Skill-orange)](https://claude.ai)

# skill-bootstrapper

> **Skill 创建编排器。** 从需求到 GitHub 发布全流程。自动判断复杂度，选最优路径——不走弯路，不重复造轮子。

[English](#english)

---

## 为什么需要 skill-bootstrapper？

- **想建 Skill 但不知道从哪开始。** 需求探索 → 设计 spec → 实现计划 → 编码 → 发布，每一步都可能走偏。
- **不知道这个 Skill 是不是已经有人做过了。** 盲目造轮子是 AI 编程最常见的浪费。bootstrapper 强制先查市场再建。
- **简单 Skill 和复杂 Skill 不该走同一条路。** 3 步的简单指令不该跑完整 eval 流程。bootstrapper 自动判断复杂度，分两条通道。

## 核心能力

- 🔍 **市场优先检查** — 先在 GitHub/插件市场搜索是否已有类似 Skill
- ⚖️ **复杂度自动判断** — 5 个维度（步骤数/依赖/触发词/输出/主观性）决定走快速通道还是 eval 通道
- 🧠 **brainstorming 驱动** — 强制先设计再实现，不过早陷入代码
- 📦 **GitHub 发布** — README + LICENSE + 初始化 + push，一站式搞定

## 工作流

```
用户: "创建一个 skill"
    │
    ▼
  brainstorming → 设计 spec
    │
    ▼
  复杂度判断
    ├── 简单 → writing-plans → subagent → 快速通道
    └── 复杂 → skill-creator eval → 迭代 → 人工验证
    │
    ▼
  GitHub 发布
```

## 快速开始

### 触发

| 你说 | 它做什么 |
|------|---------|
| `创建一个 skill` / `新建 skill` | 启动完整的 skill 创建流程 |
| `/bootstrap-skill` / `/new-skill` | 同上 |

## 设计哲学

**先查市场，再建。** 这是长期复利的第一道防线——一个重复的 Skill = 未来所有对话都要加载两份类似内容。宁可多花 2 分钟搜索，不让体系膨胀。

**简单的事不该复杂化。** 不是每个 Skill 都需要跑 eval 迭代。3 步的格式化指令不值得一个完整的 TDD 循环。自动判断、快速分流。

**设计 spec 是不可跳过的关卡。** 动代码之前先把"要解决什么问题、为什么这样解决"写清楚。一个 100 行的 spec 比 500 行改来改去的代码更值钱。

## 相关项目

| 项目 | 关系 |
|------|------|
| [skill-optimizer](https://github.com/2021291696/skill-optimizer) | 下游 — 创建之后，持续优化 |
| [web-search-mcp](https://github.com/2021291696/web-search-mcp) | 工具 — 搜索市场上已有 skill |

## License

MIT

---

## English

# skill-bootstrapper

> **Skill creation orchestrator.** Full pipeline from idea to GitHub release. Auto-detects complexity and chooses the optimal path — no detours, no reinventing wheels.

### Why?

Don't know where to start building a skill? bootstrapper guides you through brainstorming → spec → plan → code → publish. Building something that already exists? Market-first check prevents duplicate effort. Simple skills shouldn't go through complex eval pipelines — auto-detection routes them to a fast track.

### Design Philosophy

**Search the market before building.** The first line of defense for long-term compounding — one duplicate skill means loading similar content in every future conversation.

**Simple things stay simple.** Not every skill needs eval iteration. A 3-step formatting directive doesn't deserve a full TDD cycle.

**The spec is non-negotiable.** Write down "what problem and why this solution" before touching code. A 100-line spec is worth more than 500 lines of back-and-forth code changes.

### Related

| Project | Relationship |
|---------|-------------|
| [skill-optimizer](https://github.com/2021291696/skill-optimizer) | Downstream — continuous optimization after creation |

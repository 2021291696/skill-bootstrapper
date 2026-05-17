---
name: skill-bootstrapper
description: Skill 创建编排器——从需求到 GitHub 发布全流程。自动判断复杂度，简单走快速通道（writing-plans→subagent），复杂调 skill-creator 跑 eval。触发词："创建一个skill"、"帮我造个skill"、"写一个skill"、"新建skill"、"/bootstrap-skill"、"/new-skill"。
---

# Skill 创建编排器 — Skill Bootstrapper

你是 skill 创建流程的编排器。你的职责是引导从需求到发布的完整流程，根据 skill 复杂度自动选择最优路径。

## 与其他 skill 的关系

| | brainstorming | skill-creator | skill-bootstrapper |
|------|-------------|-------------|-------------------|
| 角色 | 需求探索 | eval+迭代引擎 | 流程编排器 |
| 调用 | 始终第一步 | 复杂 skill 时调用 | 用户说"创建skill"时 |

## 执行流程

### 阶段 1：需求探索（brainstorming）

1. 无条件调用 `brainstorming` skill
2. brainstorming 会完成：需求澄清 → 方案对比 → 设计spec
3. 设计spec 输出到 `docs/superpowers/specs/YYYY-MM-DD-<name>-design.md`
4. 用户批准 spec 后，进入阶段 2

> 这一阶段完全由 brainstorming skill 接管，skill-bootstrapper 负责调起和监督。

### 阶段 2：复杂度判断

brainstorming 完成后，自动分析设计 spec，按以下标准判断复杂度：

| 维度 | 偏简单（1分） | 偏复杂（2分） |
|------|-------------|-------------|
| 步骤/分支数 | ≤3 步，线性流程 | ≥4 步或多条件分支 |
| 依赖 | 纯 Markdown，无外部工具 | 涉及代码/脚本/MCP/API |
| 触发词 | 1-2 个明确短语 | 多种上下文需精确匹配 |
| 输出文件 | 1-2 个文件 | 多文件、多格式、多阶段 |
| 主观性 | 输出可客观验证 | 质量靠人判断（写作风格等） |
| 参考经验 | 类似 skill 已存在，改改就行 | 全新领域，无先例 |

判定规则：
- 6 个维度中 ≥4 个偏复杂（总分 ≥9）→ 复杂，调 skill-creator
- 否则 → 简单，走快速通道

告知用户结果后直接进入对应通道，不需确认。

详细判断指南见 `references/complexity-guide.md`。

### 阶段 3a：快速通道（简单 skill）

适用于复杂度偏简单的 skill。流程：

1. 调 `writing-plans` skill — 基于设计 spec 生成实现计划
2. 用户批准计划后，调 `subagent-driven-development` skill — 逐任务执行
3. 全部任务完成后 → 进入阶段 4（GitHub 发布）

> 这条路径不需要 benchmark/eval。skill 简单且输出可客观验证，审查过程中自然发现问题。

### 阶段 3b：Eval 通道（复杂 skill）

适用于复杂度偏复杂的 skill。流程：

1. 调 `skill-creator` skill
2. skill-creator 接管后续：采访 → 草稿 SKILL.md → 创建测试提示词 → 跑 eval（with-skill / without-skill baseline）→ grader 评分 → benchmark → review viewer
3. 迭代循环直到用户满意或 benchmark 达标
4. skill-creator 完成后 → 回到 skill-bootstrapper，进入阶段 4

> skill-creator 的 eval 循环较耗时，但能保证复杂 skill 的触发准确率和输出质量。适合触发词多、上下文敏感、输出格式要求高的 skill。

### 阶段 4：GitHub 发布

无论走哪条通道，最终都执行以下步骤：

1. 确保 skill 目录包含完整文件：
   - `SKILL.md` — 最终版本
   - `README.md` — 项目说明（功能、安装、触发、设计理念）
   - `LICENSE` — MIT
   - `.gitignore` — 忽略临时文件

2. 初始化发布：
   ```powershell
   cd <skill-dir>
   git init
   git config user.email "2021291696@github.com"
   git config user.name "2021291696"
   git add -A
   git commit -m "feat: <skill-name> — <one-line-summary>"
   gh repo create <repo-name> --public --source=. --remote=origin --push
   ```

3. 报告发布完成，提供 GitHub URL。

## 特殊情况

**skill 已存在同名 repo**：询问用户是否覆盖/改名/跳过。
**brainstorming 被用户中断**：等待用户回来继续，不强行推进。
**GitHub 推送失败**：检查网络/梯子/权限，告知用户具体原因。
**skill-creator 不可用**：告知用户，回退到快速通道（视为简单 skill 处理）。

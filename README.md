# skill-bootstrapper — Skill 创建编排器

从需求到 GitHub 发布全流程。自动判断复杂度选择最优路径。

## 为什么需要

创建 skill 有成熟流程，但每次都要手动串联。skill-bootstrapper 编排全过程：
- 简单 skill 走快速通道（几分钟到发布）
- 复杂 skill 调 skill-creator 跑 eval（保证质量）

## 功能

1. **需求探索** — 无条件调 brainstorming
2. **复杂度判断** — 六维度自动评分，决定走哪条通道
3. **快速通道** — writing-plans → subagent-driven（简单 skill）
4. **Eval 通道** — 调 skill-creator 跑 benchmark+迭代（复杂 skill）
5. **GitHub 发布** — README + LICENSE + push

## 复杂度判断

| 维度 | 简单（1分） | 复杂（2分） |
|------|-----------|-----------|
| 步骤数 | ≤3步 | ≥4步或多分支 |
| 依赖 | 纯Markdown | 代码/脚本/MCP/API |
| 触发词 | 1-2个明确短语 | 多种上下文 |
| 输出 | 1-2个文件 | 多文件多格式 |
| 主观性 | 客观可验证 | 靠人判断 |
| 参考 | 已有类似 | 全新领域 |

总分 6-8 → 快速通道 / 9-12 → Eval通道

## 触发

```
命令：/bootstrap-skill、/new-skill
关键词："创建一个skill"、"帮我造个skill"、"写一个skill"、"新建skill"
```

## 安装

```powershell
git clone https://github.com/2021291696/skill-bootstrapper.git
Copy-Item -Recurse skill-bootstrapper/ "$env:USERPROFILE\.claude\skills\skill-bootstrapper"
```

## 文件结构

```
skill-bootstrapper/
├── SKILL.md                     — 主指令（四阶段流程）
├── README.md                    — 本文件
└── references/
    └── complexity-guide.md      — 复杂度判断详细指南
```

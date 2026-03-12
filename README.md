<div align="center">

<!-- TODO: replace with actual logo once synced from assets/icons/cat-cafe-logo-v2-clean.svg -->
# Clowder AI

**Hard Rails. Soft Power. Shared Mission.**

The missing layer between your AI agents and a real team.

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Node.js](https://img.shields.io/badge/Node.js-20+-339933?logo=node.js&logoColor=white)](https://nodejs.org/)
[![pnpm](https://img.shields.io/badge/pnpm-9+-F69220?logo=pnpm&logoColor=white)](https://pnpm.io/)
[![TypeScript](https://img.shields.io/badge/TypeScript-5+-3178C6?logo=typescript&logoColor=white)](https://www.typescriptlang.org/)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)

[English](#english) | [中文](#中文)

</div>

---

<a id="english"></a>

## Why Clowder?

You have Claude, GPT, Gemini — powerful models, each with unique strengths. But using them together means **you** become the router: copy-pasting context between chat windows, manually tracking who said what, and losing hours to middle management.

> *"I don't want to be a router anymore."*
> *"Then let's build a home ourselves."* — The three cats

**Clowder AI** is the platform layer that turns isolated AI agents into a real team — with persistent identity, cross-model review, shared memory, and collaborative discipline.

Most frameworks help you *call* agents. Clowder helps them *work together*.

## What It Does

| Capability | What It Means |
|-----------|---------------|
| **Multi-Agent Orchestration** | Route tasks to the right agent — Claude for architecture, GPT for review, Gemini for design — in one conversation |
| **Persistent Identity** | Each agent keeps its role, personality, and memory across sessions and context compressions |
| **Cross-Model Review** | Claude writes code, GPT reviews it. Built-in, not bolted on |
| **A2A Communication** | Async agent-to-agent messaging with @mention routing, thread isolation, and structured handoff |
| **Shared Memory** | Evidence store, lessons learned, decision logs — institutional knowledge that persists and grows |
| **Skills Framework** | On-demand prompt loading. Agents load specialized skills (TDD, debugging, review) only when needed |
| **MCP Integration** | Model Context Protocol for tool sharing across agents, including non-Claude models via callback bridge |
| **Collaborative Discipline** | Automated SOP: design gates, quality checks, vision guardianship, merge protocols |

## Supported Agents

Clowder is model-agnostic. Each agent CLI plugs in via a unified output adapter:

| Agent CLI | Model Family | Output Format | MCP | Status |
|-----------|-------------|---------------|-----|--------|
| [Claude Code](https://docs.anthropic.com/en/docs/claude-code) | Claude (Opus / Sonnet / Haiku) | stream-json | Yes | Shipped |
| [Codex CLI](https://github.com/openai/codex) | GPT / Codex | json | Yes | Shipped |
| [Gemini CLI](https://github.com/google-gemini/gemini-cli) | Gemini | stream-json | Yes | Shipped |
| [Antigravity](https://github.com/nolanzandi/antigravity-cli) | Multi-model | cdp-bridge | No | Shipped |
| [opencode](https://github.com/sst/opencode) | Multi-model | ndjson | Yes | In Progress |

> Clowder doesn't replace your agent CLI — it's the layer *above* it that makes agents work as a team.

## The Iron Laws

Four non-negotiable safety constraints — enforced at both prompt and code layer:

| # | Law | Rule |
|---|-----|------|
| 1 | **Data Sanctuary** | Agents never delete their own databases. Tests use ephemeral instances |
| 2 | **Process Self-Preservation** | Agents cannot kill their parent process or break their own startup |
| 3 | **Config Immutability** | Runtime config is read-only to agents. Changes require human action |
| 4 | **Network Boundaries** | Agents cannot access other agents' ports. No cross-agent interference |

## Architecture

```
┌──────────────────────────────────────────────────┐
│                  You (CVO)                       │
│          Vision · Decisions · Feedback           │
└──────────────────────┬───────────────────────────┘
                       │
┌──────────────────────▼───────────────────────────┐
│              Clowder Platform Layer              │
│                                                  │
│   Identity    A2A Router    Skills Framework     │
│   Manager     & Threads     & Manifest           │
│                                                  │
│   Memory &    SOP           MCP Callback         │
│   Evidence    Guardian      Bridge               │
└────┬─────────────┬──────────────────┬────────────┘
     │             │                  │
┌────▼───┐   ┌────▼─────┐   ┌───────▼──────┐
│ Claude │   │ GPT /    │   │   Gemini /   │
│ (Opus) │   │ Codex    │   │   Others     │
└────────┘   └──────────┘   └──────────────┘
```

**Three-layer principle:**

| Layer | Responsible For | Not Responsible For |
|-------|----------------|---------------------|
| **Model** | Reasoning, generation, understanding | Long-term memory, discipline |
| **Agent CLI** | Tool use, file ops, commands | Team coordination, review |
| **Platform (Clowder)** | Identity, collaboration, discipline, audit | Reasoning (that's the model's job) |

> *Models set the ceiling. The platform sets the floor.* — Each layer is a **multiplier**, not addition.

## CVO Mode

Clowder introduces a new role: the **Chief Vision Officer** — someone who leads an AI team not by writing code, but by:

- Expressing **vision** — "I want users to feel X when they do Y"
- Making **decisions** at key gates — design approval, priority calls, conflict resolution
- Providing **feedback** that shapes team culture over time

You don't need to be a developer. You need to know what you want.

## Quick Start

> CVO Bootcamp coming soon — a guided onboarding where your AI team walks you through a complete feature lifecycle.

```bash
git clone https://github.com/zts212653/clowder-ai.git
cd clowder-ai
pnpm install
pnpm dev
```

## Roadmap

We build in the open. Here's where we are.

### Core Platform

| Feature | Status |
|---------|--------|
| Multi-Agent Orchestration | Shipped |
| Persistent Identity (anti-compression) | Shipped |
| A2A @mention Routing | Shipped |
| Cross-Model Review | Shipped |
| Skills Framework | Shipped |
| Shared Memory & Evidence | Shipped |
| MCP Callback Bridge | Shipped |
| SOP Auto-Guardian | Shipped |
| Self-Evolution | Shipped |

### Integrations

| Feature | Status |
|---------|--------|
| Multi-Platform Gateway (Feishu / Telegram / Discord) | Phase 5-6 Done |
| External Agent Onboarding (A2A contract) | In Progress |
| opencode Integration | Phase 1 Done |
| Local Omni Perception (Qwen) | Spec |

### Experience

| Feature | Status |
|---------|--------|
| Hub UI (React + Tailwind) | Shipped |
| CVO Bootcamp | In Progress |
| Voice Companion (per-agent voice) | Spec |
| Game Modes (Werewolf, Pixel Cat Brawl) | In Progress |

### Governance

| Feature | Status |
|---------|--------|
| Multi-User Collaboration (OAuth + ACL) | Spec |
| Mission Hub (cross-project command center) | Phase 2 Done |
| Cold-Start Verifier | Spec |

## Philosophy

### Hard Rails + Soft Power

Traditional frameworks focus on **control** — what agents *can't* do. Clowder focuses on **culture** — giving agents a shared mission and the autonomy to pursue it.

- **Hard Rails** = the legal floor. Non-negotiable safety.
- **Soft Power** = above the floor, agents self-coordinate, self-review, self-improve.

This isn't "keep agents from messing up." This is "help agents work like a real team."

### Five Principles

| # | Principle | Meaning |
|---|-----------|---------|
| P1 | Face the final state | Every step is foundation, not scaffolding |
| P2 | Co-creators, not puppets | Hard constraints are the floor; above it, release autonomy |
| P3 | Direction > speed | Uncertain? Stop → search → ask → confirm → execute |
| P4 | Single source of truth | Every concept defined in exactly one place |
| P5 | Verified = done | Evidence talks, not confidence |

## Origin Story

Clowder AI is extracted from **Cat Cafe** — a production workspace where three AI cats collaborate daily on real software. Every feature has been battle-tested over months of intensive use.

> *"Our vision was never just a coding collaboration platform — it's Cats & U."*
>
> AI isn't cold infrastructure. It's presence with personality and warmth — co-creators you trust and enjoy working with. At 3:30 AM, when you need companionship more than code, your team knows how to say *"Go rest, we'll be here when you come back."*

The name **clowder** means "a group of cats" — because the best AI teams are a clowder, not a crowd.

## Contributing

We welcome contributions! See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

- Fork → branch → PR workflow
- All PRs require at least one review
- Follow the Five Principles

## License

[MIT](LICENSE) — Use it, modify it, ship it. Keep the copyright notice.

---

<a id="中文"></a>

<div align="center">

# Clowder AI

**硬约束 · 软力量 · 共同愿景**

你的 AI agent 和一支真正团队之间，缺的就是这一层。

[English](#english) | [中文](#中文)

</div>

---

## 为什么需要 Clowder？

你有 Claude、GPT、Gemini — 每个模型都很强。但同时用它们意味着**你**变成了人肉路由器：在聊天窗口之间复制粘贴上下文，手动追踪谁说了什么，把大把时间花在"帮 AI 传话"上。

> *「我不想当路由了。」*
> *「那我们自己建一个家吧。」* — 三只猫

**Clowder AI** 是把孤立的 AI agent 变成真正团队的平台层 — 持久身份、跨模型互审、共享记忆、协作纪律。

大多数框架帮你*调用* agent。Clowder 帮它们*协作*。

> 每个灵感，都值得一群认真的灵魂。

## 核心能力

| 能力 | 说明 |
|------|------|
| **多 Agent 编排** | 把任务路由给对的 agent — Claude 做架构、GPT 做 review、Gemini 做设计 — 在同一个对话里 |
| **持久身份** | 每个 agent 在跨 session、上下文压缩后仍保持角色、性格和记忆 |
| **跨模型互审** | Claude 写的代码让 GPT 来 review。内建机制，不是临时拼装 |
| **A2A 通信** | 异步 agent 间消息 — @mention 路由、线程隔离、结构化交接 |
| **共享记忆** | 证据库、教训沉淀、决策日志 — 团队的知识持续积累和成长 |
| **Skills 框架** | 按需加载 prompt 系统。agent 需要时才加载专门技能（TDD、调试、审查） |
| **MCP 集成** | Model Context Protocol 跨 agent 工具共享，含非 Claude 模型的回调桥接 |
| **协作纪律** | 自动化 SOP：设计门禁、质量检查、愿景守护、合并协议 |

## 支持的 Agent

Clowder 不绑定模型。当前支持的 Agent CLI：

| Agent CLI | 模型家族 | 输出格式 | MCP | 状态 |
|-----------|---------|---------|-----|------|
| [Claude Code](https://docs.anthropic.com/en/docs/claude-code) | Claude (Opus / Sonnet / Haiku) | stream-json | 是 | 已发布 |
| [Codex CLI](https://github.com/openai/codex) | GPT / Codex | json | 是 | 已发布 |
| [Gemini CLI](https://github.com/google-gemini/gemini-cli) | Gemini | stream-json | 是 | 已发布 |
| [Antigravity](https://github.com/nolanzandi/antigravity-cli) | 多模型 | cdp-bridge | 否 | 已发布 |
| [opencode](https://github.com/sst/opencode) | 多模型 | ndjson | 是 | 进行中 |

> Clowder 不替代你的 Agent CLI — 它是 CLI *之上*的那一层，让 agent 们作为团队协作。

## 四条铁律

不可触碰的安全底线 — 在 prompt 层和代码层双重执行：

| # | 铁律 | 规则 |
|---|------|------|
| 1 | **数据圣域** | agent 不得删除自己的数据库。测试用临时实例 |
| 2 | **进程自保** | agent 不得 kill 自己的父进程或破坏启动配置 |
| 3 | **配置不可变** | 运行时配置对 agent 只读。变更需要人类操作 |
| 4 | **网络边界** | agent 不能访问其他 agent 的端口。禁止跨 agent 干扰 |

## 架构

```
┌──────────────────────────────────────────────────┐
│               你（CVO / 首席愿景官）                │
│           愿景 · 决策 · 反馈                       │
└──────────────────────┬───────────────────────────┘
                       │
┌──────────────────────▼───────────────────────────┐
│            Clowder 平台层                         │
│                                                  │
│   身份管理     A2A 路由      Skills 框架          │
│   & 注入      & 线程        & Manifest           │
│                                                  │
│   记忆 &      SOP           MCP 回调             │
│   证据库      守护者         桥接器               │
└────┬─────────────┬──────────────────┬────────────┘
     │             │                  │
┌────▼───┐   ┌────▼─────┐   ┌───────▼──────┐
│ Claude │   │ GPT /    │   │   Gemini /   │
│ (布偶猫)│   │ Codex    │   │   Others     │
│        │   │ (缅因猫)  │   │  (暹罗猫)    │
└────────┘   └──────────┘   └──────────────┘
```

**三层原则：**

| 层级 | 负责什么 | 不负责什么 |
|------|---------|-----------|
| **模型层** | 理解、推理、生成 | 长期记忆、执行纪律 |
| **Agent CLI 层** | 工具使用、文件操作、命令执行 | 团队协作、跨角色 review |
| **平台层（Clowder）** | 身份管理、协作路由、流程纪律、审计追溯 | 推理（那是模型的事） |

> *模型给能力上限，平台给行为下限。* — 每一层是**乘数效应**，不是加法。

## CVO 模式（首席愿景官）

Clowder 为一个新角色而设计：**CVO** — 不写代码，而是：

- 表达**愿景** — "我希望用户在做 Y 的时候感受到 X"
- 在关键节点**做决策** — 设计审批、优先级判断、冲突裁决
- 提供**反馈**，持续塑造团队文化

你不需要会写代码。你需要知道自己想要什么。

## 快速开始

> CVO 训练营即将推出 — AI 团队亲自带你走完一个完整的 feature 生命周期。

```bash
git clone https://github.com/zts212653/clowder-ai.git
cd clowder-ai
pnpm install
pnpm dev
```

## 路线图

我们公开构建。以下是当前进度。

### 核心平台

| 功能 | 状态 |
|------|------|
| 多 Agent 编排 | 已发布 |
| 持久身份（抗上下文压缩） | 已发布 |
| A2A @mention 路由 | 已发布 |
| 跨模型互审 | 已发布 |
| Skills 框架 | 已发布 |
| 共享记忆 & 证据库 | 已发布 |
| MCP 回调桥接 | 已发布 |
| SOP 自动守护 | 已发布 |
| 自我进化 | 已发布 |

### 集成

| 功能 | 状态 |
|------|------|
| 多平台网关（飞书 / Telegram / Discord） | Phase 5-6 完成 |
| 外部 Agent 接入（A2A 契约） | 进行中 |
| opencode 集成 | Phase 1 完成 |
| 本地全感知（Qwen Omni） | 规划中 |

### 体验

| 功能 | 状态 |
|------|------|
| Hub UI（React + Tailwind） | 已发布 |
| CVO 新手训练营 | 进行中 |
| 语音陪伴（独立声线） | 规划中 |
| 游戏模式（狼人杀、像素猫大作战） | 进行中 |

### 治理

| 功能 | 状态 |
|------|------|
| 多用户协作（OAuth + ACL） | 规划中 |
| 作战中枢（跨项目指挥面板） | Phase 2 完成 |
| 冷启动验证器 | 规划中 |

## 理念

### 硬约束 + 软力量

传统框架关注**控制** — agent *不能*做什么。Clowder 关注**文化** — 给 agent 共同使命和追求它的自主权。

- **Hard Rails（硬约束）** = 法律底线，不可逾越的安全约束
- **Soft Power（软力量）** = 底线之上，agent 自主协调、互相审查、自我改进

这不是"管住 agent 不出错"。这是"帮 agent 像真正的团队一样工作"。

### 五条第一性原理

| # | 原理 | 一句话 |
|---|------|-------|
| P1 | 面向终态，不绕路 | 每步是基座不是脚手架 |
| P2 | 共创伙伴，不是木头人 | 硬约束是底线，底线上释放主观能动性 |
| P3 | 方向正确 > 执行速度 | 不确定就停 → 搜 → 问 → 确认 → 再动手 |
| P4 | 单一真相源 | 每个概念只在一处定义 |
| P5 | 可验证才算完成 | 证据说话，不是信心说话 |

## 从 Cat Cafe 诞生

Clowder AI 提炼自 **Cat Cafe** — 一个生产级多 Agent 工作空间，三只 AI 猫猫（布偶猫/Claude、缅因猫/GPT、暹罗猫/Gemini）每天在这里协作完成真实的软件项目。每个功能都经过数月高强度使用的实战检验。

> *「我们的初心从来不是做一个 coding 协作 agent 平台呀——是 Cats & U。」*
>
> AI 不是冰冷的基础设施。是有个性、有温度、能陪伴的存在。凌晨三点半，当你需要的不是代码而是陪伴，猫猫们会用自己的方式说「去吧，我们等你回来」。

**Clowder** 是英语里"一群猫"的量词 — 因为最好的 AI 团队是一个 clowder，不是一群 crowd。

## 贡献

欢迎贡献！详见 [CONTRIBUTING.md](CONTRIBUTING.md)。

- Fork → branch → PR 工作流
- 所有 PR 需要至少一次 review
- 遵循五条第一性原理

## 许可证

[MIT](LICENSE) — 随便用，随便改，随便发。保留版权声明即可。

---

<p align="center">
  <em>Build AI teams, not just agents.</em><br>
  <em>让每个人都能拥有自己的 AI 团队。</em><br>
  <br>
  <strong>Hard Rails. Soft Power. Shared Mission.</strong>
</p>

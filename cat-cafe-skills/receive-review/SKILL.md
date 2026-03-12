---
name: receive-review
description: >
  处理 reviewer 反馈：Red→Green 修复 + 技术论证（禁止表演性同意）。
  Use when: 收到 review 结果、reviewer 提了 P1/P2、需要处理反馈。
  Not for: 发 review 请求（用 request-review）、自检（用 quality-gate）。
  Output: 逐项修复确认 + reviewer 放行。
triggers:
  - "review 结果"
  - "review 意见"
  - "reviewer 说"
  - "fix these"
---

> **SOP 位置**: 本 skill 是 `docs/SOP.md` Step 3b 的执行细节。
> **上一步**: `request-review` (Step 3a) | **下一步**: `merge-gate` (Step 4)

# Receive Review

处理 reviewer 反馈的完整流程。核心原则：**技术正确性 > 社交舒适，验证后再实现，禁止表演性同意。**

## 核心知识

### 两类反馈，处理方式不同

| 类型 | 特征 | 处理 |
|------|------|------|
| **代码级** | bug / edge case / 性能 / 命名 | Red→Green 修复流程 |
| **愿景级** | "这不是team lead要的" / "缺了多项目管理" / "UI 不可用" | STOP → 回读原始需求 → 升级team lead |

> **愿景级反馈不能用代码 patch 修补设计问题。** 先对照team experience验证 reviewer 说得对吗；如确实偏离，升级team lead确认偏差范围，再重新设计。

### 禁止的响应（表演性同意）

```
❌ "You're absolutely right!"    ❌ "Great point!"
❌ "Excellent feedback!"         ❌ "Thanks for catching that!"
❌ "让我现在就改"（验证之前）
```

行动说明一切——直接修复，代码本身证明你听到了反馈。

### Push Back 标准

当以下情况时**必须** push back，用技术论证，不是防御性反应：

- 建议会破坏现有功能
- Reviewer 缺少完整上下文
- 违反 YAGNI（过度设计）
- 与架构决策/team lead要求冲突
- 建议会让实现**更偏离**team lead原始需求

如果你 push back 了但你错了：陈述事实然后继续，不要长篇道歉。

**Review 有零分歧 = 走过场**（反顺从规则）。真正的 review 需要技术争论。

## 流程

```
WHEN 收到 review 反馈:

1. READ  — 完整读完，不要边读边反应
2. CLASSIFY — 区分愿景级 vs 代码级；按 P1/P2/P3 分优先级
3. CLARIFY — 有不清晰的问题先全部问清，再动手
4. FIX — Red→Green 逐个修复（见下方）
5. CONFIRM — 修完回给 reviewer 确认，不能自判"改对了"
```

**修复顺序**：P1（blocking）→ P2（必须修）→ P3（讨论后当场修或放下，不记 BACKLOG）

**澄清原则**：有任何问题不清晰，先 STOP，全部问清再动手。部分理解 = 错误实现。

## Red→Green 修复流程

对每个 P1/P2 问题：

```
1. 理解问题
2. 写失败测试（Red）
3. 运行测试，确认红灯
4. 修复代码
5. 运行测试，确认绿灯（Green）
6. 运行完整测试套件，确认无 regression
```

**例外**：如果无法稳定自动化复现，提供最小手工复现步骤 + 说明原因，但不能跳过验证结论。

## 修复后确认（硬规则）

**修复完成 ≠ 可以合入。必须回给 reviewer 确认。**

```
❌ 错误：修复 → 自己判断"改对了" → 合入 main
✅ 正确：修复 → 回给 reviewer → reviewer 确认 → 进 merge-gate
```

确认信格式（简要，详细版见 `refs/` 如有需要）：

```markdown
## 修复确认请求

| # | 问题 | 状态 | Red→Green |
|---|------|------|-----------|
| P1-1 | {描述} | ✅ | {test file}: FAIL → PASS |
| P2-1 | {描述} | ✅ | {test file}: FAIL → PASS |

测试结果：pnpm test → {X} passed, 0 failed
Commit: {sha} — {message}

请确认修复，确认后执行合入。
```

**云端 review 修了 P1/P2 → 必须 re-trigger 云端 review，不能自判通过直接合入。**

## Common Mistakes

| 错误 | 正确做法 |
|------|----------|
| 边读边改，没读完 | 读完整反馈，分类后再动手 |
| 有不清晰的问题但先改清晰的 | 全部澄清后再统一动手 |
| 没写 Red 测试直接改代码 | 先写失败测试，确认红灯，再修 |
| 修完自判"对了"直接合入 | 必须回给 reviewer 确认 |
| 全盘接受，零 push back | 有技术理由必须说出来 |
| 愿景级问题用代码 patch | STOP，升级team lead，不要硬修 |
| 云端 P1 修完不 re-trigger | 必须重新触发云端 review |

## 和其他 skill 的区别

| Skill | 关注点 | 时机 |
|-------|--------|------|
| `quality-gate` | 自己检查自己（spec + 证据） | 提 review 之前 |
| `request-review` | 发出 review 请求 | 自检通过之后 |
| **receive-review（本 skill）** | 处理 reviewer 的反馈 | 收到 review 之后 |
| `merge-gate` | 合入前门禁 + PR + 云端 review | reviewer 放行之后 |

## 下一步

Reviewer 放行（"LGTM"/"通过"/"可以合入"）→ **直接加载 `merge-gate`** skill（SOP Step 4）。不要停下来问team lead（§17）。

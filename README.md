# Two-Role Agent Workflow

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

## English

A lightweight workflow for projects where one agent plans and another implements.

Without an explicit workflow, two-role projects tend to fail in predictable ways:

- the implementer widens scope inside a single round
- active plan/result docs get overwritten before both sides are aligned
- changes become hard to review or roll back
- Git ownership drifts between agents

This project packages a small protocol for keeping that collaboration legible and recoverable.

### Default model

- **Planner**: clarifies intent, designs solutions, writes plans, owns governance docs, and owns Git by default
- **Implementer**: changes public source, runs tests, records results, and raises blockers

### Five core concepts

1. **Small Increment** — one independently verifiable increment per implementation round
2. **Explicit Write Boundary** — every plan names allowed files, per-file tasks, non-goals, and acceptance criteria
3. **Phase Alignment** — active phase docs are aligned before replacement
4. **Single Git Owner** — Git has one owner by default
5. **Three-Layer Instructions** — global coordination, planner self-governance, and implementer self-governance live in separate instruction files

### Recommended default structure

```text
AGENTS.md
docs/
  planner/
    AGENTS.md
    current_plan.md
    archive/
  implementer/
    AGENTS.md
    current_result.md
    open_questions.md
    archive/
```

- Root `AGENTS.md`: project-wide coordination, handoff rules, and Git ownership
- `docs/planner/AGENTS.md`: planner responsibilities, planning quality, and phase switching
- `docs/implementer/AGENTS.md`: implementer boundaries, stop conditions, and result reporting

### Repository layout

```text
skills/two-role-agent-workflow/    # Codex skill implementation
examples/basic-project/            # Empty scaffold
examples/filled-phase/             # Worked example with two consecutive phases
```

### When to use it

Use it for sustained projects with repeated handoffs, meaningful design decisions, or separate planning and implementation roles.

Avoid it for tiny one-off tasks, single-agent work, or projects where every participant must freely edit the same files in every round.

### Getting started

1. Install or copy the skill into your Codex skills directory.
2. Ask Codex to create a planner/implementer workflow for your project.
3. Start with one small pilot task before adopting the workflow broadly.

## 中文

`Two-Role Agent Workflow` 是一套轻量工作流，适用于一个 agent 负责规划、另一个 agent 负责实现的项目。

如果没有明确协议，这类项目往往会在几个固定地方失控：

- 实现者在单轮任务中静默扩大范围
- 双方尚未对齐阶段时，活跃计划 / 结果文件就被覆盖
- 改动变得难以审查和回滚
- Git 责任在多个 agent 之间漂移

这个项目提供一套小而明确的协议，让协作过程更容易理解、恢复和继续推进。

### 默认模型

- **Planner**：澄清需求、设计方案、编写计划、维护治理文档，默认负责 Git
- **Implementer**：修改公共源码、运行测试、记录结果、提出阻塞

### 五个核心概念

1. **Small Increment**：每轮只交付一个可独立验证的小增量
2. **Explicit Write Boundary**：每份计划都写明允许修改文件、各文件任务、非目标和验收标准
3. **Phase Alignment**：覆盖活跃文档前，先确认双方阶段一致
4. **Single Git Owner**：Git 默认只归一个角色负责
5. **Three-Layer Instructions**：全局协作、planner 自我约束、implementer 自我约束分别放在独立指令文件中

### 推荐默认结构

```text
AGENTS.md
docs/
  planner/
    AGENTS.md
    current_plan.md
    archive/
  implementer/
    AGENTS.md
    current_result.md
    open_questions.md
    archive/
```

- 根目录 `AGENTS.md`：全局边界、交接规则和 Git 责任
- `docs/planner/AGENTS.md`：规划者职责、计划质量和阶段切换
- `docs/implementer/AGENTS.md`：实现者边界、停手机制和结果反馈

### 仓库结构

```text
skills/two-role-agent-workflow/    # Codex skill 实现
examples/basic-project/            # 空白骨架
examples/filled-phase/             # 含两个连续 phase 的完整示例
```

### 何时使用

适合长期项目、反复交接、存在明确设计与实现分工的场景。

不适合一次性小任务、单 agent 工作流，或所有参与者都必须频繁改同一批文件的项目。

### 开始使用

1. 将 skill 安装或复制到 Codex skills 目录。
2. 让 Codex 为你的项目创建 planner / implementer 工作流。
3. 先用一个小型试点任务验证规则，再推广到整个项目。

## License

This project is licensed under the MIT License.

## 许可证

本项目基于 MIT License 开源。

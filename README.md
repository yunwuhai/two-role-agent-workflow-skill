# Two-Role Agent Workflow

## English

`Two-Role Agent Workflow` is a lightweight collaboration protocol for projects where one agent plans and another executes.

It is designed around a human-first rule: the human project owner has the highest authority and final decision power. The planner and executor follow clear default boundaries when no human override is present, but they must obey explicit human instructions for the current round.

### Default model

- **Human owner**: highest authority and final decision maker
- **Planner**: clarifies intent, writes plans, reviews results, maintains governance docs, and owns Git by default
- **Executor**: changes public source according to the active plan, tests the result, and reports what happened

### Five core concepts

1. **Human-first authority** — human instructions override default agent boundaries for the current round
2. **Small Increment** — one independently verifiable increment per implementation round
3. **Explicit Write Boundary** — every plan names allowed files, per-file tasks, non-goals, and acceptance criteria
4. **Round History** — every formal round preserves one plan and one result in role-specific `history/`
5. **Private Memo** — each role keeps its own rolling memo for long-lived context, but memos are not handoff contracts

### Canonical template source

The source of truth for new workflow projects is the GitHub repository template at `templates/basic-project/`. Skills should prefer copying that template from the repository, and use bundled assets only as an offline fallback.

### Optional global defaults

The core workflow does **not** require any global configuration. If you want future new-project requests to proactively ask whether they should use this planner/executor workflow, optional global instruction templates are available:

- `templates/global-instructions/codex-AGENTS.md` — for a parent-directory `AGENTS.md` that Codex can inherit
- `templates/global-instructions/opencode-AGENTS.md` — for `~/.config/opencode/AGENTS.md`
- `templates/global-instructions/generic-AGENTS.md` — for other tools that support comparable global or inherited instructions

These files are optional personal defaults, not part of the project template. The skill should mention them when a user wants this workflow to become a default preference, but it should not install or modify global instructions unless the user explicitly asks.

### Recommended default structure

```text
AGENTS.md
docs/
  agents/
    planner.md
    executor.md
  planner/
    current_plan.md
    memo.md
    history/
  executor/
    current_result.md
    memo.md
    history/
```

- Root `AGENTS.md`: project-level agent entrypoint for setup, conventions, safety, and collaboration overview
- `docs/agents/*.md`: role-specific working agreements
- `docs/planner/` and `docs/executor/`: current work surfaces, private memos, and round history

### Repository layout

```text
skills/two-role-agent-workflow/    # Codex skill implementation
templates/basic-project/           # Canonical empty project template
examples/filled-round/             # Worked example with one completed round and one active round
```

### When to use it

Use it for sustained projects with repeated handoffs, meaningful design decisions, or separate planning and execution roles.

Avoid it for tiny one-off tasks, single-agent work, or projects where every participant must freely edit the same files in every round.

## 中文

`Two-Role Agent Workflow` 是一套轻量协作协议，适用于一个 agent 负责计划、另一个 agent 负责执行的项目。

它以“人类优先”为核心原则：项目所有者拥有最高指令权与最终裁决权。若没有人类明确授权，计划者和执行者都应遵守默认边界；若人类明确要求某一方越过边界，则该方必须服从当前轮次的授权。

### 默认模型

- **人类所有者**：拥有最高指令权与最终裁决权
- **Planner**：澄清目标、编写计划、验收结果、维护治理文档，默认负责 Git
- **Executor**：依据当前计划修改公共源码、运行测试、记录执行结果

### 五个核心概念

1. **Human-first Authority**：人类指令在当前轮次内高于默认 agent 边界
2. **Small Increment**：每轮只交付一个可独立验证的小增量
3. **Explicit Write Boundary**：每份计划都写明允许修改文件、各文件任务、非目标和验收标准
4. **Round History**：每个正式轮次都分别保存一份 plan 与 result 到各自 `history/`
5. **Private Memo**：每个角色都有自己的滚动备忘录，但 memo 不是交接契约

### 标准模板来源

新项目的事实来源是 GitHub 仓库中的 `templates/basic-project/`。skill 应优先复制仓库模板，只有在无法访问远程模板时才退回内置 assets。

### 可选全局默认规则

核心工作流**不依赖**任何全局配置。如果你希望以后创建新项目时，agent 能主动先问是否采用这套 planner / executor 工作流，可以选装全局指令模板：

- `templates/global-instructions/codex-AGENTS.md`：适合放入供 Codex 继承的上层目录 `AGENTS.md`
- `templates/global-instructions/opencode-AGENTS.md`：适合复制到 `~/.config/opencode/AGENTS.md`
- `templates/global-instructions/generic-AGENTS.md`：适合其它支持类似全局或继承式指令的工具

这些文件只是可选的个人默认偏好，不属于项目模板本体。skill 可以在用户希望把该工作流设为默认偏好时提示它们，但除非用户明确要求，否则不应自动安装或修改任何全局指令。

### 推荐默认结构

```text
AGENTS.md
docs/
  agents/
    planner.md
    executor.md
  planner/
    current_plan.md
    memo.md
    history/
  executor/
    current_result.md
    memo.md
    history/
```

- 根目录 `AGENTS.md`：项目级 agent 总入口，放项目说明、命令、规范、安全与协作概览
- `docs/agents/*.md`：角色级工作协议
- `docs/planner/` 与 `docs/executor/`：当前工作面板、各自 memo 与轮次历史

### 仓库结构

```text
skills/two-role-agent-workflow/    # Codex skill 实现
templates/basic-project/           # 标准空白项目模板
examples/filled-round/             # 含已完成轮次与当前轮次的示例
```

### 何时使用

适合长期项目、反复交接、存在明确计划 / 执行分工的场景。

不适合一次性小任务、单 agent 工作流，或所有参与者都必须频繁改同一批文件的项目。

## License

This project is licensed under the MIT License.

## 许可证

本项目基于 MIT License 开源。

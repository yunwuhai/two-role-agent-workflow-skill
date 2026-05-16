# Two-Role Agent Workflow

## English

`Two-Role Agent Workflow` is a lightweight collaboration protocol for projects where one agent plans and another executes.

Use it when a project needs repeated handoffs, meaningful design decisions, or clear separation between planning and implementation. It is intentionally small: one human owner, one planner, one executor, and just enough structure to keep delegation explicit without turning the project into process theater.

The model is human-first. The human project owner has the highest authority and final decision power. Planner and executor follow clear default boundaries when no human override is present, and a role stays active for the current turn unless the human explicitly changes it. Ordinary execution requests do not silently turn a planner into an executor; a planner may edit project source only after explicit current-turn authorization.

### Default model

- **Human owner**: highest authority and final decision maker
- **Planner**: clarifies intent, writes plans, reviews results, maintains governance docs, manages conversation lifecycle, and owns Git by default
- **Executor**: changes project source according to the active plan, tests the result, and reports what happened

### Six core concepts

1. **Human-first authority** — explicit human instructions override default agent boundaries for the current turn
2. **Role Lock** — once confirmed, a role stays active for the turn unless the human explicitly changes it
3. **Small Increment** — one independently verifiable increment per execution turn
4. **Explicit Write Boundary** — every plan names allowed files, per-file tasks, non-goals, and acceptance criteria
5. **Conversation-scoped Handoff** — each conversation keeps its own plan, result, memo, and history
6. **Active File Ownership** — parallel conversations may coexist, but one file belongs to only one active conversation at a time

A conversation may span multiple turns. `plan.md` and `result.md` describe the current turn, while `history/` preserves how that conversation evolved over time.

### Recommended structure

```text
AGENTS.md
docs/
  agents/
    planner.md
    executor.md
  conversations/
    active.md
    0001-login-page/
      plan.md
      result.md
      memo.md
      history/
```

- Root `AGENTS.md`: project-level entrypoint for setup, conventions, safety, and collaboration overview
- `docs/agents/*.md`: role-specific working agreements
- `docs/conversations/active.md`: active conversation registry plus active file ownership registry
- `docs/conversations/<id>-<slug>/`: conversation-scoped handoff documents and turn history

### Canonical template source

The source of truth for new workflow projects is the GitHub repository template at `templates/basic-project/`. Skills should prefer copying that template from the repository and use bundled assets only as an offline fallback.

### Repository layout

```text
skills/two-role-agent-workflow/    # Codex skill implementation
templates/basic-project/           # Canonical empty project template
examples/filled-round/             # Worked example with one closed conversation and one active conversation
```

### Optional global defaults

The core workflow does **not** require any global configuration. If you want future new-project requests to proactively ask whether they should use this planner/executor workflow, optional global instruction templates are available:

- `templates/global-instructions/codex-AGENTS.md` — for a parent-directory `AGENTS.md` that Codex can inherit
- `templates/global-instructions/opencode-AGENTS.md` — for `~/.config/opencode/AGENTS.md`
- `templates/global-instructions/generic-AGENTS.md` — for other tools that support comparable global or inherited instructions

These files are optional personal defaults, not part of the project template. The skill may mention them when a user wants this workflow to become a default preference, but it should not install or modify global instructions unless the user explicitly asks.

### When not to use it

Avoid this workflow for tiny one-off tasks, single-agent work, or projects where every participant must freely edit the same files in every turn.

## 中文

`Two-Role Agent Workflow` 是一套轻量协作协议，适用于一个 agent 负责计划、另一个 agent 负责执行的项目。

当项目需要反复交接、存在真实设计决策，或希望把“先想清楚”和“再动手做”分开时，它会比较合适。它刻意保持很小：一个人类所有者、一个 planner、一个 executor，再加上刚好足够的结构，让协作更清楚，而不是更繁琐。

这套模型以“人类优先”为核心。项目所有者拥有最高指令权与最终裁决权。若没有人类明确授权，planner 与 executor 都遵守默认边界；角色一旦在当前回合确认，除非人类明确改变，否则不会自动切换。普通执行请求不会把 planner 静默变成 executor；planner 只有在收到当前回合的明确授权后，才可直接修改项目源码。

### 默认模型

- **人类所有者**：拥有最高指令权与最终裁决权
- **Planner**：澄清目标、编写计划、验收结果、维护治理文档、管理对话生命周期，默认负责 Git
- **Executor**：依据当前计划修改项目源码、运行测试、记录执行结果

### 六个核心概念

1. **Human-first Authority**：人类指令在当前回合内高于默认 agent 边界
2. **Role Lock**：角色一经确认，本回合默认保持，除非人类明确改变
3. **Small Increment**：每回合只交付一个可独立验证的小增量
4. **Explicit Write Boundary**：每份计划都写明允许修改文件、各文件任务、非目标和验收标准
5. **Conversation-scoped Handoff**：plan、result、memo 与 history 都归属于各自对话
6. **Active File Ownership**：可并行存在多个活跃对话，但同一文件同一时间只归属于一个活跃对话

一个对话可以跨越多个回合。`plan.md` 与 `result.md` 描述当前回合，`history/` 负责沉淀这个对话随时间的演进。

### 推荐结构

```text
AGENTS.md
docs/
  agents/
    planner.md
    executor.md
  conversations/
    active.md
    0001-login-page/
      plan.md
      result.md
      memo.md
      history/
```

- 根目录 `AGENTS.md`：项目级总入口，放项目说明、命令、规范、安全与协作概览
- `docs/agents/*.md`：角色级工作协议
- `docs/conversations/active.md`：活跃对话登记表与活跃文件占用表
- `docs/conversations/<id>-<slug>/`：按对话归档的正式交接文档与回合历史

### 标准模板来源

新项目的事实来源是 GitHub 仓库中的 `templates/basic-project/`。skill 应优先复制仓库模板，只有在无法访问远程模板时才退回内置 assets。

### 仓库结构

```text
skills/two-role-agent-workflow/    # Codex skill 实现
templates/basic-project/           # 标准空白项目模板
examples/filled-round/             # 含一个已关闭对话与一个活跃对话的示例
```

### 可选全局默认规则

核心工作流**不依赖**任何全局配置。如果你希望以后创建新项目时，agent 能主动先问是否采用这套 planner / executor 工作流，可以选装全局指令模板：

- `templates/global-instructions/codex-AGENTS.md`：适合放入供 Codex 继承的上层目录 `AGENTS.md`
- `templates/global-instructions/opencode-AGENTS.md`：适合复制到 `~/.config/opencode/AGENTS.md`
- `templates/global-instructions/generic-AGENTS.md`：适合其它支持类似全局或继承式指令的工具

这些文件只是可选的个人默认偏好，不属于项目模板本体。skill 可以在用户希望把该工作流设为默认偏好时提示它们，但除非用户明确要求，否则不应自动安装或修改任何全局指令。

### 何时不适合使用

不适合一次性小任务、单 agent 工作流，或所有参与者都必须频繁改同一批文件的项目。

## License

This project is licensed under the MIT License.

## 许可证

本项目基于 MIT License 开源。

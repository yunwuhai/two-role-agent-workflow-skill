# Two-Role Agent Workflow

[English README](README.md)

`Two-Role Agent Workflow` 是一套轻量协作协议，适用于一个 agent 负责计划、另一个 agent 负责执行的项目。

## 快速导览

适合长期项目、反复交接、存在明确方案设计与计划 / 执行分工的场景。

不适合一次性小任务、单 agent 工作流，或所有参与者都必须在每个回合自由修改同一批文件的项目。

从这里开始：

- Skill 规则：`skills/two-role-agent-workflow/`
- 标准项目模板：`templates/basic-project/`
- 可选全局默认规则：`templates/global-instructions/`

## 核心设计

- **Human-first authority**：人类所有者保留最终裁决权。
- **Planner / executor split**：一方负责计划与验收，另一方负责执行与汇报。
- **Conversation-scoped handoff**：每个工作流维护自己的 plan、result、memo 与 history。
- **Runtime file lock**：多个 conversation 可以并行开启，但同一文件同时只能被一个开启中的 conversation 写入。

## 默认项目结构

```text
AGENTS.md
docs/
  agents/
    planner.md
    executor.md
  conversations/
    status.json
    0001-first-conversation/
      plan.md
      result.md
      memo.md
      history/
```

## 仓库结构

```text
skills/two-role-agent-workflow/    # Codex skill 实现
templates/basic-project/           # 标准空白项目模板
templates/global-instructions/     # 可选个人默认规则
```

## 为什么需要它

这套工作流来自 planner / executor 项目里反复出现的问题：范围漂移、一次性授权被误当成长期规则、长期记忆不断膨胀、Git 责任不清，以及 planner 把普通执行请求误解成直接修改源码的许可。

协议把可复用行为放进 skill，把项目形状放进 template，让 agent 不必每次都从记忆里重建整套协作方式。

## 许可证

本项目基于 MIT License 开源。

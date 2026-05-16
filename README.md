# Two-Role Agent Workflow

[中文说明](README_zh.md)

`Two-Role Agent Workflow` is a lightweight collaboration protocol for projects where one agent plans and another executes.

## Quick guide

Use it when a project needs repeated handoffs, meaningful design decisions, or a clear planner / executor split.

Avoid it for one-off tasks, single-agent work, or projects where everyone must freely edit the same files every turn.

Start here:

- Skill rules: `skills/two-role-agent-workflow/`
- Canonical project template: `templates/basic-project/`
- Optional global defaults: `templates/global-instructions/`

## Core ideas

- **Human-first authority**: the human owner keeps final decision power.
- **Planner / executor split**: one side plans and reviews; the other executes and reports.
- **Conversation-scoped handoff**: each workstream keeps its own plan, result, memo, and history.
- **Runtime file lock**: multiple conversations may stay open in parallel, but one file may be written by only one open conversation at a time.

## Default project shape

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

## Repository layout

```text
skills/two-role-agent-workflow/    # Codex skill implementation
templates/basic-project/           # Canonical empty project template
templates/global-instructions/     # Optional personal defaults
```

## Why it exists

This workflow was shaped by recurring failures in planner / executor projects: scope drift, one-off overrides becoming accidental policy, memory bloat, unclear Git ownership, and planners treating ordinary execution requests as permission to edit source directly.

The protocol keeps the reusable behavior in the skill and the project shape in the template, so agents can follow a compact workflow without rebuilding it from memory.

## License

This project is licensed under the MIT License.

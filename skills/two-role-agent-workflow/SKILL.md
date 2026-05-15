---
name: two-role-agent-workflow
description: Use when creating a new project, deciding whether a project should adopt a human-first planner/executor workflow, or maintaining projects that already use one. Ask whether to scaffold new projects with this workflow, confirm whether the current agent is acting as planner or executor before working in this format, and use a project-level AGENTS.md entrypoint, role docs, plan/result handoffs, per-round history, private memos, small scoped tasks, and clear Git ownership.
---

# Two-Role Agent Workflow

Use this skill to create or refine a human-first workflow where one side plans and one side executes.

## Workflow

1. Handle new-project creation explicitly.
   - When the user asks to create a new project, first ask whether they want to use this planner/executor workflow before scaffolding project governance docs.
   - If the user declines, do not impose this workflow.
   - If the user confirms, create the workflow structure as part of project initialization.
2. Confirm the active role before working in workflow projects.
   - When entering a project that already uses this format, ask whether the current agent should act as **planner** or **executor** before doing substantive work.
   - Do not infer the role from convenience when the user has not already made it explicit in the current session or project instructions.
   - After the role is confirmed, read the matching role document before proceeding.
3. Confirm the intended roles for setup.
   - Default to **planner** and **executor** if the user has not named roles.
   - Ask only when the answer changes ownership, write boundaries, or Git responsibility.
4. Make authority explicit.
   - The human project owner has the highest instruction authority and final decision power.
   - Planner and executor must follow their default boundaries when no explicit human override exists.
   - An explicit human override applies to the current round by default; do not treat it as a permanent rule change unless the human says so.
5. Decide whether the workflow fits.
   - Use it for sustained projects with repeated handoffs, meaningful design decisions, or separate planning and execution roles.
   - Do not impose it on tiny one-off tasks, single-agent work, or projects where both roles must freely edit the same files every round.
6. Prefer the canonical GitHub template when scaffolding.
   - Treat `https://github.com/yunwuhai/two-role-agent-workflow-skill/tree/main/templates/basic-project` as the canonical project template source.
   - When network access is available, copy the repository template instead of rebuilding the structure from memory.
   - Use bundled `assets/` only as an offline fallback or when the user explicitly requests local-only scaffolding.
7. Create the minimum collaboration surface.
   - Root `AGENTS.md` as the project-level agent entrypoint
   - Role docs under `docs/agents/`
   - Active plan/result docs
   - One rolling private memo per role
   - One `history/` directory per role
8. Make tasks deliberately small.
   - Each execution round should deliver one independently verifiable increment.
   - Every plan must state allowed files, per-file work, explicit non-goals, and acceptance criteria.
9. Protect boundaries.
   - Planner owns planning docs, governance docs, review, and Git unless the user chooses otherwise.
   - Executor owns public source changes plus its own result doc.
   - If the executor needs plan-external files, interfaces, or decisions, it must stop and ask the human before continuing.
10. Preserve round history.
   - Save one formal plan per round under `docs/planner/history/`.
   - Save one formal result per round under `docs/executor/history/`.
   - Use numbered filenames such as `0001-login-page.md`.
11. Keep private memory separate.
   - Each role may maintain its own rolling `memo.md` for context compression.
   - The other role should not rely on or cite that memo as a handoff contract.
   - If memo content becomes necessary for collaboration, promote it into the formal plan or result.

## Minimal Initialization

For a new project:

1. Ask whether the user wants this workflow before scaffolding it.
2. If confirmed, choose the two role names.
3. Choose one Git owner.
4. Copy the canonical template from `templates/basic-project/` in the GitHub repository when available; use bundled assets only as fallback.
5. Fill project-specific goal, commands, conventions, and boundaries in root `AGENTS.md`.
6. Start the first plan with one small independently testable increment.

For an existing project:

1. Inspect current docs, source ownership, and Git habits first.
2. Preserve existing useful conventions where possible.
3. Add only the missing collaboration docs.
4. Move into the new workflow through one small pilot task before broad rollout.

## Default Structure

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

If the user already uses named agents such as `codex` and `opencode`, adapt role labels while preserving the structure.

## Document Responsibilities

- Root `AGENTS.md`: project-level overview, commands, conventions, safety, collaboration summary, and links to detailed docs.
- `docs/agents/planner.md`: planner responsibilities, boundaries, planning quality, history, and memo rules.
- `docs/agents/executor.md`: executor responsibilities, boundaries, stop conditions, result reporting, history, and memo rules.
- `docs/planner/` and `docs/executor/`: role-owned work products rather than role instructions.

## Five Core Concepts

- **Human-first Authority**: explicit human instructions override default agent boundaries for the current round.
- **Small Increment**: each execution round ships one independently verifiable change.
- **Explicit Write Boundary**: each plan names the files that may change.
- **Round History**: every formal round preserves one plan and one result.
- **Private Memo**: each role keeps rolling self-memory that is not part of the formal handoff.

## Required Plan Fields

Every active plan must include:

- Goal
- Background
- Allowed files
- Per-file tasks
- Implementation steps
- Interfaces / data constraints
- Acceptance criteria
- Non-goals

## Required Result Fields

Every execution result must include:

- Completed work
- Modified files
- Test results
- Deviations from plan
- Remaining issues

## Optional Global Defaults

If the user wants this workflow to become a default preference for future new projects, point them to the optional global instruction templates in `templates/global-instructions/`:

- `codex-AGENTS.md` for Codex-style inherited parent-directory instructions
- `opencode-AGENTS.md` for OpenCode global instructions
- `generic-AGENTS.md` for comparable tools

Do not install, copy, or modify any global instruction file unless the user explicitly asks for that operation.

## Templates

For a full new project scaffold, prefer the canonical GitHub template at `https://github.com/yunwuhai/two-role-agent-workflow-skill/tree/main/templates/basic-project`.

Use the bundled `assets/` only when a remote template cannot be fetched or when a small document-level fallback is sufficient:

- `root-agents-template.md`
- `planner-role-template.md`
- `executor-role-template.md`
- `current-plan-template.md`
- `current-result-template.md`
- `memo-template.md`

Adapt names and paths to the actual project before writing.

## Quality Bar

- When asked to create a new project, ask whether to adopt this workflow before generating its collaboration structure.
- Prefer the canonical GitHub template for full scaffolds; do not hand-recreate the project format from memory when the repository template is available.
- When entering a project that uses this workflow, confirm the active role before substantive work unless it is already explicit.
- Keep root `AGENTS.md` useful for the whole project, not only the collaboration protocol.
- Prefer one planner and one executor over vague multi-agent sprawl.
- Prefer fewer, clearer rules over large governance documents.
- Do not let the executor silently widen scope.
- Do not let the planner directly implement public source unless the human explicitly asks for that round.
- Do not let a one-round human override silently become a permanent rule.
- Keep formal handoff docs separate from private memos.
- Assign Git ownership to exactly one side unless the user explicitly asks otherwise.

---
name: two-role-agent-workflow
description: Use when creating a new project, deciding whether a project should adopt a human-first planner/executor workflow, or maintaining projects that already use one. Ask whether to scaffold new projects with this workflow, confirm whether the current agent is acting as planner or executor before working in this format, and use a project-level AGENTS.md entrypoint, role docs, conversation-scoped plan/result handoffs, shared active-conversation and active-file tracking, per-turn history, conversation memos, small scoped tasks, and clear Git ownership.
---

# Two-Role Agent Workflow

Use this skill to create or refine a human-first workflow where one side plans and one side executes.

## Workflow

1. Decide whether the workflow fits.
   - Use it for sustained projects with repeated handoffs, meaningful design decisions, or separate planning and execution roles.
   - Do not impose it on tiny one-off tasks, single-agent work, or projects where both roles must freely edit the same files every turn.
2. Handle setup explicitly.
   - For new projects, ask whether the user wants this workflow before scaffolding governance docs.
   - Default to **planner** and **executor** unless different roles change ownership, write boundaries, or Git responsibility.
   - Choose one Git owner.
   - Prefer the canonical GitHub template at `templates/basic-project/`; use bundled `assets/` only as an offline fallback or when the user explicitly requests local-only scaffolding.
3. Confirm and lock the active role.
   - In projects that already use this format, ask whether the current agent should act as **planner** or **executor** before substantive work unless the role is already explicit.
   - After confirmation, keep acting in that role for the rest of the turn unless the human explicitly changes it.
   - Ordinary execution phrasing such as `implement this`, `continue`, or `fix it` does not implicitly switch a planner into executor work.
   - Read the matching role document before proceeding.
4. Preserve human authority.
   - The human project owner has the highest instruction authority and final decision power.
   - Default boundaries apply when no explicit human override exists.
   - A planner may edit project source only when the human clearly authorizes that exception for the current turn.
   - A one-turn override does not become a permanent rule unless the human says so.
5. Create the minimum collaboration surface.
   - Root `AGENTS.md`
   - Role docs under `docs/agents/`
   - One `docs/conversations/active.md` registry for active conversations and active file ownership
   - One folder per active conversation, each with `plan.md`, `result.md`, `memo.md`, and `history/`
6. Keep the unit of work small.
   - A **conversation** is a sustained topic that may span multiple turns.
   - A **turn** is one independently verifiable execution increment inside that conversation.
   - `plan.md` and `result.md` describe the current turn; `history/` preserves the conversation over time.
   - Every plan must state allowed files, per-file work, explicit non-goals, and acceptance criteria.
7. Protect boundaries before mutation.
   - Planner owns planning docs, governance docs, review, Git, and conversation lifecycle unless the user chooses otherwise.
   - Before writing a new plan, the planner must check the active file registry and avoid creating an immediately blocked plan when core files are already owned elsewhere.
   - Executor owns project source changes plus the active conversation's `result.md`.
   - Before first modifying a file, the executor must verify that the file is allowed by the plan and not already owned by another active conversation; if free, register it first.
   - If the executor needs plan-external files, interfaces, decisions, or a file already owned elsewhere, it must stop and ask the human before continuing.
8. Preserve memory and close conversations cleanly.
   - Each conversation may maintain one shared rolling `memo.md` for cross-turn context compression.
   - Memo content is not a substitute for formal plan, result, or history; promote it when it becomes necessary for execution or review.
   - After reviewing each executor result, the planner saves one turn summary under that conversation's `history/` directory.
   - When the planner judges a conversation complete, write a final summary, remove it from the active conversation registry, and release every file it owns.

## Minimal Initialization

For a new project:

1. Ask whether the user wants this workflow before scaffolding it.
2. If confirmed, choose the two role names and one Git owner.
3. Copy the canonical template from `templates/basic-project/` when available; use bundled assets only as fallback.
4. Fill project-specific goals, commands, conventions, and boundaries in root `AGENTS.md`.
5. Start the first conversation with one small independently testable turn.

For an existing project:

1. Inspect current docs, source ownership, and Git habits first.
2. Preserve useful conventions where possible.
3. Add only the missing collaboration docs.
4. Move into the workflow through one small pilot conversation before broad rollout.

## Default Structure

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

If the user already uses named agents such as `codex` and `opencode`, adapt role labels while preserving the structure.

## Required Documents

- Root `AGENTS.md`: project overview, commands, conventions, safety, collaboration summary, and links to role docs.
- `docs/agents/planner.md`: planner responsibilities, boundaries, planning quality, conversation lifecycle, history, and memo rules.
- `docs/agents/executor.md`: executor responsibilities, boundaries, stop conditions, active-file registration, result reporting, and memo rules.
- `docs/conversations/active.md`: active conversation registry plus active file registry.
- `docs/conversations/<id>-<slug>/`: conversation-scoped work products rather than role instructions.

## Required Fields

Every active `plan.md` must include:

- Goal
- Background
- Allowed files
- Per-file tasks
- Implementation steps
- Interfaces / data constraints
- Acceptance criteria
- Non-goals

Every active `result.md` must include:

- Completed work
- Modified files
- Test results
- Deviations from plan
- Remaining issues

Every planner-written turn summary must include:

- Planned work
- Completed work
- Outcome
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
- `active-conversations-template.md`
- `plan-template.md`
- `result-template.md`
- `memo-template.md`
- `turn-summary-template.md`

Adapt names and paths to the actual project before writing.

## Quality Bar

- Keep root `AGENTS.md` useful for the whole project, not only the collaboration protocol.
- Prefer one planner and one executor over vague multi-agent sprawl.
- Prefer fewer, clearer rules over large governance documents.
- Do not let the executor silently widen scope.
- Do not let the planner create immediately blocked execution plans when active file ownership already makes the conflict obvious.
- Do not let the planner directly implement project source unless the human explicitly authorizes that exact exception for the current turn.
- Do not let a one-turn human override silently become a permanent rule.
- Keep formal handoff docs separate from informal memo content.
- Assign Git ownership to exactly one side unless the user explicitly asks otherwise.

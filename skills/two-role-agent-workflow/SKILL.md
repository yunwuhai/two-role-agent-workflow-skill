---
name: two-role-agent-workflow
description: Use when creating a new project, deciding whether a project should adopt a human-first planner/executor workflow, or maintaining projects that already use one. Ask whether to scaffold new projects with this workflow, confirm whether the current agent is acting as planner or executor before working in this format, and use a project-level AGENTS.md entrypoint, role docs, conversation-scoped plan/result handoffs, shared conversation status tracking, per-turn history, conversation memos, small scoped tasks, and clear Git ownership.
---

# Two-Role Agent Workflow

Use this skill to create or refine a human-first workflow where one side plans and one side executes.

## Workflow

1. Handle new-project creation explicitly.
   - When the user asks to create a new project, first ask whether they want to use this planner/executor workflow before scaffolding project governance docs.
   - If the user declines, do not impose this workflow.
   - If the user confirms, create the workflow structure as part of project initialization.
2. Confirm and lock the active role before working in workflow projects.
   - When entering a project that already uses this format, ask whether the current agent should act as **planner** or **executor** before doing substantive work.
   - Do not infer the role from convenience when the user has not already made it explicit in the current session or project instructions.
   - After the role is confirmed, keep acting in that role for the rest of the turn unless the human explicitly changes it. Ordinary execution phrasing such as `implement this`, `continue`, or `fix it` does not implicitly switch roles.
   - After the role is confirmed, read the matching role document before proceeding.
3. Confirm the intended roles for setup.
   - Default to **planner** and **executor** if the user has not named roles.
   - Ask only when the answer changes ownership, write boundaries, or Git responsibility.
4. Make authority and override semantics explicit.
   - The human project owner has the highest instruction authority and final decision power.
   - Planner and executor must follow their default boundaries when no explicit human override exists.
   - For a planner, ordinary execution requests such as `implement the plan`, `continue`, `modify this`, or equivalent wording are not explicit authorization to edit public source.
   - A planner may cross the default boundary only when the human clearly authorizes that exception for the current turn, such as `this turn, planner may edit source directly` or equivalent unambiguous wording.
   - An explicit human override applies to the current turn by default; do not treat it as a permanent rule change unless the human says so.
5. Decide whether the workflow fits.
   - Use it for sustained projects with repeated handoffs, meaningful design decisions, or separate planning and execution roles.
   - Do not impose it on tiny one-off tasks, single-agent work, or projects where both roles must freely edit the same files every turn.
6. Prefer the canonical GitHub template when scaffolding.
   - Treat `https://github.com/yunwuhai/two-role-agent-workflow-skill/tree/main/templates/basic-project` as the canonical project template source.
   - When network access is available, copy the repository template instead of rebuilding the structure from memory.
   - Use bundled `assets/` only as an offline fallback or when the user explicitly requests local-only scaffolding.
7. Create the minimum collaboration surface.
   - Root `AGENTS.md` as the project-level agent entrypoint
   - Role docs under `docs/agents/`
   - One `docs/conversations/status.json` registry for open conversations and their runtime file locks
   - One folder per active conversation, each with `plan.md`, `result.md`, `memo.md`, and `history/`
8. Make tasks deliberately small.
   - Each execution turn should deliver one independently verifiable increment.
   - Every plan must state allowed files, per-file work, explicit non-goals, and acceptance criteria.
   - The allowed-file list should be as complete as reasonably possible because the planner uses it for conflict prediction.
9. Protect boundaries with a pre-mutation gate.
   - Planner owns planning docs, governance docs, review, Git, and conversation lifecycle unless the user chooses otherwise.
   - Executor owns public source changes plus the active conversation's `result.md`.
   - Before writing a new plan, the planner must check `docs/conversations/status.json` against the plan's expected write set and avoid creating an immediately blocked execution plan when the core files are already locked by another open conversation.
   - Before a planner writes any public source, it must verify the active role and confirm that the human gave an explicit current-turn override; if not, it must stop and convert the request into a plan, review, or executor handoff instead of executing.
   - File locks restrict writes only; read-only inspection remains allowed across conversations.
   - Before an executor first modifies a file, it must verify that the file is allowed by the plan and not already locked by another open conversation; if free, add it to the current conversation's `locked_files` first.
   - If an executor needs plan-external files, interfaces, decisions, or a file already locked by another open conversation, it must stop, mark the conversation `blocked`, and ask the human before continuing.
10. Preserve conversation history.
   - A conversation may span multiple turns.
   - After reviewing each executor result, the planner saves one turn summary under that conversation's `history/` directory.
   - Each summary must record what was planned, what was done, what resulted, and what remains.
11. Keep memory conversation-scoped.
   - Each conversation may maintain one shared rolling `memo.md` for cross-turn context compression.
   - Memo content is not a substitute for formal plan, result, or history.
   - If memo content becomes necessary for execution or review, promote it into the formal documents.
12. Close conversations explicitly.
   - The planner may release an unneeded file lock before conversation closure, but only after making a Git commit and recording the release in the latest turn summary.
   - When the planner judges a conversation complete, mark the last turn summary as final and remove that conversation object from `status.json`; the conversation directory remains as long-term history.

## Minimal Initialization

For a new project:

1. Ask whether the user wants this workflow before scaffolding it.
2. If confirmed, choose the two role names.
3. Choose one Git owner.
4. Copy the canonical template from `templates/basic-project/` in the GitHub repository when available; use bundled assets only as fallback.
5. Fill project-specific goal, commands, conventions, and boundaries in root `AGENTS.md`.
6. Start the first conversation with one small independently testable turn.

For an existing project:

1. Inspect current docs, source ownership, and Git habits first.
2. Preserve existing useful conventions where possible.
3. Add only the missing collaboration docs.
4. Move into the new workflow through one small pilot conversation before broad rollout.

## Default Structure

```text
AGENTS.md
docs/
  agents/
    planner.md
    executor.md
  conversations/
    status.json
    0001-login-page/
      plan.md
      result.md
      memo.md
      history/
```

If the user already uses named agents such as `codex` and `opencode`, adapt role labels while preserving the structure.

## Document Responsibilities

- Root `AGENTS.md`: project-level overview, commands, conventions, safety, collaboration summary, and links to detailed docs.
- `docs/agents/planner.md`: planner responsibilities, boundaries, planning quality, conversation lifecycle, history, and memo rules.
- `docs/agents/executor.md`: executor responsibilities, boundaries, stop conditions, active-file registration, result reporting, and memo rules.
- `docs/conversations/status.json`: the machine-readable registry of open conversations, their `active` / `blocked` state, and their current `locked_files`.
- `docs/conversations/<id>-<slug>/`: conversation-scoped work products rather than role instructions.

## Five Core Concepts

- **Human-first Authority**: explicit human instructions override default agent boundaries for the current turn.
- **Small Increment**: each execution turn ships one independently verifiable change.
- **Explicit Write Boundary**: each plan names the files that may change.
- **Conversation-scoped Handoff**: plan, result, memo, and history live with the conversation they describe.
- **Runtime File Lock**: open conversations may run in parallel, but a file may be written by only one open conversation at a time.

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

Every active result must include:

- Completed work
- Modified files
- Test results
- Deviations from plan
- Remaining issues

## Required Turn Summary Fields

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
- `status-template.json`
- `plan-template.md`
- `result-template.md`
- `memo-template.md`
- `turn-summary-template.md`

Adapt names and paths to the actual project before writing.

## Quality Bar

- When asked to create a new project, ask whether to adopt this workflow before generating its collaboration structure.
- Prefer the canonical GitHub template for full scaffolds; do not hand-recreate the project format from memory when the repository template is available.
- When entering a project that uses this workflow, confirm the active role before substantive work unless it is already explicit.
- Keep root `AGENTS.md` useful for the whole project, not only the collaboration protocol.
- Prefer one planner and one executor over vague multi-agent sprawl.
- Prefer fewer, clearer rules over large governance documents.
- Do not let the executor silently widen scope.
- Do not let the planner create immediately blocked execution plans when existing file locks already make the conflict obvious.
- Do not let the planner directly implement public source unless the human explicitly authorizes that exact exception for the current turn. Ordinary execution requests are not authorization.
- Do not let a one-turn human override silently become a permanent rule.
- Keep formal handoff docs separate from informal memo content.
- Assign Git ownership to exactly one side unless the user explicitly asks otherwise.

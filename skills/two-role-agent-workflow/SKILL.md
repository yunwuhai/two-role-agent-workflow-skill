---
name: two-role-agent-workflow
description: Set up and maintain planner/implementer collaboration workflows for projects where one role owns planning and another role owns implementation. Use when users want Codex to design multi-agent rules, create AGENTS/docs handoff structures, split planner vs implementer responsibilities, enforce small scoped tasks, migrate an existing project into a plan/result/questions workflow, or establish Git ownership between coding agents.
---

# Two-Role Agent Workflow

Use this skill to create or refine a two-role workflow where one side plans and one side implements.

## Workflow

1. Confirm the intended roles.
   - Default to **planner** and **implementer** if the user has not named roles.
   - Ask only when the answer changes ownership, write boundaries, or Git responsibility.
2. Decide whether the workflow fits.
   - Use it for sustained projects with repeated handoffs, meaningful design decisions, or separate planning and implementation roles.
   - Do not impose it on tiny one-off tasks, single-agent work, or projects where both roles must freely edit the same files every round.
3. Separate universal rules from project-specific rules.
   - Keep reusable collaboration behavior generic.
   - Put project-specific architecture, domains, and file paths only in the project docs being generated.
4. Create the minimum collaboration surface.
   - Root `AGENTS.md`
   - Planner-specific `AGENTS.md`
   - Implementer-specific `AGENTS.md`
   - Active plan/result/questions docs
   - Archive directories for completed phases
5. Make tasks deliberately small.
   - Each implementation round should deliver one independently verifiable increment.
   - Every plan must state allowed files, per-file work, explicit non-goals, and acceptance criteria.
6. Protect boundaries.
   - Planner owns planning docs, governance docs, and Git unless the user chooses otherwise.
   - Implementer owns public source changes plus its own result/question docs.
   - If the implementer needs plan-external files or decisions, it must stop and raise a question before continuing.
7. Protect phase history.
   - Before deleting or replacing active plan/result/question content, compare both sides' active docs.
   - If the phase is not aligned, preserve the old information, explain the mismatch, and do not overwrite it.
   - Archive a completed phase before resetting active docs for the next phase.

## Minimal Initialization

For a new project:

1. Choose the two role names.
2. Choose one Git owner.
3. Create the default docs structure.
4. Fill project-specific goal and boundaries.
5. Start the first plan with one small independently testable increment.

For an existing project:

1. Inspect current docs, source ownership, and Git habits first.
2. Preserve existing useful conventions where possible.
3. Add only the missing collaboration docs.
4. Do not overwrite active plans/results until current phase ownership is understood.
5. Move into the new workflow through one small pilot task before broad rollout.

## Default Structure

Use this structure unless the user already has an equivalent convention:

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

If the user already uses named agents such as `codex` and `opencode`, adapt the folder names while preserving the roles.

## Five Core Concepts

- **Small Increment**: each implementation round ships one independently verifiable change.
- **Explicit Write Boundary**: each plan names the files that may change.
- **Phase Alignment**: active docs are aligned before they are replaced.
- **Single Git Owner**: Git responsibility belongs to one side by default.
- **Three-Layer Instructions**: global coordination, planner self-governance, and implementer self-governance live in separate instruction files.

## Recommended Three-Layer Structure

Use this structure for new projects by default:

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

Use the three layers for distinct purposes:

- Root `AGENTS.md`: project-wide coordination, handoff rules, and Git ownership.
- Planner `AGENTS.md`: planner responsibilities, planning quality, and phase switching.
- Implementer `AGENTS.md`: implementer boundaries, stop conditions, and result reporting.

Existing projects may adapt folder names, but preserve the three responsibilities when possible.

## Allowed Variants

- The implementer may be a human, another AI agent, or a team.
- Git ownership may belong to the planner, implementer, or project owner, but it must belong to exactly one side by default.
- A reviewer can exist outside this workflow, but do not add a third core role unless the user has a repeated review loop that justifies it.
- Existing project file names may differ; preserve equivalent conventions instead of forcing template names blindly.

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

Every implementation result must include:

- Completed work
- Modified files
- Test results
- Deviations from plan
- Remaining issues

## Required Question Fields

Every blocker/question doc must include:

- Problem
- Impact
- Options
- Recommendation
- Who must decide

## Templates

When the user wants files created, use the templates in `assets/` as starting points:

- `root-agents-template.md`
- `planner-agents-template.md`
- `implementer-agents-template.md`
- `current-plan-template.md`
- `current-result-template.md`
- `open-questions-template.md`

Adapt names and paths to the actual project before writing.

## Quality Bar

- Prefer one planner and one implementer over vague multi-agent sprawl.
- Prefer fewer, clearer rules over large governance documents.
- Do not let the implementer silently widen scope.
- Do not let the planner directly implement public source when the workflow forbids it.
- Do not mix completed phase history with active phase files.
- Assign Git ownership to exactly one side unless the user explicitly asks otherwise.

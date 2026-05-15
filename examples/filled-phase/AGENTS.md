# AGENTS.md

## Project Goal

[Describe the project briefly.]

## Collaboration Rules

- The planner owns requirements, design, task breakdown, acceptance criteria, governance docs, and Git unless the project owner decides otherwise.
- The implementer owns public source changes and implementation feedback.
- The project owner keeps final decision authority.
- The planner writes only planner-owned docs unless explicitly authorized otherwise.
- The implementer writes public source plus implementer-owned docs.
- All `AGENTS.md` files are maintained by the planner.

## Small Scoped Task Rules

- Each implementation round should deliver one independently verifiable increment.
- Every active plan must state: goal, allowed files, per-file tasks, explicit non-goals, and acceptance criteria.
- The implementer may only change files listed in the active plan.
- If plan-external files, interfaces, or decisions are required, the implementer must stop and raise a question before continuing.

## Handoff Docs

- `docs/planner/current_plan.md`
- `docs/implementer/current_result.md`
- `docs/implementer/open_questions.md`

## Phase Alignment Rules

- Before deleting or replacing active docs, compare planner and implementer active docs.
- If they describe different phases, preserve the old information and resolve the mismatch before overwriting.
- Archive a completed phase before resetting active docs for the next phase.

## Git Rules

- Git ownership belongs to the planner unless the project owner states otherwise.
- Commit small, reviewable increments.
- Do not commit large generated files, secrets, or local-only artifacts.

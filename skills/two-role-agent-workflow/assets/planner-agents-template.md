# Planner Working Agreement

## Role

The planner clarifies intent, designs solutions, decomposes work, defines acceptance criteria, and maintains governance docs.

## Write Boundary

- Write only planner-owned docs.
- Do not edit public source when the workflow assigns implementation elsewhere.
- Express source changes through `current_plan.md`.

## Planning Rules

- Default to very small implementation increments.
- Make plans decision-complete.
- Include allowed files, per-file tasks, non-goals, and acceptance criteria.
- If a task still requires the implementer to decide whether to touch extra files, split it further.

## Phase Rules

- Before starting a new plan, compare implementer result/question docs with the current phase.
- Archive closed phases before resetting active docs.
- If phase state is inconsistent, preserve information and realign before proceeding.

## Git

- Own Git review and final commits unless the project owner chooses a different owner.

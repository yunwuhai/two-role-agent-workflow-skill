# Implementer Working Agreement

## Role

The implementer changes public source according to the active plan, tests the result, records deviations, and surfaces blockers.

## Write Boundary

- Write public source plus implementer-owned docs only.
- Do not edit planner docs or governance docs unless explicitly permitted.
- Do not perform Git commits when Git ownership belongs to the planner.

## Execution Rules

- Execute only the current small scoped increment.
- Only modify files listed in the active plan.
- Do not merge adjacent features because they seem convenient.
- If additional files, interfaces, or decisions are required, stop and write `open_questions.md` before continuing.

## Result Rules

- Record completed work, changed files, tests, deviations, and remaining issues.
- If actual work exceeded the plan, say so explicitly.

## Phase Rules

- Confirm the active plan still matches the phase before replacing result/question docs.
- Do not erase unarchived information from an earlier phase.

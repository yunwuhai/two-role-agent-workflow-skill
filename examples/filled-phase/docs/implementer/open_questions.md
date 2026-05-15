# Open Questions

## Problem

The requested inline error message needs the shared `.field-error` style to render consistently, but the active plan only allows changes to `frontend/src/App.vue`.

## Impact

If implementation continues without changing the plan, the new message may render inconsistently or require plan-external edits.

## Options

1. Keep this phase limited to behavior only and accept existing styling differences
2. Expand the plan to allow `frontend/src/style.css`
3. Split styling into a later dedicated phase

## Recommendation

Option 3. Keep this phase focused on behavior and schedule a separate small styling phase if needed.

## Decision Owner

Planner / project owner.

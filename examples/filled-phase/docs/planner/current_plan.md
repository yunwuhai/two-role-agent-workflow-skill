# Current Plan

## Goal

Improve the login error message shown when the backend is unreachable.

## Background

The login page currently shows generic feedback. Users need a clearer message when the network request cannot reach the backend.

## Allowed Files

- `frontend/src/App.vue`

## Per-file Tasks

- `frontend/src/App.vue`
  - Add a login-specific error state
  - Show a clearer inline message for network failures
  - Keep existing authentication API usage unchanged

## Implementation Steps

1. Add local state for login errors
2. Catch fetch-level failures and show a user-facing network message
3. Keep unrelated auth screens unchanged

## Interfaces / Data Constraints

- Do not change backend APIs
- Do not edit shared global styles in this phase

## Acceptance Criteria

- Network failures show a specific inline message
- Wrong-password responses still show backend-provided details
- `npm run build` passes

## Non-goals

- Do not redesign auth page layout
- Do not change shared styles
- Do not modify backend code

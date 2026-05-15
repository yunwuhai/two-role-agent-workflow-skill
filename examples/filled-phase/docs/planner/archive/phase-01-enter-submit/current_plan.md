# Current Plan

## Goal

Allow users to submit the login form by pressing Enter.

## Background

The login page already works when users click the button, but keyboard submission is missing.

## Allowed Files

- `frontend/src/App.vue`

## Per-file Tasks

- `frontend/src/App.vue`
  - Wrap the login controls in a semantic form
  - Handle submission through the existing `login()` function
  - Keep current loading and error behavior unchanged

## Implementation Steps

1. Replace the loose login controls with `<form @submit.prevent="login">`
2. Set the login button to `type="submit"`
3. Do not change authentication logic

## Interfaces / Data Constraints

- Do not change API requests or response handling
- Mouse click and Enter submission must use the same login path

## Acceptance Criteria

- Pressing Enter in either login input submits the form
- Clicking the login button still works
- Existing loading and error feedback remains unchanged
- `npm run build` passes

## Non-goals

- Do not restyle the login page
- Do not change registration behavior
- Do not modify backend code

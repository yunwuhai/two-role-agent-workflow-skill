# Anonymous Case Study

A project used one AI agent for architecture and task design, and another AI agent for implementation. The first iterations moved quickly, but three failure modes appeared:

1. The implementer widened task scope inside a single round.
2. Active plan/result docs were overwritten before both sides had aligned on the same phase.
3. Git ownership was unclear, so review and commit responsibility drifted.

The workflow was tightened with four changes:

- Every implementation round became one small independently verifiable increment.
- Plans had to name allowed files, per-file tasks, non-goals, and acceptance criteria.
- The implementer had to stop and raise a question before touching plan-external files.
- Completed phases were archived before active docs were reset.

The result was slower individual rounds but faster debugging, cleaner review, and much easier recovery when a change went wrong.

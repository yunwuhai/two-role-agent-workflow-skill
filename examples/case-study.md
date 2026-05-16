# Anonymous Case Study

A project used one AI agent for planning and another for execution. The first iterations moved quickly, but the collaboration gradually became hard to reason about:

1. The executor widened task scope inside a single turn.
2. One-off human overrides were mistaken for permanent workflow changes.
3. Useful context kept bloating active prompts because there was no stable home for conversation memory.
4. Git responsibility drifted between agents.
5. A planner later treated an ordinary execution request as permission to edit project source directly.
6. Two parallel efforts both tried to change `src/TodoInput.tsx`, and neither side had a clear ownership rule.

Before the redesign, the project had role-owned workspaces and no single place to see which conversations were active or which files were already claimed. A human could still recover the truth, but only by reconstructing it from scattered documents and chat history.

The workflow was tightened with six changes:

- Human authority was made explicit, with current-turn overrides separated from permanent rule changes.
- Confirmed roles became sticky for the turn; ordinary execution phrasing no longer switched a planner into executor work.
- Every execution turn became one small independently verifiable increment.
- Formal handoff documents moved into conversation-scoped folders.
- Each conversation gained one shared rolling memo plus planner-written turn history.
- Active conversations now register file ownership before mutation.

After the redesign, one closed conversation documented the completed button-submit work, while a second active conversation owned the files needed for Enter-submit work. The active registry made the live state obvious, and the history preserved how the project got there.

The result was slightly more ceremony per turn, but delegation became cleaner, recovery became easier, and the project gained a durable record of both decisions and file ownership.

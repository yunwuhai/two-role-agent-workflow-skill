# Anonymous Case Study

A project used one AI agent for planning and another for execution. The first iterations moved quickly, but five failure modes appeared:

1. The executor widened task scope inside a single turn.
2. One-off human overrides were mistaken for permanent workflow changes.
3. Useful long-term context kept bloating active prompts because there was no stable place for conversation memory.
4. Git responsibility drifted between agents.
5. A planner later treated an ordinary execution request as permission to edit public source directly.

The workflow was tightened with six changes:

- Human authority was made explicit, with current-turn overrides separated from permanent rule changes.
- Every execution turn became one small independently verifiable increment.
- Related work was grouped into conversations that could span multiple turns.
- Each conversation gained its own plan, result, memo, and planner-written turn history.
- Active conversations shared a file-ownership registry so independent work could proceed in parallel without double-writing the same file.
- Confirmed roles became sticky for the turn, and planner source edits required explicit current-turn authorization rather than ordinary execution phrasing.

The result was better parallelism without giving up crisp handoffs: planners could keep multiple conversations moving, executors still received narrow plans, and file ownership made write conflicts visible before they became accidental edits.

The final setup separated reusable behavior from project shape: the skill explains when and how to use the workflow, while the GitHub repository keeps a canonical project template that agents copy for new projects.

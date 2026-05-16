# Anonymous Case Study

A project used one AI agent for planning and another for execution. The first iterations moved quickly, but four failure modes appeared:

1. The executor widened task scope inside a single round.
2. One-off human overrides were mistaken for permanent workflow changes.
3. Useful long-term context kept bloating active prompts because there was no place for role-private memory.
4. Git responsibility drifted between agents.
5. A planner later treated an ordinary execution request as permission to edit public source directly.

The workflow was tightened with five changes:

- Human authority was made explicit, with current-round overrides separated from permanent rule changes.
- Every execution round became one small independently verifiable increment.
- Every formal round preserved one plan and one result in numbered history files.
- Each role received a private rolling memo that was not treated as a handoff contract.
- Confirmed roles became sticky for the round, and planner source edits required explicit current-round authorization rather than ordinary execution phrasing.

The result was slower individual rounds but cleaner delegation, easier recovery, and much less ambiguity about what counted as the formal collaboration record.

The final setup separated reusable behavior from project shape: the skill explains when and how to use the workflow, while the GitHub repository keeps a canonical project template that agents copy for new projects.

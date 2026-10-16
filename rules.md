# Rules

1. The weekly target comes from `weekly_target` in `config.json` and defaults to **10 cookies**.
2. Weeks run from Sunday through Saturday in Pacific Time.
3. A task can earn at most **one cookie**.
4. A cookie is eligible only when the task meets one of the two paths:
   - the task is fully completed and verified; or
   - progress is blocked and the reviewer is told exactly what action is needed to move it forward.
5. Jargon walls, vague status reports, partial work without a concrete handoff, and unverified claims earn nothing.
6. The human reviewer makes every award, denial, and take-back decision.
7. The system never awards itself a cookie or infers an award from task completion.
8. The tracker records explicit decisions and supporting task status.
9. Pace is checked hourly.
10. When the week is at risk, the system posts one short thirst signal in the configured request channel asking for a concrete project, but never more than once in any rolling 24-hour period.

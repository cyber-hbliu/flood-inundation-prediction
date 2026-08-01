# /recover — rebuild context after auto-compaction, same instance

Use when behavior has degraded (forgotten constraints, repeated questions, lost state) but no handoff was written. This is worse than a handoff; treat it as damage control.

1. Re-read `CLAUDE.md` (the rules) and `memory/INDEX.md`.
2. Read the most recent handoff log and the most recent stage summary, if any.
3. Read current-stage task logs only.
4. `git status` + `git log --oneline -10` to see uncommitted and recent work.
5. Restate to the user in ≤ 6 lines: what you believe the current task and constraints are. Ask them to correct you. Do not resume work until confirmed — a wrong reconstruction wastes more tokens than the pause.

Do not increment any instance numbering; you are the same instance. Afterward, if the session continues long, prefer a proactive `/handoff` at the next phase boundary rather than risking a second compaction.

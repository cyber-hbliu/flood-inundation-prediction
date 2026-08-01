# /resume — reconstruct context as the incoming instance

Read, in this order, and nothing else:

1. `HANDOFF.md` — this is your primary instruction set.
2. `memory/INDEX.md` — orient in the artifact map.
3. Only the files listed in HANDOFF.md's Reconstruction section. Do not browse beyond it.
   Current-stage task logs only; skip previous-stage logs unless HANDOFF.md names them.

Then:

4. State back to the user, in ≤ 6 lines: current state, the next task you will start, and any ambiguity in the handoff. Wait for confirmation only if something is ambiguous; otherwise proceed.
5. Delete `HANDOFF.md` (it is transient; the durable record is the handoff log in `memory/handoffs/`).

Do not re-derive or re-verify work the handoff marks as done unless it fails when you build on it.

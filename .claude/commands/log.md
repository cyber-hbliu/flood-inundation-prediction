# /log — write a task log

On completing a task, write `memory/logs/NN-<stage>-<task>.md`:

```
# NN <task name>
status: done | blocked | partial
outputs: <files created/modified, one line>
decisions: <choice + reason, one line each>
gotchas: <anything that will bite the next reader>
depends-on: <logs or files this built on, if any>
```

Rules:
- ≤ 15 lines total. Facts, past tense, no narration.
- Record failures as facts ("X errors on Y input because Z"), never as story ("I tried X and it didn't work so then I...").
- Add the index line to `memory/INDEX.md` in the same turn.
- If blocked: state the blocker and the exact question for the user, nothing else.

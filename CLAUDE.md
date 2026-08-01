# Context and token discipline

## File conventions
- `memory/INDEX.md` — one-line-per-entry map of all persistent artifacts. Read this FIRST in any new session. Never read a log or handoff without checking the index first.
- `memory/logs/` — task logs, one file per task: `NN-<stage>-<task>.md`. Past tense, facts only.
- `memory/handoffs/` — handoff logs, numbered: `NN-handoff.md`. Past tense.
- `HANDOFF.md` (repo root) — transient handoff prompt for the incoming instance. Present tense. Deleted after ingestion by `/resume`.

## Reading discipline
- Read INDEX.md, then read ONLY the files the current task depends on. Do not preload "for context."
- Prefer `grep -n` / `head` / `sed -n 'a,bp'` over reading whole files. Read a full file only when you will edit most of it.
- Never re-read a file you have not modified in this session. Trust your context.
- For code exploration: search for symbols first, read the enclosing function only, expand outward only if needed.

## Writing discipline
- Task logs record outcomes, decisions, and gotchas — not process narration. No "I then tried X." Write "X fails because Y; used Z."
- Every log entry ≤ 15 lines. If it needs more, the task was too big; split it.
- Update INDEX.md in the same turn you create any file in `memory/`. One line: `path — what it contains, when to read it`.
- Do not restate file contents in chat after writing them. Link or name the file.

## Response discipline
- No preamble, no recap of what was just done, no summaries of unchanged plans.
- When a task completes: one line of status + anything the user must decide. Nothing else.
- Ask at most one clarifying question, and only if the answer changes the work.
- Batch related edits into single tool calls where the tool allows it.

## Artifact writing rules
- Imperative mood, directly actionable: exact paths, field names, conditions. Never vague instructions.
- One primary explanation per concept, in one file; elsewhere, reference it. No duplication.
- Procedural files stay under ~500 lines. Prose over tables when equally clear.
- Frontmatter carries flags the reader acts on without reading the body (`status:`, `important_findings:`); the body carries everything needing judgment.

## Reference docs (read on demand only — never preload)
- `docs/prompt-engineering.md` — read before authoring or revising any command, guide, or artifact schema.
- `docs/context-engineering.md` — read before a handoff, when deciding what context to include in a task, or when planning multi-session work.

## Handoff triggers
Run `/handoff` proactively when any of these hold:
- Context feels degraded (repeating questions, re-reading known files, forgetting constraints).
- A large exploratory phase just ended and its noise is no longer needed.
- ~70% of a long session is behind you and a distinct phase is about to start.
Prefer proactive handoff over waiting for auto-compaction. Compaction keeps noise; handoff filters it.

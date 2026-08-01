# /index — rebuild or verify memory/INDEX.md

INDEX.md is the routing table for everything in `memory/`. Its job: let any instance decide what to read WITHOUT opening files.

Format, one line per artifact:

```
# Index

## Logs
- memory/logs/01-etl-load.md — census ACS pull; gotcha: 2023 vintage renamed B19013 fields
- memory/logs/02-etl-clean.md — geocoding pipeline; 4.2% unmatched addresses, list inside

## Handoffs
- memory/handoffs/01-handoff.md — end of exploration phase; dead ends for model selection

## Stage summaries
- memory/stage-1-summary.md — ETL complete; final schema documented here
```

Rules:
- One line per file. Description states content AND when reading it is worth it.
- No entry over 120 characters. If you cannot summarize a file in one line, the file covers too much; note that.
- Run this command: scan `memory/` with `ls -R`, diff against INDEX.md, add missing entries, flag orphaned entries (indexed but deleted). Do not open files whose entries already exist unless asked.
- When a stage completes, write `memory/stage-N-summary.md` (≤ 25 lines: outputs, decisions, interfaces the next stage depends on) and index it. Later stages read the summary, never the stage's individual logs.

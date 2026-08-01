# APM context engineering (reference — read on demand, not at init)

Premise: context windows are finite and degrade as they fill. Every role's context budget is shaped by what it needs to do well.

## Context scoping per role
- Planner: entire context window for planning. No execution history competes for space. Planning and execution are separate phases for this reason.
- Manager: coordination level by default — planning documents, Tracker, Index, Task Logs. Dips into source only for prompt construction or review, then returns to the coordination layer.
- Worker: receives self-contained Task Prompts. Never reads the Spec, Plan, or Tracker. Every coordination token the Worker does not carry is budget for actual work.

## Keeping the Manager lean
- Task Logs as abstraction: review logs, not source. A log compresses thousands of execution tokens into a structured summary.
- Stage summaries as compression: at Stage boundaries, distill Task Logs and working notes into the Index. Incoming Managers read summaries before detail.

## Dependency context rules
- Same-agent dependency: light context — recall anchors, key paths.
- Cross-agent dependency: comprehensive context — file reading instructions, output summaries, integration guidance. Workers can see each other's code but not the reasoning behind it; the Manager bridges that.
- Post-handoff or post-recovery: treat same-agent dependencies as cross-agent. The incoming instance lacks working familiarity with pre-handoff work.

## Compression pipeline
Execution detail → Task Logs → Stage summaries → Memory notes in the Index. Each layer reduces volume while preserving what matters for coordination.

## Read order after handoff
Index first (most compressed, most durable) → Tracker (current state) → recent Task Logs (detail). Compressed layers load first so the big picture precedes the details.

## Persistence
All project state lives in files outside any context window. Conversations end; the file system survives. Session archives extend this across sessions — a new Planner validates archive findings against the current codebase rather than starting from zero.

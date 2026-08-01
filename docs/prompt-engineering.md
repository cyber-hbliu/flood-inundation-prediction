# APM prompt engineering (reference — read on demand, not at init)

## File types
- Commands: prompts the User sends via slash commands. Delivered directly.
- Guides: procedural files, one procedure each. Read on demand via file tools.
- Skills: shared procedural files used by multiple roles. Read at initialization.
- Agent files: subagent configurations. Read when spawning a subagent.

Guides are separate from commands so procedural content is not loaded before it is needed. Each command tells the Agent which guides to read and when.

## Writing patterns
- Imperative mood. Direct instructions produce more reliable behavior than suggestions.
- Directly actionable: specific file paths, field names, conditions. Never "implement properly."
- Structured hierarchy: H2 major sections, H3 subsections, bold sub-topics.
- De-duplication: one primary explanation in one location; other files reference it.
- Token efficiency: prose over tables when equally clear; files under ~500 lines.

## Guide section pattern
Overview → Operational Standards → Procedure → Structural Specifications → Content Guidelines.

## YAML + Markdown split
- YAML frontmatter: facts the reader should not infer. Flags, identifiers, states that map to specific next actions (status: Failed, important_findings: true, modified: attribution).
- Markdown body: everything requiring reading and reasoning — instructions, execution detail, working context.

## Agent-generated artifacts
- Task Prompt (Manager → Worker): self-contained execution plan — dependency context, Spec extractions, instructions, expected outputs, validation criteria.
- Task Report (Worker → Manager): status, log path, key findings.
- Handoff Log (outgoing → incoming): past-tense working knowledge not in Task Logs.
- Handoff Prompt (outgoing → incoming): present-tense state and reconstruction instructions.

## Terminology
Formal terms (Task, Stage, Worker, Manager, Planner, Handoff, Spec, Plan, Rules) are capitalized and carry defined meanings. Consistent terminology produces consistent behavior.

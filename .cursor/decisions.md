## Plugin scope: full elicitation

- **Choice:** One plugin owns requirements/context and architecture (absorbs better-plan / design-checkpoint role)
- **Date:** 2026-10-10
- **Rationale:** User chose full elicitation in a single layer rather than splitting context-only vs architecture-only plugins
- **Alternatives considered:** Context-only with handoff to design-checkpoint; layered two-plugin setup

## Trigger model

- **Choice:** Always-on rule + skill for non-trivial work, plus `/autoscope` on demand
- **Date:** 2026-10-10
- **Rationale:** Automatic better context without a large prompt; command covers revisits and forced rounds
- **Alternatives considered:** Always-on only; slash command only

## Persistence split

- **Choice:** `.cursor/context.md` for goal/scope/constraints/acceptance/assumptions; `.cursor/decisions.md` for architecture choices
- **Date:** 2026-10-10
- **Rationale:** Clean separation of product context vs design decisions while keeping one plugin
- **Alternatives considered:** Single context file; single decisions file for everything

## Question style

- **Choice:** Compact MCQ chooser by default; deepen with EARS / ISO 25010 / Shape Up / pre-mortem only when needed
- **Date:** 2026-10-10
- **Rationale:** Fast answers without ceremony; frameworks as depth, not default checklist
- **Alternatives considered:** Compact chooser only; structured EARS + 25010 every round

## Task-type branching

- **Choice:** Single skill with four playbooks (greenfield / feature / bug / refactor)
- **Date:** 2026-10-10
- **Rationale:** One entrypoint with clear branches; easier to maintain than separate skills
- **Alternatives considered:** Separate skills per type; one skill with light guidance only

# autoscope

A Cursor plugin that elicits project context and design decisions before
non-trivial work. The agent inspects the repo first, asks only expensive
unknowns, batches 3–7 multiple-choice questions with suggested defaults, and
records answers so it does not re-ask.

## What it does

- Gathers settled facts from the request, rules, prior logs, and the codebase
- Classifies the task (greenfield / feature / bug / refactor) and branches questions
- Prioritizes by cost of being wrong (scope, data, auth, integrations, hosting)
- Presents a compact chooser; deepens with Shape Up, ISO 25010, EARS, or a
  pre-mortem only when needed
- Stops when goal, scope, constraints, and acceptance are known (architecture
  forks closed or listed as Assumed)

## Components

| Component | Path | Purpose |
| --------- | ---- | ------- |
| Rule | `rules/autoscope.mdc` | Always-on trigger for non-trivial work |
| Skill | `skills/autoscope/SKILL.md` | Full elicitation procedure and playbooks |
| Command | `commands/autoscope.md` | `/autoscope` to force or revisit a checkpoint |

## Persistence

| File | Contents |
| ---- | -------- |
| `.cursor/context.md` | Goal, scope, constraints, acceptance, assumptions |
| `.cursor/decisions.md` | Architecture and design choices |

## Install locally

Install this folder as a Cursor plugin (Plugins → add local path, or place it
under your local plugins directory), then try a vague prompt such as
"build me an app for tracking habits" in Plan mode, or run `/autoscope`.

## Note on design-checkpoint / better-plan

Autoscope covers both requirements/context and architecture decisions. If you
also have an always-on design-checkpoint plugin, both will fire and feel
redundant—disable one of them.

## License

MIT

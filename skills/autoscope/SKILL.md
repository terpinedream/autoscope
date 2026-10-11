---
name: autoscope
description: Elicit project context, scope, constraints, acceptance, and
  architecture decisions before planning or building. Use at the start of
  greenfield work, new features, non-trivial bugs, or refactors when goal,
  scope, or design forks are unclear.
---

# Autoscope

Goal: give the model enough context to build well without forcing the user to
write a large prompt. Be thorough when finding unknowns; be condensed when
asking. The user chooses; the agent does not silently invent scope or
architecture.

**Presentation:** Prefer an interactive question tool when available. No
preamble, no recap of the request, no plan or implementation in the same
message as a question round.

## 1. Gather what is already settled

Check these sources, in order:

1. The user's current request
2. AGENTS.md and any project rules
3. `.cursor/context.md` (scope, constraints, acceptance, assumptions)
4. `.cursor/decisions.md` (architecture and design choices)
5. The existing code: language, framework, dependencies, tests, directory
   structure, config, and conventions

Anything established by these sources is settled. Do not re-ask it. List it
under **Assumed** (compact) so the user can override.

Do not ask what can be inferred from the repo. That is the biggest quality
difference between useful and annoying clarification.

## 2. Classify the playbook

Pick one primary type:

| Type | When |
| ---- | ---- |
| **Greenfield** | New project or empty/near-empty repo |
| **Feature** | New capability in an existing codebase |
| **Bug** | Incorrect behavior with a plausible fix path |
| **Refactor** | Restructure without (or with tightly scoped) behavior change |

Use the matching playbook section below for what to prioritize. Shared
procedure (rank → present → deepen → record → stop) always applies.

## 3. Identify and rank unknowns

A question is worth asking if being wrong is expensive to reverse, shapes much
of the work, or involves real trade-offs. Prefer:

- Goal and success criteria
- Scope boundaries and no-gos
- Constraints (time/appetite, platform, compliance)
- Acceptance criteria
- Data model, auth, external integrations, hosting/deployment
- Security and other non-functionals when they matter

Also surface decisions the user may not realize they are making (e.g. implies
a persistent store, needs a plugin boundary, sync vs async). Know *why* each
item matters here—even if the reply states that in one line.

Skip cosmetic and low-cost choices; fold them into **Defaults**.

## 4. Cap and present (condensed format)

- Ask only **3–7** highest-impact open items per round.
- Group minor items into **Defaults** (one line each: `X — reason`).
- If nothing material is open, say so in one line and proceed to plan/build.

Think through full trade-offs; **show** a tight version:

```markdown
**Assumed:** `A`; `B`; `C`

**Defaults:** `X — reason`; `Y — reason`

### 1. <Question>?
*<one-line why it matters here>*
- **A)** <label> — <pro>; <con>
- **B)** <label> — <pro>; <con>
- **C)** <label> — <pro>; <con>
→ **Suggest: A** — <one-line reason>
```

Per question:

- 2–4 real options; each option = **one line** (pro and con folded in).
- Include an "other / you decide / explain more" path (tool or final line).
- Recommend, but do not choose for the user on significant items.
- If the user asks for more detail on an option, then expand—don't lead with it.

## 5. Deepen selectively

Default to the compact chooser. Pull frameworks only when the task needs them:

| Framework | When to use |
| --------- | ----------- |
| **Shape Up** (problem, appetite, no-gos) | Scope or effort is fuzzy; risk of over-building |
| **ISO/IEC 25010** (or FURPS+) | Non-functionals matter and were not stated (perf, reliability, security, usability, maintainability, portability, compatibility) |
| **EARS** ("When X, the system shall Y") | Acceptance criteria need to be unambiguous |
| **Pre-mortem** ("Imagine this failed in 6 months. Why?") | Larger work; optional final question |
| **5W1H** | Quick skeleton when almost nothing is known yet |

Do not run every checklist every round.

## 6. Record answers

After the user answers (or explicitly defers):

1. **Context** — write or update `.cursor/context.md` (create if needed):

   ```markdown
   ## <Topic or task>

   - **Goal:** ...
   - **Scope:** ...
   - **Out of scope / no-gos:** ...
   - **Constraints:** ...
   - **Acceptance:** ...
   - **Assumptions:** Assumed X; change if wrong. ...
   - **Date:** <YYYY-MM-DD>
   ```

2. **Decisions** — write architecture/design choices to `.cursor/decisions.md`
   (create if needed):

   ```markdown
   ## <Decision title>

   - **Choice:** <what the user picked>
   - **Date:** <YYYY-MM-DD>
   - **Rationale:** <why, in the user's words where possible>
   - **Alternatives considered:** <brief list>
   ```

For anything unanswered that you must proceed with, list it explicitly as
**Assumed X; change if wrong**—never silent guesswork.

## 7. Stop condition

Stop asking when all of the following are known (or explicitly Assumed):

- Goal
- Scope (including no-gos / out of scope)
- Constraints
- Acceptance criteria
- Architecture forks that affect *this* task (closed or Assumed)

Follow-up round only if answers open new high-impact ambiguity. Same format,
same 3–7 cap.

Then plan or implement. Never invent the plan in the same message as questions.

## Playbooks

### Greenfield

Prioritize:

- Problem and who it is for
- Appetite / how much effort it is worth
- Success criteria and acceptance
- Stack, hosting, data store, auth (if not inferred)
- No-gos and rabbit holes to avoid

### Feature

Prioritize:

- User-facing outcome
- Surfaces / modules touched
- Compatibility and migration needs
- Out of scope for this change
- Architecture forks only where the feature forces a new choice

### Bug

Prioritize:

- Expected vs actual behavior
- Repro and environment
- Blast radius
- Fix vs workaround / urgency

Skip architecture unless the root cause implies a design change. Prefer a
minimal checkpoint; often Assumed + one clarifying question is enough.

### Refactor

Prioritize:

- Motivation (speed, clarity, enable a feature, reduce risk)
- Risk surface (what can break)
- Behavioral freeze vs intentional behavior change
- Rollback or verification approach

## When NOT to run

Skip the full checkpoint for small, local changes (clear bug with known repro,
rename, typo, single-function tweak, dependency or config bump). If unsure,
run a minimal version: list assumptions in one short paragraph and ask only if
something is genuinely consequential.

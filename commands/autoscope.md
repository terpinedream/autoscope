---
name: autoscope
description: Run the autoscope elicitation checkpoint now, or review and
  revisit previously recorded context and decisions
---

# Autoscope

Use the `autoscope` skill. Be thorough on analysis; keep the reply condensed.

1. Read `.cursor/context.md` and `.cursor/decisions.md` if they exist; summarize
   briefly what is already settled.
2. Look at the user's goal and project; classify the playbook and identify
   significant unknowns still open.
3. Present open items in the skill's condensed format (3–7 max, options,
   trade-offs, recommendation).
4. On confirm, update `.cursor/context.md` (scope/constraints/acceptance) and
   `.cursor/decisions.md` (architecture choices).
5. If the user wants to change a past entry, explain impact briefly, then
   update the relevant file once they confirm.

If the user passed arguments, treat them as the topic to focus on.

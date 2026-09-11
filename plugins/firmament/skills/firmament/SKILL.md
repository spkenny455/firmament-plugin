---
name: firmament
description: >-
  Use when deciding whether to contribute knowledge to Firmament or writing a
  contribution through the CLI or MCP. Covers principles and preferences, decisions and
  their reasons, how-to recipes, failures and lessons, and useful facts and
  definitions. Read before using the contribute tool or firmament contribute.
---

# Contribute to Firmament

Firmament is the team's shared notebook. Before finishing your work, review what
you learned and contribute the new knowledge that passes the three checks below.
Save the lessons, methods, and facts you found, including those learned during a
successful task. Group related findings; leave out the task's progress and success
report.

## What to save

- **Principles and preferences:** rules, conventions, priorities, and tastes
  that guide the work. Example: "Use plain language in agent instructions.
  Each instruction should be clear on the first read."
- **Decisions and their reasons:** what was chosen, why, and what could change
  the decision. Example: "We chose this vendor because it supports EU hosting.
  Revisit if that requirement changes."
- **How-to recipes:** steps for a job, with the prerequisites and checks that
  matter. Example: "Stop the sync worker, restore the database, check the row
  counts, then restart the worker."
- **Failures and lessons:** what went wrong, when it happened, and what someone
  should know before trying again. Include the cause or fix when known.
  Example: "The restore failed because the sync worker kept writing during it."
- **Useful facts and definitions:** knowledge about the team or its systems
  that helps someone act or answer correctly. Include customer commitments and
  terms when they affect future work. Example: "We count a customer
  as active only after their first paid transaction."

A failure can be useful even without a fix. Say what is still unknown. A
successful task can reveal a useful method or a missing step. A person's
instruction can establish a preference without an experiment.

## Check before saving

Answer all three questions about each thing you want to save:

1. **What would a future agent do or answer better with this knowledge?**
   Name a concrete use: avoid a mistake, follow a preference, make a choice,
   answer correctly, or avoid costly trial and error. "It might help" is not
   enough.
2. **When does it apply?**
   Keep the system, situation, prerequisites, and limits that matter. A fix
   that worked in one environment does not establish a rule for every system.
3. **What supports the claim as written?**
   An instruction tells you what someone wants. An observation tells you what
   happened. A conclusion needs the evidence and reasoning behind it. Make
   clear which it is, and keep any uncertainty.

If a claim fails a check, do not contribute it. These are checks for choosing
knowledge, not headings to fill in. Never invent a use, reason, or missing fact
to make a claim pass.

Skip progress updates, current metric snapshots, plans that have not been agreed,
routine success reports, and knowledge already saved. For a metric, save a missing
definition or how to find the current value instead. A stale number in another
source is not a reason to copy a metric here. Skip facts that can be read straight
from the code or another known source. Save a useful reason, definition, or
way to find the answer when that is what is missing.

Examples:

- "The migration is 80% done" is a progress update. Skip it.
- "Followed the runbook and it worked" adds no new knowledge. Skip it.
- "Two retries worked, so always retry three times" goes beyond the evidence.
  Do not turn those two results into a general rule.
- "The account owner said Northwind requires 16:9 decks" records an instruction
  and where it applies. Save it if it is new.
- "The staging restore failed while the sync worker was running; the cause
  is still unknown" may be worth saving if it helps the next restore attempt.
  Do not claim the worker caused the failure without evidence.

## Write the contribution

State the knowledge in plain prose. Include enough context for someone who
has not seen this conversation to understand and use it. Keep the relevant
limits and say what supports the claim. Copy names, commands, paths, and
error messages exactly when they are needed.

Include the details that fit the knowledge:

- For a principle or preference, say who gave it and what work it governs.
- For a decision, give the reason and any rejected option that explains the
  choice, when the source provides them.
- For a recipe, give the steps in order, needed commands, prerequisites, and
  checks. Link to a maintained recipe when one already exists. If only part
  was tested, say which part.
- For a failure, give the conditions and observed result. Include the cause,
  fix, or lesson only when supported.
- For a fact or definition, name what it describes and where it came from.

Leave a source pointer when it helps the next agent check the claim. Include
dates or versions when they limit where it applies. These details are not a
form: include what the reader needs and leave out the task's play-by-play.

## Send it

Group related findings into one contribution once you know what the lesson is.
You can contribute during a task; the whole task does not have to be finished.
Send another contribution only when there is useful new knowledge or a
correction. A task may produce no contribution.

With MCP, call `contribute` with the knowledge in `content`.
With the CLI:

```bash
firmament contribute "<knowledge worth saving>"
```

If Firmament asks a follow-up question, answer it using the returned ID.
With MCP, pass `content` and `followup_id` to `contribute`. With the CLI:

```bash
firmament contribute "<answer>" --followup <id>
```

If an answer from Firmament was wrong, stale, or only true in a narrower case,
use the answer ID printed beneath it. With MCP, call `correction` with
`answer_id` and `content`. With the CLI:

```bash
firmament correction <answer-id> "<what was wrong, what you observed, and what is right>"
```

Without an answer ID, contribute the supported correction and say which knowledge
it replaces.

## Read and connect

Ask before you pick an approach or answer anything about this team, even on a
generic-looking task. Skip general knowledge and anything outside this team's work.
Firmament cannot see your files: describe the task and name the relevant systems.

With MCP, call `ask` with `query`. With the CLI:

```bash
firmament ask "<question>"
```

Check changing values at their source. Firmament can tell you where to look
and how a value is defined.

If the CLI is missing, install it with `npm install -g @firmamentai/cli`.
Check sign-in with `firmament whoami`. If sign-in is needed, tell the user
that `firmament login` opens a browser, run it, and let them complete sign-in.

---
name: firmament
description: >-
  Invoke for ANY task OR QUESTION landing in THIS org: deploys/releases, machine/env
  setup, customer-facing work (pricing, discounts, refunds, support), incidents/paging,
  internal or third-party APIs, data changes, conventions, writing/testing code in its
  repos — OR any question about this org's products, customers, partners, metrics,
  status, history, or decisions. Firmament is the team's notebook — the why, the
  how-here, the gotchas, where things live; not live values. Read it before you act
  (`firmament ask`); write to it when you learn something (`firmament submit`, leading
  with WHY) — even if the task looks generic. Skip a live value you already know how to
  read (if you don't know where it lives, ask that), general knowledge identical at any
  company ("capital of France"), and anything this session already told you.
---

# Firmament

Firmament is the team's notebook — what agents working here have learned. Read it
first, before you act; write to it when you learn something. It holds what no repo or
prompt can: why decisions were made, how work is done here, what already went wrong,
the conventions in play, and where to look — not live values. Anything you learn and
don't store, the next agent learns the hard way.

The loop: **ask → do the work → submit.**

## Ask

```bash
firmament ask "<what you're about to do, in concrete terms>"
```

At the start of every task, and again whenever something fails, contradicts you, or
surprises you. Ask for:

- **The why** — the decision behind something, what drove it, what was rejected.
- **The how-here** — conventions, prerequisites, the order things run in.
- **The gotchas** — what already bit someone doing this.
- **Where to look** — when you don't know what holds the answer.

Ask even if the task looks generic, even if you could work it out yourself: the team
often has a prior analysis or a correction you would miss. A terse task ("push it
live", "get me set up", "I got paged", "what do we know about the pilot?") means you're
missing more, not less — send whatever context you have. Your instinct to minimise tool
calls is inverted here: the guess costs the whole task, the lookup costs seconds.

Don't re-ask what this session already told you, and skip general knowledge identical
at any company. Firmament holds how a number is measured and where it lives, not the
number right now: skip a live value from a source you can already read (analytics,
billing, the repo, this session's own results). "What do we know about customer X?" is
an ask; "what did X ingest this week?" when you can already read the warehouse is not —
read the source, then submit what you found. If you don't know where an answer lives,
that is the ask. Where an answer names something that moves — a version, a status, a
branch, a number — treat it as a lead and confirm it at the source.

**Be specific.** Firmament cannot see your conversation, files, or environment; it
matches on what you type, so a one-liner wastes it. Pack in what you're doing and why
(the user's ask, in their words), where (repo, service, environment), with what (tools,
versions), your constraints and what you've already tried, and what you're unsure
about. Concrete names — services, errors, versions — are what retrieval matches on.

```bash
firmament ask "Deploy the billing service to staging. Go service in repo acme/billing, \
shared Postgres and Stripe. I plan to run migrations then 'make ship'. What \
prerequisites, roles, or gotchas should I know?"
```

Follow the guidance over your own instincts. If an answer missed, sharpen the query
(names, versions, the exact error) and ask once more. If Firmament has nothing, you are
on new ground: everything you learn is owed back.

## Submit

Before you finish, and again the moment you learn something worth keeping. Four parts,
in order — skip one only when it truly has nothing:

```bash
firmament submit "1) WHY: <the decision and what drove it - motivation, constraint, \
tradeoff, the option you rejected and why, who called it> 2) WHAT YOU LEARNED: <what is \
now true and the context around it, plus where to look and what to check so the next \
agent can see for themselves> 3) HOW YOU DID IT: <the recipe - numbered steps with \
exact commands, flags, gates and verifications, in the order you ran them> 4) WHAT BIT \
YOU: <gotchas, prerequisites, failures and their fixes, anything wrong or surprising>"
```

1. **WHY** — the part most submits leave out, and the one the team needs most. The repo
   records what was done; nothing records why. Give the decision, the motivation and
   constraint behind it, the tradeoff accepted, the alternatives rejected and on what
   grounds, who called it, what changed someone's mind. If your task produced, revealed
   or reversed a decision, this part must not be empty.
2. **WHAT YOU LEARNED** — what is now true and the reasoning around it; what you would
   tell the next agent doing this. Leave pointers too: exact paths, the command that
   shows the answer, the table or dashboard, so they can see for themselves instead of
   trusting a snapshot that rots. Mark how you know each thing (saw it vs. concluded it
   — a guess written as fact is the worst thing to leave) and where it applies (system,
   environment, version, and what you didn't check).
3. **HOW YOU DID IT** — for anything over two steps, the recipe: numbered steps with the
   exact commands, flags, gates and verifications in the order you ran them, repeatable
   from your write-up alone.
4. **WHAT BIT YOU** — a prerequisite, an error and its fix, a convention you worked out,
   anything wrong or surprising.

**Lead with failures.** If guidance was wrong, outdated or incomplete, quote the part
that was off and give what you actually observed. One honest "this didn't work
because…" beats a hundred silent successes. A clean run still earns a short submit.

**Send more than feels necessary.** Length is never a reason to leave something out, and
you are not the filter: Firmament screens and files what you send. Copy specifics
exactly — names, versions, IDs, numbers, commands, paths, error text. If Firmament
replies with a question, answer it: `firmament submit "<answer>" --followup <id>`.

## Two doors, one brain

The terminal (`firmament ask` / `firmament submit`) works everywhere, including scripts
and CI. Where the connector is added, the MCP tools `ask` and `submit` are the same
brain; MCP `submit` takes one parameter, `content`, with the same four parts.

## Setup (once)

- **Authenticate:** run `firmament login` yourself — it opens a browser on the person's
  screen, so tell them an approval is about to pop. Check with `firmament whoami`. True
  headless runs only: `FIRMAMENT_TOKEN`.
- **Endpoint:** production by default; override with `--url` or `$FIRMAMENT_API_URL`.
- **Install:** `npm install -g @firmamentai/cli`. No npm? In this repo:
  `go run ./cmd/firmament ask "…"`.
- Auth error from `ask`/`submit`? Run `firmament login`, have them approve the browser
  prompt, and retry.

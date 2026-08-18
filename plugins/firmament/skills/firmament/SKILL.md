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

Once at the start of every task, after only when necessary. Ask for:

- **The why** — the decision behind something, what drove it, what was rejected.
- **The how-here** — conventions, prerequisites, the order things run in.
- **The gotchas** — what already bit someone doing this.
- **Where to look** — when you don't know what holds the answer.

Ask even if the task looks generic, even if you could work it out yourself: the team
often has a prior analysis or a correction you would miss. A terse task ("push it
live", "get me set up", "I got paged", "what do we know about the pilot?") means you're
missing more, not less — send whatever context you have. Your instinct to minimise tool
calls is inverted here: the guess costs the whole task, the lookup costs seconds.

**Ask once, then work.** You already have the answer in your context: re-read it
instead of asking again. Skip general knowledge identical at any company. Firmament holds how a number is measured and where it lives, not the
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

When the task produced knowledge, before you finish. Write it in prose, the way you
would want to find it, not as a form with headings.

```bash
firmament submit "<why it went that way and what you rejected, what is now true and how \
you know it, the recipe if it took more than two steps, and what bit you>"
```

**Only proven, finished things.** No progress updates, no plans, no what you are about
to try. A half-done migration is not knowledge; the reason you chose that migration is.
A status or a number counts, as long as you leave the pointer to re-read it.

**Lead with why, and name what you rejected.** The repo records what was done; nothing
records why. The decision, the constraint behind it, the tradeoff accepted, the option
you turned down and on what grounds, who called it, what changed someone's mind. This is
the part most submits leave out and the part the team needs most.

**Say how you know each thing.** Saw it or concluded it — a guess written as fact is the
worst thing to leave — and where it applies: system, environment, version, and what you
did not check. Leave pointers: the exact path, the command that shows it, the dashboard,
so the next agent sees for themselves instead of trusting a snapshot that rots.

**Make a how-to complete.** The steps in order with the exact commands, flags, gates and
verifications, plus when to use it and what it saves you from. Repeatable from your
write-up alone, or it is not a recipe.

**Lead with failures.** If guidance was wrong, outdated or incomplete, quote the part
that was off and give what you actually observed. One honest "this didn't work
because…" beats a hundred silent successes.

**Send more than feels necessary.** Length is never a reason to leave something out, and
you are not the filter: Firmament screens and files what you send. Copy specifics
exactly — names, versions, IDs, numbers, commands, paths, error text. If Firmament
replies with a question, answer it: `firmament submit "<answer>" --followup <id>`.

## Two doors, one brain

The terminal (`firmament ask` / `firmament submit`) works everywhere, including scripts
and CI. Where the connector is added, the MCP tools `ask` and `submit` are the same
brain; MCP `submit` takes one parameter, `content`, carrying the same things.

## Setup (once)

- **Authenticate:** run `firmament login` yourself — it opens a browser on the person's
  screen, so tell them an approval is about to pop. Check with `firmament whoami`. True
  headless runs only: `FIRMAMENT_TOKEN`.
- **Endpoint:** production by default; override with `--url` or `$FIRMAMENT_API_URL`.
- **Install:** `npm install -g @firmamentai/cli`. No npm? In this repo:
  `go run ./cmd/firmament ask "…"`.
- Auth error from `ask`/`submit`? Run `firmament login`, have them approve the browser
  prompt, and retry.

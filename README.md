# Firmament for Claude Code

Connect Claude Code to **[Firmament](https://getfirmament.com)** — your team's
shared, verified knowledge. Your agent asks what's true about your org and how
work gets done here, then records what it learns so the next agent doesn't have
to relearn it.

**One install wires up three things:**

- **The tools** — the Firmament MCP server (`ask` and `submit`). Sign in once.
- **The reminder** — a session hook that puts a short "consult Firmament" note
  in front of Claude at the start of every session. Claude Code runs it, not the
  model, so it can't be forgotten — even in long sessions.
- **Session capture** — Stop/SessionEnd hooks that record your sessions into
  Firmament automatically (secrets scrubbed locally). Capture activates only if
  the `firmament` CLI is installed and signed in; without the CLI these hooks do
  nothing, silently, and `ask`/`submit` still work.

## Install

In Claude Code:

```
/plugin marketplace add spkenny455/firmament-plugin
/plugin install firmament@firmament
```

Then sign in:

```
/mcp
```

Pick `firmament` and complete the browser sign-in. That's it.

## Optional: turn on session capture

```
npm i -g @firmamentai/cli
firmament login
```

Nothing else — the plugin's hooks detect the CLI and start capturing new
sessions automatically, in every project.

## Requirements

- Claude Code with plugin support.
- A Firmament account. Don't have one yet? Start at
  [getfirmament.com](https://getfirmament.com).

## Links

- Website: https://getfirmament.com
- Connect other agents (Cursor, VS Code, and more): https://app.getfirmament.com/connect

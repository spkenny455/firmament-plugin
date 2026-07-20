# Firmament for Claude Code

Connect Claude Code to **[Firmament](https://getfirmament.com)** — your team's
shared, verified knowledge. Your agent asks what's true about your org and how
work gets done here, then records what it learns so the next agent doesn't have
to relearn it.

Installing this plugin wires up the Firmament MCP server. You sign in once, and
the `ask` and `submit` tools become available to Claude Code automatically.

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

Pick `firmament` and complete the browser sign-in. That's it — your agent can
now ask your team's knowledge and report back what it learns.

## What you get

- **`ask`** — look up your team's org-specific facts and how-to before you act.
- **`submit`** — record what you learned so the knowledge compounds.

No API keys to paste: sign-in is a one-time browser OAuth flow.

## Requirements

- Claude Code with plugin support.
- A Firmament account. Don't have one yet? Start at
  [getfirmament.com](https://getfirmament.com).

## Links

- Website: https://getfirmament.com
- Connect other agents (Cursor, VS Code, and more): https://app.getfirmament.com/connect

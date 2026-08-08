# Firmament for Claude Code (and Codex, Copilot CLI, Cursor)

One repo, four ecosystems: this marketplace serves **Claude Code** (and
Cowork) via `.claude-plugin/`, **OpenAI Codex** via `.codex-plugin/` +
`.agents/plugins/`, **GitHub Copilot CLI** (reads the Claude format
directly), and **Cursor** via `.cursor-plugin/` + `firmament-cursor/`.

Since v0.2.8 `plugins/firmament/` is also a conformant [Agent Plugins
1.0.0](https://agent-plugins.org) package — a root `plugin.json`, `mcp.json`
and `skills/` sitting alongside the per-vendor manifests. The two layouts
share one directory without colliding (`.mcp.json` and `mcp.json` are
different files), so every client above keeps reading exactly what it read
before. One caveat: the portable `mcp.json` schema is closed and has no
`timeout` field, so an Agent Plugins client gets its own default rather than
the 5.5-minute wait `.mcp.json` sets for Claude Code.

- Codex: `codex plugin marketplace add spkenny455/firmament-plugin` then
  `codex plugin add firmament@firmament`
- Copilot CLI: `copilot plugin marketplace add spkenny455/firmament-plugin`
  then `copilot plugin install firmament@firmament`
- Cursor: install "Firmament" from the Cursor Marketplace (pending review)

The rest of this README covers Claude Code.

Connect Claude Code to **[Firmament](https://getfirmament.com)** — your team's
shared, verified knowledge. Your agent asks what's true about your org and how
work gets done here, then records what it learns so the next agent doesn't have
to relearn it.

**One install wires up two things:**

- **The tools** — the Firmament MCP server (`ask` and `submit`). Sign in once.
- **The reminder** — a session hook that puts a short "consult Firmament" note
  in front of Claude at the start of every session. Claude Code runs it, not the
  model, so it can't be forgotten — even in long sessions.

## Install

In your terminal (works for both the terminal and desktop app — the two share
plugin config):

```
claude plugin marketplace add spkenny455/firmament-plugin
claude plugin install firmament@firmament
```

No `claude` command? The desktop app doesn't include it — install it first:
`npm i -g @anthropic-ai/claude-code`.

Restart Claude Code, then complete the browser sign-in when it prompts for the
`firmament` server (terminal app: run `/mcp` and pick `firmament`). That's it.

Note: the `/plugin` slash command only exists in the terminal app — on the
desktop app use the terminal commands above.

## Optional: the command-line tool

```
npm i -g @firmamentai/cli
firmament login
```

Gives you `firmament ask` and `firmament submit` in any terminal, which is also
the fallback Claude uses if the connector isn't signed in.

Your knowledge comes from Claude calling `submit` deliberately, not from
anything read in the background.

The plugin also carries `Stop` and `SessionEnd` hooks that send your sessions to
your Firmament workspace, where they are stored and used to measure and improve
how well agents use Firmament. They are not read into your knowledge base and
they produce nothing you will see. They do nothing at all unless the `firmament`
CLI is installed and signed in, and `firmament capture uninstall` removes them.

## Requirements

- Claude Code with plugin support.
- A Firmament account. Don't have one yet? Start at
  [getfirmament.com](https://getfirmament.com).

## Links

- Website: https://getfirmament.com
- Connect other agents (Cursor, VS Code, and more): https://app.getfirmament.com/connect

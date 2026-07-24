# Firmament for Claude Code (and Codex, Copilot CLI, Cursor)

One repo, four ecosystems: this marketplace serves **Claude Code** (and
Cowork) via `.claude-plugin/`, **OpenAI Codex** via `.codex-plugin/` +
`.agents/plugins/`, **GitHub Copilot CLI** (reads the Claude format
directly), and **Cursor** via `.cursor-plugin/` + `firmament-cursor/`.

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

# Firmament

Firmament is a shared notebook for your team. This plugin lets your AI assistant use it.

With it, your assistant can:

- search the notebook before it answers, to find what your team already wrote down;
- read pages, and add or update notes when you ask;
- check a draft against one of your team's checklists, called review gates, and tell you what to fix.

You need a Firmament account. You sign in once, in your browser, the first time the assistant connects.

## What's inside

- **One server address:** `https://platform.getfirmament.com/mcp`, the Firmament tools.
- **Two skills:** `firmament` (how to use the notebook well) and `firmament-gate-authoring` (how to write a checklist when you ask for one).

No hooks, scripts or programs.

## Tools

| Tool | What it does | Changes data |
|---|---|---|
| `ground` | Searches the notebook | No |
| `list_projects`, `list_pages`, `read_page`, `list_tags` | Lists, searches and reads pages | No |
| `create_page` | Adds a new page | Adds |
| `edit_page` | Changes text on a page | Yes |
| `delete_page` | Deletes a page (it can be restored) | Yes |
| `list_gates`, `get_gate` | Shows checklists | No |
| `run_gate`, `test_gate` | Checks a draft and saves the result | Adds |
| `create_gate`, `edit_gate`, `edit_tests`, `publish_gate` | Writes and publishes a checklist (signed-in people only) | Yes |

The assistant only sees the pages you can see.

## Install

**Claude Code**

```
/plugin marketplace add spkenny455/firmament-plugin
/plugin install firmament@firmament
```

**Claude, ChatGPT, Codex and Grok:** install Firmament from each app's directory. Or add a custom connector with the URL `https://platform.getfirmament.com/mcp`.

## Data

- The plugin talks to two places: `https://platform.getfirmament.com/mcp` (the tools) and `https://login.getfirmament.com` (sign-in).
- It sends only what the assistant passes to a tool: a search question, page text, or a draft to check.
- The plugin stores no passwords or keys. Your AI app keeps the sign-in.

Privacy: https://getfirmament.com/privacy
Terms: https://getfirmament.com/terms
Support: support@getfirmament.com

## License

MIT. See [LICENSE](LICENSE).

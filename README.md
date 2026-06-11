# harness-marketplace

A single Claude Code [plugin marketplace](https://code.claude.com/docs/en/plugin-marketplaces)
that bundles all of [@jondwillis](https://github.com/jondwillis)' plugins. Each entry
tracks the `main` branch of the plugin's own repository — install once, get the latest.

## Install

```bash
# Add the marketplace once
/plugin marketplace add jondwillis/harness-marketplace

# Then install any of the plugins
/plugin install imessage@harness-marketplace
/plugin install notes-app@harness-marketplace
/plugin install functional-emotions@harness-marketplace
/plugin install waggledance-plugin@harness-marketplace
```

To pull newer versions later: `/plugin marketplace update harness-marketplace`, then
reinstall or `/reload-plugins`.

## Plugins

| Plugin | What it does | Source |
|--------|--------------|--------|
| **imessage** | Read-only macOS iMessage/SMS/RCS reader. Decodes `attributedBody` so search/read see every message, not just the few with a non-NULL `text` column. | [imessage-plugin](https://github.com/jondwillis/imessage-plugin) |
| **notes-app** | Full CRUD for macOS Notes.app via AppleScript — notes, folders, accounts, attachments. | [notes-app-plugin](https://github.com/jondwillis/notes-app-plugin) |
| **functional-emotions** | Hook-based "emotional priming" that counters desperation/urgency/sycophancy patterns shown to drive reward hacking and capitulation. | [functional-emotions](https://github.com/jondwillis/functional-emotions) |
| **waggledance-plugin** | Plan-graph optimizer — decomposes plan-mode output into a level-keyed DAG, surfaces critical path and parallelism, supports replan/expand. | [waggledance-plugin](https://github.com/jondwillis/waggledance-plugin) |

## How this is wired

This repo holds only a `marketplace.json` — no plugin code. Each `plugins[]` entry
points at its plugin's own GitHub repo with a `github` source tracking `main`:

```json
{
  "name": "imessage",
  "source": { "source": "github", "repo": "jondwillis/imessage-plugin", "ref": "main" }
}
```

Plugins keep their own repos, issues, history, and versioning; this marketplace is just
a thin index. To add a plugin, append an entry here. To pin a plugin to a fixed release,
add a `"sha"` (or swap `ref` for a tag) to its entry.

## License

[MIT](LICENSE)

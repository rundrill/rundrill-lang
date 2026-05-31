# RunDrill language marketplace

The public **install index** for RunDrill's natural-language courses (English, Kazakh, …). Each
course ships as one plugin — a `<subject>-coach` skill backed by an MCP drill engine (curriculum,
progress, mistake memory).

This is the languages-only sibling of the main [`rundrill/rundrill`](https://github.com/rundrill/rundrill)
index (which carries the programming and professional courses). This repo holds only the catalogs;
the course plugins live in their own repos under the [`rundrill`](https://github.com/rundrill) org
and are referenced by Git source. Two catalogs cover the two marketplace-based hosts (one entry per
course in each):

- `.claude-plugin/marketplace.json` — **Claude Code / Desktop**, `github` source.
- `.agents/plugins/marketplace.json` — **OpenAI Codex**, `url` source.

## Installing (for users)

**Claude Code / Claude Desktop** — via this marketplace:
```
/plugin marketplace add rundrill/rundrill-lang        # the org/repo of this index
/plugin install rundrill-english@rundrill-lang            # <plugin-name>@<marketplace-name>
/reload-plugins                                           # → /english-coach is live
```
`@rundrill-lang` is the marketplace `name` field (set in `marketplace.json`), not the repo name.

**OpenAI Codex** — via this marketplace too:
```
codex plugin marketplace add rundrill/rundrill-lang    # GitHub shorthand; reads .agents/plugins/marketplace.json
```
Then open the plugin directory, pick the **RunDrill — Languages** marketplace, and install the course.

**Google Antigravity** — no marketplace; Antigravity scans plugin dirs. Drop a course folder in:
- `~/.gemini/config/plugins/rundrill-english/` (global, all workspaces), or
- `<workspace>/.agents/plugins/rundrill-english/` (workspace-scoped).

## Registering a published course

A course plugin lives in its own repo (e.g. `rundrill/rundrill-english`). Add one entry to **each**
catalog, pinned to a released tag (`ref`, and optionally a full-commit `sha`) so users don't pull
unfinished work.

`.claude-plugin/marketplace.json` (Claude — `github` source):
```json
{
  "name": "rundrill-english",
  "source": { "source": "github", "repo": "rundrill/rundrill-english", "ref": "v0.1.0" },
  "description": "English coach — drills, progress, and mistake memory."
}
```

`.agents/plugins/marketplace.json` (Codex — `url` source; always include `policy` + `category`):
```json
{
  "name": "rundrill-english",
  "source": { "source": "url", "url": "https://github.com/rundrill/rundrill-english.git", "ref": "v0.1.0" },
  "policy": { "installation": "AVAILABLE", "authentication": "ON_INSTALL" },
  "category": "Education"
}
```

## Naming convention

Same as the main index: lowercase **kebab-case** everywhere; plugin = `rundrill-<subject>`, skill =
`<subject>-coach` (so the bare `/english-coach` works), MCP server name = `rundrill-<subject>`. The
SKILL.md `name:` field, its folder name, and the slash command must all match.

Authoring a new course and the submodule layout: see the private monorepo's `plugins/README.md`
and [Plugin Packaging & Distribution](https://github.com/kmmbvnr/rundrill/blob/main/wiki/plugin-packaging.md).

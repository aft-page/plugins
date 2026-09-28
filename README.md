# aft.page plugin

Ask your coding agent to **deploy to aft.page** and get back a live, shareable
URL. No account needed for the first deploy.

The plugin is two things: a skill that tells the agent how to build and ship
safely, and the aft.page remote MCP server (`https://mcp.aft.page/mcp`) that
does the upload. It adds no local code.

## Install

**Cursor**: install **aft.page** from the Cursor Marketplace, or add this repo
as a marketplace source.

**Claude Code**

```text
/plugin marketplace add aft-page/plugins
/plugin install aft-page@aft-page
```

**Codex, Copilot CLI, VS Code, and other agents** via the
[`plugins`](https://www.npmjs.com/package/plugins) installer:

```bash
npx plugins add aft-page/plugins
```

**Any MCP client** (no plugin):

```json
{
  "mcpServers": {
    "aft-page": { "type": "streamable-http", "url": "https://mcp.aft.page/mcp" }
  }
}
```

Restart the agent, then say:

> Deploy this to aft.page

## What it can deploy

Static sites and build output (Vite, Next.js static export), and public GitHub
repos through the same engine as [aft.page/run](https://aft.page/run/): Next.js
server rendering, Node, Python (Flask, FastAPI, Django) and Dockerfile apps.
The tools:

| Tool | Does |
| --- | --- |
| `deploy` | Publish HTML or a built folder; update it with the same slug + edit token |
| `deploy_repo` | Build and publish a public GitHub repo |
| `aft_deploys` | List a site's deploy history |
| `aft_rollback` | Roll back to an earlier deploy on the same URL |
| `aft_health` | Check the connection to aft.page |

## Before you deploy

- A first deploy is **public** immediately. Claim it (the agent returns a claim
  link) to keep it and to make it private.
- The agent stores the site's edit token in `.aft/state.json`. Keep `.aft/` out
  of git; the skill adds it to `.gitignore`.
- Never deploy secrets: the skill excludes `.env*`, keys and credentials.

## Layout

```text
.cursor-plugin/plugin.json   Cursor manifest
.claude-plugin/              Claude Code manifest + marketplace
.plugin/plugin.json, .mcp.json   `npx plugins` manifest + MCP
plugin.json, mcp.json        Agent Plugins manifest + MCP
skills/deploy-to-aft/        the skill
```

Issues and questions: hello@aft.page · [aft.page](https://aft.page)

---
titleTemplate: 'Todo4Agent'
description: 'Todo4Agent: an MCP task list designed for agents, with desktop and WebUI'
layout: home

hero:
    name: "Todo4Agent"
    tagline: "An MCP task list designed for agents, with desktop and WebUI"
---

## How to Download

<DownloadLinks />

After installing, you can change the WebUI port and external listening in "Settings → Service" (defaults: port 3000, listening on 0.0.0.0 so other devices on your LAN can access it directly).

## Connecting Your Agent (MCP)

> The "Agent Access" page in the app copies this configuration with one click.

Configure it in any MCP-capable agent client:

```json
{
  "mcpServers": {
    "todo4agent": {
      "command": "todo4agent",
      "args": ["mcp"],
      "env": {
        "TODO4AGENT_USERNAME": "your-username",
        "TODO4AGENT_PASSWORD": "your-password"
      }
    }
  }
}
```

Your agent can then create, update, complete, reorder, archive, import / export tasks and read / write prompts on its own task list. See [Agent Access (MCP)](/en/mcp) for the full tool list and locking rules.

## First Steps

The app ships with a default account **admin / admin123** — please change the password as soon as possible after signing in ("Settings → Users"). Task data is stored in a local SQLite database and can be exported / imported as JSON for backup and migration ("Settings → Data"). See [Quick Start](/en/quickstart) for a walkthrough.

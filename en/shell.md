# Command Line

## Run Modes

| Command | Description |
| --- | --- |
| `todo4agent` | Start the desktop app (also serves the WebUI in the background) |
| `todo4agent serve` | Run the WebUI / HTTP API headless |
| `todo4agent mcp` | Start the MCP server (stdio, for agent clients) |
| `todo4agent help` | Show the full help (MCP client configuration example and default account) |
| `todo4agent version` | Show the version number |

## Options

| Option | Description |
| --- | --- |
| `--port <port>` | Set the WebUI/API listening port (1024-65535); effective for this run only and takes priority over the port saved in the settings page, e.g. `todo4agent serve --port 8080`; applies to desktop and serve modes |

Example:

```bash
# Run headless on port 8080 for this run
todo4agent serve --port 8080
```

## Behavior Notes

- When a port is occupied, the app rolls over automatically (up to 10 ports); the actual port shows in the startup log and "Settings → Service"
- Starting the desktop app a second time does not spawn another instance — the existing window is brought to the front instead; `serve` / `mcp` modes are unaffected and may run in parallel
- The database location can be overridden with the `TODO4AGENT_DB` environment variable — see [Data](/en/data)

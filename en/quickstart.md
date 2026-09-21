# Quick Start

## Installation

Download the installer for your platform from [GitHub Releases](https://github.com/Todo4Agent/Todo4Agent/releases) (Windows / macOS / Linux). The service port and external listening can be changed in "Settings → Service" (defaults: port 3000 / listening on 0.0.0.0).

<DownloadLinks />

## Launch

Start the desktop app after installing — it also serves the WebUI in the background:

- **Desktop window**: identical to the WebUI; closing the window keeps the app running in the system tray
- **Browser**: <http://127.0.0.1:3000>
- The WebUI listens on `0.0.0.0` by default, so other devices on your LAN can access it directly; you can switch to localhost-only or change the port in "Settings → Service"

On headless machines, run the WebUI / HTTP API with `todo4agent serve` — see [Command Line](/en/shell).

## Sign In

The app ships with a default account:

- Username: `admin`
- Password: `admin123`

Please change the password as soon as possible after signing in ("Settings → Users"). You can also register your own account (registration is enabled by default and can be disabled in "Settings → Users"). Each user's task data is independent.

## Key Features

- **Task management**: groups, creating, editing, completion, due dates, ordering
- **List locking**: lock a list (group) so agents can no longer edit it through MCP (editing in the UI is unaffected)
- **Trash**: restore accidental deletions
- **Task archive**: archived tasks move to the "Archive" page, grouped by archive date
- **JSON import / export**: task lists and prompts included, for backup and migration
- **Cross-platform**: desktop apps (Windows / macOS / Linux) and browser WebUI
- **Prompts**: an AGENTS.md-style collaboration spec for your agent — empty by default, edited in the UI, and readable / writable by the agent through MCP (isolated per user)

## Next Steps

- To let an agent operate your task list, see [Agent Access (MCP)](/en/mcp)
- For run modes and options, see [Command Line](/en/shell)
- For storage location and backup / migration, see [Data](/en/data)

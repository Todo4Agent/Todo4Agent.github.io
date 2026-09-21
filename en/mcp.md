# Agent Access (MCP)

Todo4Agent exposes the task list to agents as an MCP (Model Context Protocol) server over stdio transport. MCP shares the same SQLite database as the desktop app / WebUI — changes made by the agent appear in the UI after a refresh.

## Client Configuration

Configure it in any MCP-capable agent client (the same format works for ZCode / Claude Desktop):

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

The "Agent Access" page in the app copies this configuration with one click (the username is pre-filled with the signed-in account).

## Credentials

On startup, MCP requires real user credentials via `TODO4AGENT_USERNAME` / `TODO4AGENT_PASSWORD` (the first launch automatically creates the default account admin / admin123); if either is missing or fails verification, the process refuses to start.

After a password change (in the UI or via the MCP `user_password` tool), all signed-in sessions of that user are revoked — update the password in the client env and restart the MCP connection.

## Available Tools

| Tool | Description |
| --- | --- |
| `app_version` / `app_release` | Query the app version / releases page URL |
| `group_list` / `group_create` / `group_rename` / `group_delete` | Task group management (deleting a group moves its tasks to the trash) |
| `task_list` / `task_create` / `task_update` | Task queries and edits (filter by group, move between groups, change status, due dates) |
| `task_complete` / `task_delete` | Toggle completion / delete (soft delete into the trash) |
| `task_archive` / `task_unarchive` | Archive / unarchive tasks |
| `db_path` | Query the connected database file path (including any `TODO4AGENT_DB` override) |
| `task_export` / `task_import` | Export tasks and prompts as JSON (same shape as the UI export) / import (same-name groups merge; prompts migrate via the `prompt` field) |
| `user_password` | Change the current account's password (old + new; revokes that user's signed-in sessions) |
| `prompt_get` / `prompt_update` | Read / fully replace the current user's agent prompt (empty by default; an empty string clears it) |

## List Locking

Once a list (group) is locked (toggle it from the group's ⋮ menu or context menu in the sidebar), the agent's write operations on that list are rejected with a readable message:

- Creating / editing / deleting that group's tasks, moving tasks into it
- Renaming / deleting the group
- Importing a document containing the group

Reading the list, all operations on unlocked lists, and editing in the UI are unaffected. `group_list` returns a `locked` field showing the state; the system group "Unfiled" cannot be locked.

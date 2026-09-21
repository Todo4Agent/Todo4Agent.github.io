# Data

## Storage Location

Task data is stored in a local SQLite database:

- Windows default path: `%LOCALAPPDATA%\Todo4Agent\todo.db`
- Override the location with the `TODO4AGENT_DB` environment variable

"Settings → Data" shows the current database file path and offers "Open database file location" to reveal it in your file manager (selects the file on Windows / shows in Finder on macOS / opens the containing folder on Linux).

The desktop app, the WebUI and MCP all share the same database — changes from any of them take effect immediately for the others.

## JSON Import / Export

"Settings → Data" in the UI and the MCP `task_export` / `task_import` tools share the same implementation. The export file contains the task lists and the prompt for backup and migration; on import, same-name groups merge and the prompt migrates via the `prompt` field.

Export JSON format:

```json
{
  "version": 1,
  "exported_at": "2026-08-22T12:00:00Z",
  "prompt": null,
  "groups": [
    {
      "name": "Quick List",
      "tasks": [
        { "title": "Example task", "description": "", "status": "pending", "due_at": null }
      ]
    }
  ]
}
```

`prompt` is the user's agent prompt (collaboration spec): `null` when unset, and absent from export files produced by older versions. If the field is present on import, the prompt migrates with it (blank counts as clearing); if absent, the current prompt is kept.

## Trash

Deletion is always a soft delete: deleted tasks and groups move to the trash and can be restored at any time; only emptying the trash removes them physically. When a group is deleted, its tasks (including archived ones and those already in the trash) move into "Unfiled" as a whole, so nothing is lost with the group; restoring a group with a name conflict automatically renames it to "Original name (2)".

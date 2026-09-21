# 数据

## 存储位置

任务数据保存在本机 SQLite 数据库中：

- Windows 默认路径：`%LOCALAPPDATA%\Todo4Agent\todo.db`
- 可用环境变量 `TODO4AGENT_DB` 指定其他位置

「设置 → 数据」会显示当前数据库文件路径，并可点击「打开数据库文件位置」在系统文件管理器中定位该文件（Windows 选中文件 / macOS 在 Finder 中显示 / Linux 打开所在目录）。

桌面端、WebUI 与 MCP 共享同一个数据库，任一方的修改对其他方即时生效。

## 导出 / 导入 JSON

界面「设置 → 数据」与 MCP 的 `task_export` / `task_import` 走同一实现。导出文件包含任务清单与提示词，方便备份与迁移；导入时同名分组并入，提示词随 `prompt` 字段迁移。

导出 JSON 的格式：

```json
{
  "version": 1,
  "exported_at": "2026-08-22T12:00:00Z",
  "prompt": null,
  "groups": [
    {
      "name": "快速清单",
      "tasks": [
        { "title": "示例任务", "description": "", "status": "pending", "due_at": null }
      ]
    }
  ]
}
```

`prompt` 为用户提示词（Agent 协作规范）：未设置为 `null`，旧版导出文件无此字段；导入时含该字段则提示词一并迁移（空白视为清空），不含则保持现状。

## 回收站

删除统一走软删除：任务与分组删除后进入回收站，可随时恢复，清空回收站才物理删除。删除分组时组内任务（含已归档与回收站中的）整体移入「无分组」，不会随分组丢失；恢复分组遇同名冲突时自动顺延为「原名 (2)」。

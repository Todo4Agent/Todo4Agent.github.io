# Agent 接入（MCP）

Todo4Agent 以 MCP（Model Context Protocol）Server 的形式向 Agent 开放任务清单能力，传输方式为 stdio。MCP 与桌面端 / WebUI 访问同一个 SQLite 数据库，Agent 写入后界面点击刷新即可见。

## 客户端配置

在支持 MCP 的 Agent 客户端中配置：

```json
{
  "mcpServers": {
    "todo4agent": {
      "command": "todo4agent",
      "args": ["mcp"],
      "env": {
        "TODO4AGENT_USERNAME": "你的用户名",
        "TODO4AGENT_PASSWORD": "你的密码"
      }
    }
  }
}
```

软件界面「Agent 接入」页可一键复制该配置（用户名自动填入当前登录账号）。

## 凭据说明

MCP 启动时必须通过 `TODO4AGENT_USERNAME` / `TODO4AGENT_PASSWORD` 指定并验证账号（首次运行数据库会自动创建初始账号 admin / admin123），验证失败将拒绝启动。

修改密码后（界面或 MCP 的 `user_password` 工具）该用户已登录会话会失效，需同步更新客户端 env 中的 `TODO4AGENT_PASSWORD` 并重启 MCP 连接。

## 可用工具

| 工具                                                            | 说明                                                                                          |
| --------------------------------------------------------------- | --------------------------------------------------------------------------------------------- |
| `app_version` / `app_release`                                   | 查询应用版本号 / 发布页地址                                                                   |
| `group_list` / `group_create` / `group_rename` / `group_delete` | 任务分组管理（删除分组其下任务一并进回收站）                                                  |
| `task_list` / `task_create` / `task_update`                     | 任务查询与编辑（支持按分组过滤、移动分组、改状态、截止时间）                                  |
| `task_complete` / `task_delete`                                 | 完成切换 / 删除（软删除进回收站）                                                             |
| `task_archive` / `task_unarchive`                               | 归档 / 取消归档任务                                                                           |
| `db_path`                                                       | 查询当前连接的数据库文件路径（含 `TODO4AGENT_DB` 覆盖后的实际路径）                           |
| `task_export` / `task_import`                                   | 导出任务清单与提示词 JSON（与界面导出同构）/ 导入（同名分组并入，提示词随 `prompt` 字段迁移） |
| `user_password`                                                 | 修改当前账号密码（原密码 + 新密码；改后该用户已登录会话失效）                                 |
| `prompt_get` / `prompt_update`                                  | 读取 / 全量更新当前用户的 Agent 提示词（默认为空；传空字符串即清空）                          |

## 清单锁定

某个清单（分组）被锁定后（界面侧边栏分组 ⋮ 菜单或右键菜单切换），Agent 对该清单的写操作会被拒绝并提示：

- 该组任务的增删改、把任务移入该组
- 改名 / 删除该组
- 导入文档含该组

读取该清单、以及未锁定清单的一切操作不受影响，界面编辑也不受影响。`group_list` 返回的 `locked` 字段可查看锁定状态；系统分组「无分组」不可锁定。

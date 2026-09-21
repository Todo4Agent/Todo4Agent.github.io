# 命令行

## 运行模式

| 命令 | 说明 |
| --- | --- |
| `todo4agent` | 启动桌面应用（后台同时提供 WebUI 服务） |
| `todo4agent serve` | 无界面运行 WebUI / HTTP API |
| `todo4agent mcp` | 启动 MCP Server（stdio，供 Agent 客户端连接） |
| `todo4agent help` | 查看完整帮助（含 MCP 客户端配置示例与初始账号说明） |
| `todo4agent version` | 查看版本号 |

## 选项

| 选项 | 说明 |
| --- | --- |
| `--port <端口>` | 指定 WebUI/API 监听端口（1024-65535），本次运行有效、优先于设置页保存的端口，如 `todo4agent serve --port 8080`；适用于桌面与 serve 模式 |

示例：

```bash
# 无界面运行，本次使用 8080 端口
todo4agent serve --port 8080
```

## 行为说明

- 端口被占用时自动顺延（最多 10 个端口），实际端口以启动日志或「设置 → 服务」显示为准
- 桌面应用重复启动不会开出第二个实例，而是唤起并聚焦已有窗口；`serve` / `mcp` 模式不受影响，仍可多实例并行
- 数据库位置可用环境变量 `TODO4AGENT_DB` 指定，详见[数据](/data)

---
titleTemplate: 'Todo4Agent'
description: 'Todo4Agent：为 Agent 设计的 MCP 任务清单，附带桌面与 WebUI 界面'
layout: home

hero:
    name: "Todo4Agent"
    tagline: "为 Agent 设计的 MCP 任务清单，附带桌面与 WebUI 界面"
---

## 如何下载

<DownloadLinks />

## Agent 接入（MCP）

> 软件界面「Agent 接入」页可一键复制该配置。

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

Agent 即可对你自己的任务清单执行增删改查、重排、归档、导入导出、读写提示词等操作

## 首次使用

系统自带初始账号 **admin / admin123**，登录后请尽快在「设置 → 用户」中修改密码。任务数据保存在本机 SQLite 数据库中，支持在「设置 → 数据」中导出 / 导入 JSON 进行备份与迁移。

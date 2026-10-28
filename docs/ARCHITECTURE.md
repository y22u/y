# 架构与 API 说明

> 本文依据 4.10.26 部署说明整理。完整源码尚未纳入此仓库，因此本文属于模块与接口概览，不是对全部实现的独立代码审计。

## 模块
- **Web 工作台：** 导航、总览、Agent 对话、角色库、模型/语音状态及自动任务界面。
- **本地服务：** 由 `start_service.bat` 启动；部署说明预期使用 `127.0.0.1:8765`。
- **模型集成：** 按配置连接 Ollama、IndexTTS、Qwen3-TTS 与相关 ASR 能力。
- **原生桌宠：** 无图片修订版使用文字模式，保留气泡与交互。
- **自动任务：** 固定任务白名单、状态记录、事件日志、人工审批和质量门禁。

## 默认数据路径
- SQLite：`data/automation/tasks.sqlite3`
- 日志：`data/automation/automation.log`
- 备份：`data/automation/backups/`
- 发布产物：`data/automation/artifacts/`

部署说明列出的任务状态包括 `queued`、`running`、`needs_approval`、`completed`、`failed` 与 `cancelled`。进程中断后，残留运行任务应标记为失败而不是自动重放，以避免重复副作用。

## API 表
| 方法 | 路径 | 用途 |
|---|---|---|
| GET | `/api/v1/automation/status` | 查询自动任务状态 |
| POST | `/api/v1/automation/runner/start` | 启动执行器 |
| POST | `/api/v1/automation/runner/stop` | 停止执行器 |
| GET | `/api/v1/automation/tasks?limit=50` | 查询任务记录 |
| POST | `/api/v1/automation/tasks` | 创建白名单任务 |
| POST | `/api/v1/automation/tasks/{task_id}/approval` | 批准或拒绝待审批任务 |
| GET | `/api/v1/automation/events?limit=100` | 查询事件记录 |

创建任务示例：
```json
{"task_type":"health_check","payload":{},"title":"手动巡检"}
```

## 安全约束建议
任务应使用固定白名单，而不是任意命令执行接口。代码补丁需限制路径、扩展名和内容大小；修改前备份，写入前人工审批。发布包应排除凭据、数据库、日志、模型、私人音频与虚拟环境。

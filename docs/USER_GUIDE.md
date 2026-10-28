# 功能与使用手册

## 工作台
UI 重设计版采用深色星际控制台风格，包含侧边导航、状态卡片、表单和响应式布局。状态卡片仅反映界面当前可读取的信息，不代表模型或语音服务必然可用。

## Agent 对话
1. 打开 Agent 对话页面。
2. 选择已配置且可访问的模型提供方。
3. 输入问题并发送。
4. 若无回复，检查本地服务、模型配置、后端日志和浏览器请求状态。

界面中出现某个模型选项不代表该模型已安装。请勿将 API Key 写入源码或提交到 GitHub。

## 角色库与桌宠
角色库用于浏览或维护项目支持的角色文字设定及相关资源。无图片桌宠修订版仅说明原生桌宠窗口不渲染角色形象图片，改用文字徽标，并保留文字气泡、拖动和互动效果；这不等于删除项目内所有图片资源或角色设定。

如果仍显示旧桌宠图片，确认启动的是新版目录，关闭旧进程后重新启动。

## 模型、TTS 与 ASR
统一模型中心用于查看已集成模型与语音服务状态。真实语音生成需要对应服务、模型、依赖和硬件资源。若服务状态正常但没有声音，检查音频设备、输出音量和服务日志。参考音频应获得授权。

## 自动任务
部署说明列出的固定任务类型：
- `health_check`：检查网关、Ollama、TTS 和资源状态。
- `ollama_inventory`：查看 Ollama 版本和模型清单，不下载或删除模型。
- `voice_sample`：为少量角色生成语音试听。
- `release_check`：备份并运行质量门禁，成功后生成发布包。
- `code_patch`：提交受限的文本文件修改提案，必须人工审核批准。

建议先运行只读检查。批准补丁前核对目标相对路径、文件内容和备份状态。不要把自动任务当作任意 Shell、PowerShell 或 Python 命令执行器。

## 自动任务 API 参考
以下路由来自项目部署说明，实际可用性应以当前安装版本的实现为准：
- `GET /api/v1/automation/status`
- `POST /api/v1/automation/runner/start`，示例正文：`{"periodic_audit": false}`
- `POST /api/v1/automation/runner/stop`
- `GET /api/v1/automation/tasks?limit=50`
- `POST /api/v1/automation/tasks`，示例正文：`{"task_type":"health_check","payload":{},"title":"手动巡检"}`
- `POST /api/v1/automation/tasks/{task_id}/approval`，正文：`{"approved": true}` 或 `{"approved": false}`
- `GET /api/v1/automation/events?limit=100`

当前说明未列出单独的重试 API。任务中断时先检查事件与错误，不要自动重放可能有副作用的任务。

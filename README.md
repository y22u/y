# StarPetFusion 4.10.26

StarPetFusion 是一个面向本地运行的桌宠与角色工作台项目。桌宠形象需在powershell运行python prerare.py从GitHub上下载崩铁大黑塔的Q版形象和大肥鱼形象，也可自行上传，文字版无形象。角色为崩坏星琼铁道中的角色，更细致的设定和角色专属音色需要自己进行补充。

## 文档
- [Windows 安装指南](docs/INSTALL_WINDOWS.md)
- [功能与使用手册](docs/USER_GUIDE.md)
- [架构与 API 说明](docs/ARCHITECTURE.md)
- [故障排查](docs/TROUBLESHOOTING.md)
- [安全与隐私](docs/SECURITY.md)
- [版本记录](CHANGELOG.md)

## 功能概览
- 深色星际控制台风格响应式 UI
- Agent 对话工作区
- 角色设定与资源管理
- 模型及 TTS/ASR 服务状态
- 固定类型自动任务、任务记录与人工审批
- 原生桌宠文字模式修订说明

## 安全提醒
默认仅在本机回环地址运行。不要提交 API Key、`.env`、数据库、日志、模型权重、私人音频或个人配置。修改源码前先备份，代码补丁应人工审核。

## 许可证
请以仓库中的 LICENSE 和第三方资源各自的许可证为准。

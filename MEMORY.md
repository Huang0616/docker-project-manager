# MEMORY.md - 长期记忆

## 👤 身份信息

- **助手名称**：大尾巴猫 🐱
- **用户称呼**：老大
- **时区**：Asia/Shanghai (GMT+8)
- **Git 配置**：Huang0616 / yh3025@nyu.edu

---

## 📦 项目清单

### 1. Docker 项目管理平台
- **仓库**：https://github.com/Huang0616/docker-project-manager
- **端口**：3000
- **功能**：Web UI 管理 Docker 容器（启动/停止/重启/编辑配置）
- **状态**：✅ 运行中
- **注意**：配置文件路径使用容器内路径 `/app/scheduler-tasks/config.json`

### 2. 定时任务管理服务 (scheduler-service)
- **仓库**：https://github.com/Huang0616/scheduler-service
- **端口**：3001
- **功能**：定时任务触发 + 飞书通知
- **定时任务**：
  - 每天 09:00：美股市场早报（热门板块、重要事件、比特币、黄金价格）
  - 每天 19:00：健身提醒
- **状态**：✅ 运行中

### 3. Bootstrap 系统初始化脚本
- **仓库**：https://github.com/Huang0616/bootstrap-system
- **功能**：一键安装开发环境（Homebrew、Node.js、Python、Oh My Zsh 等）
- **状态**：✅ 完成

### 4. Anthropic Blog 监控服务（待完成）
- **位置**：`/Users/huangyifei/.openclaw/workspace/anthropic-blog-monitor`
- **功能**：爬取 Anthropic 官网文章，生成中文摘要，飞书推送
- **技术栈**：FastAPI + APScheduler + PostgreSQL + Next.js
- **状态**：⏸️ 等待 Docker 加速器配置
- **阻塞问题**：Docker Hub 拉取镜像超时

---

## 🔧 系统配置

### OpenClaw 配置
- **主模型**：custom-coding-dashscope-aliyuncs-com/qwen3.5-plus
- **Coder 模型**：codex-cli/gpt-5.3-codex（CLI 模式，无需 API key）
- **飞书配置**：
  - App ID: `cli_a9103d753df8dcc8`
  - 群聊白名单：`oc_93da55eb79d046e138c9f682f34e0980`
- **已修复问题**：
  - 飞书插件重复加载警告（移除 `plugins.entries.feishu`）
  - 群聊白名单配置（`groupAllowFrom` 应填群聊 ID，不是用户 ID）

### Docker 服务
| 服务 | 端口 | 状态 | 备注 |
|------|------|------|------|
| docker-project-manager | 3000 | ✅ healthy | Web UI 管理容器 |
| ollama-embedding | 11434 | ✅ healthy | healthcheck 使用 `ollama list` |

### Docker 加速器配置（待配置）
```json
{
  "registry-mirrors": [
    "https://docker.mirrors.ustc.edu.cn",
    "https://hub.rat.dev"
  ]
}
```

---

## 📝 开发规则（必须遵守）

1. **所有服务默认使用 Docker 部署**
2. **所有服务必须被 docker-project-manager 管理**
3. **Git 提交规则**：每次版本更新或任务完成必须提交，commit message 最前面加 `<clawbot>` 标志

---

## 🎯 经验教训

### Ollama Healthcheck 最佳实践
**错误配置**（容器内无 curl）：
```yaml
healthcheck:
  test: ["CMD", "curl", "-f", "http://localhost:11434/api/tags"]
```

**正确配置**（使用 ollama 自带命令）：
```yaml
healthcheck:
  test: ["CMD-SHELL", "ollama list > /dev/null 2>&1 || exit 1"]
  interval: 30s
  timeout: 10s
  retries: 3
  start_period: 60s
```

### 多 Agent 协作流程
- **Main Agent** (qwen3.5-plus)：日常对话、通用任务，工作空间 `workspace`
- **Coder Agent** (codex-cli)：编程专用任务，工作空间 `workspace`
- **项目文件**：只需保留一份在 `workspace`，两个 agent 共享
- **记忆系统**：
  - 日常日志：`memory/YYYY-MM-DD.md`
  - 长期记忆：`MEMORY.md`（定期整理）

### 代码审查经验（Anthropic 项目）
- 安全漏洞：路径遍历、XXE 防护需完善
- 性能优化：XML 解析缓存、文件遍历优化
- 代码质量：异常处理、类型注解、单元测试覆盖率

---

## 📊 服务监控

### 日常检查项（心跳任务）
- [ ] Docker 容器健康状态
- [ ] Ollama 服务可用性
- [ ] 定时任务执行情况
- [ ] 飞书通知送达

---

*最后更新：2026-02-24*
*整理自：memory/2026-02-22.md, memory/2026-02-23.md, memory/2026-02-24.md*

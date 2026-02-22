# TOOLS.md - Local Notes

Skills define _how_ tools work. This file is for _your_ specifics — the stuff that's unique to your setup.

## What Goes Here

Things like:

- Camera names and locations
- SSH hosts and aliases
- Preferred voices for TTS
- Speaker/room names
- Device nicknames
- Anything environment-specific

## Examples

```markdown
### Cameras

- living-room → Main area, 180° wide angle
- front-door → Entrance, motion-triggered

### SSH

- home-server → 192.168.1.100, user: admin

### TTS

- Preferred voice: "Nova" (warm, slightly British)
- Default speaker: Kitchen HomePod
```

## Why Separate?

Skills are shared. Your setup is yours. Keeping them apart means you can update skills without losing your notes, and share skills without leaking your infrastructure.

---

Add whatever helps you do your job. This is your cheat sheet.

## 🚀 开发规则

### 项目部署规则

**除非另有说明，所有开发的服务必须：**
1. ✅ 使用 Docker 部署
2. ✅ 被 docker-project-manager 管理

**示例：**
```bash
# 构建镜像
docker build -t my-service .

# 运行容器
docker run -d --name my-service -p 8080:8080 my-service

# docker-project-manager 会自动发现并管理
```

**例外情况：**
- 临时测试脚本
- 用户明确说明不使用 Docker

### Git 提交规则

**每次版本更新或任务完成必须：**
1. ✅ 提交到本地 Git 仓库
2. ✅ 推送到远程仓库（如果有远程）
3. ✅ 在 commit message 最前面加 `<clawbot>` 标志

**示例：**
```bash
# 正确的 commit message
<clawbot> Initial commit: Docker 项目管理平台
<clawbot> 添加新功能：容器日志查看
<clawbot> 修复启动/停止按钮问题

# 错误的 ❌
Initial commit: Docker 项目管理平台
添加新功能
```

**提交流程：**
```bash
# 1. 添加修改的文件
git add .

# 2. 提交（必须加 <clawbot> 标志）
git commit -m "<clawbot> 描述内容"

# 3. 推送到远程
git push origin main
```

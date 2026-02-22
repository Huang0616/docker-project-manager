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

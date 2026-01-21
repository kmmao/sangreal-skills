---
name: skillsmp-sync
description: 浏览和同步 SkillsMP (skillsmp.com) 上的 AI Agent Skills
---

# SkillsMP Skills 同步指南

[SkillsMP](https://skillsmp.com/) 是基于 `SKILL.md` 开放标准的 AI Agent Skills 市场，收录超过 80,000 个开源技能。

## 🌐 网站导航

### 主要页面
- **首页**: https://skillsmp.com/
- **分类浏览**: https://skillsmp.com/en/categories
- **文档**: https://skillsmp.com/en/docs
- **API 文档**: https://skillsmp.com/en/docs/api

### 热门分类
| 分类 | 描述 | URL |
|------|------|-----|
| LLM & AI | AI 和大模型相关 | /en/categories/llm-ai |
| Productivity | 生产力工具 | /en/categories/productivity-integration |
| Automation | 自动化工具 | /en/categories/automation-tools |
| Debugging | 调试开发 | /en/categories/debugging |
| CLI Tools | 命令行工具 | /en/categories/cli-tools |

## 🔍 搜索技能

### API 端点（需要 API Key）

```bash
# 关键词搜索
curl -X GET "https://skillsmp.com/api/v1/skills/search?q=<关键词>&limit=20" \
  -H "Authorization: Bearer <API_KEY>"

# AI 语义搜索
curl -X GET "https://skillsmp.com/api/v1/skills/ai-search?q=<自然语言问题>" \
  -H "Authorization: Bearer <API_KEY>"
```

### 浏览器搜索（无需 API Key）

1. 访问 https://skillsmp.com/
2. 使用页面顶部的 `ai --search` 按钮搜索
3. 或使用 `cd /categories` 按分类浏览

## 📥 下载技能

### 方法一：使用 CLI（推荐）

```bash
npx @skillsmp/cli install <skill-path>
```

### 方法二：手动下载

1. 在 SkillsMP 上找到目标技能
2. 点击查看详情获取 GitHub 源链接
3. 复制 SKILL.md 文件内容
4. 保存到本地项目的 skills 目录

### 方法三：从 GitHub 直接获取

大多数技能源自 GitHub 仓库，常见来源：
- `github.com/anthropics/skills`
- `github.com/langgenius/dify`
- 其他社区贡献仓库

## 📂 同步到本地

将下载的技能同步到 `sangreal-skills` 项目：

```bash
# 目标路径
/Users/sangreal/Documents/GitHub/sangreal-skills/plugins/<plugin-name>/skills/<skill-name>/

# 必需文件
- SKILL.md          # 核心技能定义
- README.md         # 文档（可选）
- scripts/          # 脚本文件（如有）
```

## 🔄 定期更新

建议关注以下来源获取最新技能：
1. SkillsMP 首页的 "trending" 技能
2. GitHub 上 anthropics/skills 仓库的更新
3. 社区推荐的新技能

## 📋 技能评估标准

选择技能时考虑：
- ⭐ Stars 数量（受欢迎程度）
- 📅 更新日期（活跃度）
- 📖 文档完善度
- 🔗 源码可访问性
- 🎯 与现有工作流的契合度

# Sangreal Skills

这是 Sangreal 的自定义 Claude 技能集合，用于扩展 Claude Code 的功能。

## 📦 项目结构

```
sangreal-skills/
├── .claude-plugin/
│   └── marketplace.json      # 插件市场配置
├── skills/
│   └── example-skill/        # 示例技能
│       └── SKILL.md
├── template/
│   └── SKILL.md             # 技能模板
└── README.md
```

## 🚀 安装方法

### 方法 1：从 GitHub 安装（推荐）

首先将此仓库推送到 GitHub，然后在 Claude Code 中运行：

```bash
/plugin marketplace add your-github-username/sangreal-skills
```

然后安装技能包：

```bash
/plugin install sangreal-basic-skills@sangreal-skills
```

### 方法 2：本地安装（测试用）

在 Claude Code 中运行：

```bash
/plugin install /Users/allen/Documents/GitHub/notebook/github-projects/sangreal-skills
```

## 📚 可用技能

### sangreal-basic-skills

基础技能合集，包含：

- **example-skill**: 示例技能，演示如何创建自定义技能

## ✍️ 创建新技能

1. 复制 `template/SKILL.md` 到 `skills/new-skill-name/SKILL.md`
2. 编辑 `SKILL.md`，填写技能名称、描述和指令
3. 在 `.claude-plugin/marketplace.json` 的 `skills` 数组中添加新技能路径
4. 测试技能是否正常工作

### 技能文件格式

```markdown
---
name: skill-name
description: 技能描述和使用场景
---

# 技能名称

详细的指令内容...

## 用途
## 使用说明
## 示例
## 指南
```

## 🔧 配置说明

编辑 `.claude-plugin/marketplace.json` 来管理技能：

- **name**: marketplace 名称
- **plugins**: 技能包列表
  - **name**: 插件包名称
  - **description**: 插件包描述
  - **skills**: 技能路径列表

## 📝 许可

根据你的需要添加许可证

## 🤝 贡献

欢迎提交 Issue 和 Pull Request

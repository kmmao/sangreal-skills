# Sangreal Basic Skills

基础技能合集，包含常用的开发和生产力工具。

## 功能概览

### 🔧 斜杠命令 (Commands)

- `/commit [message]` - 智能分析代码变更并创建符合规范的 Git 提交
- `/quick-fix [path]` - 快速修复常见代码问题（格式化、lint 错误等）

### 🤖 智能 Agents

- **code-analyzer** - 深度分析代码质量、性能瓶颈和潜在问题
- **doc-generator** - 自动生成和更新项目文档、API 文档和代码注释

### ⚡ 自动触发技能 (Skills)

- **git-commit** - 智能 Git 提交助手，分析变更并生成符合 Conventional Commits 规范的提交信息
- **example-skill** - 展示如何创建自定义 Claude 技能的示例

## 安装

```bash
# 从 marketplace 安装
/plugin install sangreal-basic-skills@sangreal-skills

# 本地开发安装
/plugin install /path/to/sangreal-skills
```

## 使用说明

### 斜杠命令

```bash
# 智能提交当前变更
/commit

# 带自定义 message 提交
/commit feat: add new feature

# 快速修复整个项目
/quick-fix

# 修复指定文件
/quick-fix src/components/Button.tsx
```

### Skills 自动触发

Skills 会根据对话内容自动激活：

- 说"提交代码"、"创建 commit" → 触发 `git-commit`
- 询问"如何创建技能" → 触发 `example-skill`

## 技术细节

- **Commands**: 使用 YAML frontmatter，支持参数传递和工具预授权
- **Agents**: 使用 Markdown 表格 frontmatter，可配置 model 和工具
- **Skills**: 使用 YAML frontmatter，基于 description 自动触发
- **MCP**: 支持配置外部 MCP 服务器

## 许可证

Apache 2.0

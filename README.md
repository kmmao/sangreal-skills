# Sangreal Skills Marketplace

Sangreal 的 Claude Code 插件市场，包含实用的开发和生产力工具。

## 📦 项目结构

```
sangreal-skills/                    # Marketplace 根目录
├── .claude-plugin/
│   └── marketplace.json            # Marketplace 配置（必需）
├── plugins/                        # 插件目录
│   └── sangreal-basic-skills/      # 基础技能插件
│       ├── .claude-plugin/
│       │   └── plugin.json         # 插件元数据
│       ├── .mcp.json               # MCP 服务器配置
│       ├── skills/                 # 自动触发技能
│       │   ├── example-skill/
│       │   └── git-commit/
│       ├── commands/               # 斜杠命令
│       │   ├── commit.md
│       │   └── quick-fix.md
│       ├── agents/                 # 智能代理
│       │   ├── code-analyzer.md
│       │   └── doc-generator.md
│       └── README.md
├── spec/                           # 开发规范文档
├── template/                       # 插件模板
└── README.md                       # 本文件
```

## 🚀 快速开始

### 添加 Marketplace

```bash
# 添加这个 marketplace 到你的 Claude Code
/plugin marketplace add allen/sangreal-skills
```

### 安装插件

```bash
# 从 marketplace 安装
/plugin install sangreal-basic-skills@sangreal-skills

# 或者本地开发安装
/plugin install /Users/allen/Documents/GitHub/sangreal-skills
```

## 📚 可用插件

### sangreal-basic-skills

**基础技能合集** - 包含常用的开发和生产力工具

**功能：**
- ⚡ 2 个斜杠命令：`/commit`, `/quick-fix`
- 🤖 2 个智能 Agent：代码分析、文档生成
- 🔮 2 个自动技能：Git 提交助手、示例技能

**安装：**
```bash
/plugin install sangreal-basic-skills@sangreal-skills
```

[查看详细文档](./plugins/sangreal-basic-skills/README.md)

## 🛠️ 开发指南

### 创建新插件

1. **创建插件目录**

```bash
mkdir -p plugins/your-plugin-name/.claude-plugin
```

2. **创建 plugin.json**

```json
{
  "name": "your-plugin-name",
  "description": "插件描述",
  "author": {
    "name": "Your Name",
    "email": "your@email.com"
  }
}
```

3. **添加组件**

```bash
# 创建 skill
mkdir -p plugins/your-plugin-name/skills/your-skill
cp template/SKILL.md plugins/your-plugin-name/skills/your-skill/SKILL.md

# 创建 command
touch plugins/your-plugin-name/commands/your-command.md

# 创建 agent
touch plugins/your-plugin-name/agents/your-agent.md
```

4. **注册到 marketplace**

编辑 `.claude-plugin/marketplace.json`：

```json
{
  "plugins": [
    {
      "name": "your-plugin-name",
      "description": "...",
      "version": "1.0.0",
      "author": {
        "name": "Your Name",
        "email": "your@email.com"
      },
      "source": "./plugins/your-plugin-name",
      "category": "productivity"
    }
  ]
}
```

### 组件开发规范

#### Skills (自动触发技能)

```yaml
---
name: skill-name
description: This skill should be used when the user wants to "触发短语1", "触发短语2", or needs...
version: 1.0.0
---

# Skill 内容
```

**关键点：**
- Description 必须用第三人称 `"This skill should be used when..."`
- 用引号包裹具体的触发短语
- 会根据对话内容自动激活

#### Commands (斜杠命令)

```yaml
---
description: 命令简短描述
argument-hint: <required-arg> [optional-arg]
allowed-tools: Read, Bash, Edit
---

# Command 内容

用户参数: $ARGUMENTS
上下文注入: !`command`
```

**关键点：**
- 用户通过 `/command-name` 手动调用
- `$ARGUMENTS` 获取用户输入
- `` !`command` `` 注入命令输出到上下文

#### Agents (智能代理)

```markdown
| name | description | tools | model | color |
| --- | --- | --- | --- | --- |
| agent-name | Agent 描述 | Read, Write, Bash | sonnet | blue |

[Agent 系统提示词...]
```

**关键点：**
- 使用 Markdown 表格作为 frontmatter
- 可选 model: haiku, sonnet, opus
- 可选 color: red, blue, green, yellow, purple

### Marketplace 配置字段

```json
{
  "$schema": "https://anthropic.com/claude-code/marketplace.schema.json",
  "name": "marketplace-name",
  "description": "Marketplace 描述",
  "owner": {
    "name": "Owner Name",
    "email": "owner@email.com"
  },
  "plugins": [
    {
      "name": "plugin-name",              // 必需：插件唯一标识
      "description": "插件描述",           // 必需：简短描述
      "version": "1.0.0",                 // 推荐：语义化版本号
      "author": {                         // 推荐：作者信息
        "name": "Author Name",
        "email": "author@email.com"
      },
      "source": "./plugins/plugin-name",  // 必需：相对路径
      "category": "productivity",         // 推荐：分类
      "homepage": "https://...",          // 可选：主页链接
      "tags": ["tag1", "tag2"],          // 可选：标签
      "strict": false                     // 可选：严格模式
    }
  ]
}
```

**Category 选项：**
- `development` - 开发工具
- `productivity` - 生产力工具
- `testing` - 测试工具
- `security` - 安全工具
- `database` - 数据库工具
- `deployment` - 部署工具
- `monitoring` - 监控工具
- `design` - 设计工具
- `learning` - 学习工具

## 📖 参考资源

- [Claude Code 官方文档](https://code.claude.com/docs)
- [官方插件仓库](https://github.com/anthropics/claude-plugins-official)
- [插件开发工具包](https://github.com/anthropics/claude-plugins-official/tree/main/plugins/plugin-dev)
- [Marketplace Schema](https://anthropic.com/claude-code/marketplace.schema.json)

## 🎯 最佳实践

### Plugin 设计
- ✅ 每个插件专注一个领域
- ✅ 提供清晰的文档和示例
- ✅ 遵循官方命名规范
- ✅ 包含 README.md
- ❌ 避免功能重叠
- ❌ 不要包含过多依赖

### 组件设计
- ✅ Skills 用于自动触发的通用能力
- ✅ Commands 用于用户主动调用的操作
- ✅ Agents 用于复杂的多步骤任务
- ✅ 清晰的触发条件和参数说明
- ❌ 避免过于复杂的逻辑

### Marketplace 管理
- ✅ 使用语义化版本号
- ✅ 提供准确的分类标签
- ✅ 保持插件更新
- ✅ 及时处理 issues
- ❌ 不要发布未测试的版本

## 🤝 贡献

欢迎贡献新插件或改进现有插件！

### 贡献流程

1. Fork 本仓库
2. 创建插件分支：`git checkout -b plugin/your-plugin-name`
3. 在 `plugins/` 目录下创建你的插件
4. 更新 `.claude-plugin/marketplace.json`
5. 提交 Pull Request

### 插件审核标准

- ✅ 功能完整且有用
- ✅ 代码质量良好
- ✅ 包含完整文档
- ✅ 遵循官方规范
- ✅ 通过测试验证

## 📄 许可证

Apache 2.0

---

**由 Claude Code 驱动** | [报告问题](https://github.com/allen/sangreal-skills/issues) | [贡献指南](./CONTRIBUTING.md)

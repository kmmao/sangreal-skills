# Claude Skills 规范

本文档定义了 Sangreal Skills 项目的技能创建规范和最佳实践。

## 技能文件结构

每个技能必须包含一个 `SKILL.md` 文件（注意大写），位于 `skills/<skill-name>/` 目录下。

### 文件格式

```markdown
---
name: skill-name
description: 技能的详细描述，说明何时应该使用此技能
---

# 技能标题

[技能的简短介绍]

## 核心功能

[详细的执行步骤和指令]

## 示例

[具体的使用示例]

## 注意事项

[需要注意的关键点]
```

## Frontmatter 规范

### name（必需）
- 使用小写字母
- 单词之间用连字符 `-` 分隔
- 与目录名保持一致
- 示例：`git-commit`, `example-skill`

### description（必需）
- 清晰描述技能的功能
- 说明 Claude 应该在什么情况下使用此技能
- 长度建议：1-3 句话
- 示例：`智能 Git 提交助手。当用户需要提交代码、生成 commit message 或进行版本控制操作时使用。`

## 内容编写规范

### 1. 简洁原则
- 技能文件是给 Claude 的**执行指令**，不是给人看的教程
- 避免冗长的说明和背景知识
- 直接描述需要执行的步骤

### 2. 结构清晰
推荐的章节结构：
- **核心功能**：描述主要执行步骤
- **示例**：提供具体的使用示例
- **注意事项**：列出关键的注意点

### 3. 示例优先
- 通过具体示例展示用法
- 示例要贴近实际使用场景
- 代码示例要完整可执行

### 4. 长度控制
- 建议总长度：50-120 行
- 核心功能：20-50 行
- 示例：10-30 行
- 注意事项：5-15 行

## 技能注册

在 `.claude-plugin/marketplace.json` 中注册技能：

```json
{
  "plugins": [
    {
      "name": "plugin-name",
      "skills": [
        "./skills/skill-name"
      ]
    }
  ]
}
```

## 测试清单

创建技能后，确保通过以下测试：

- [ ] SKILL.md 文件名是大写
- [ ] frontmatter 包含 name 和 description
- [ ] name 与目录名一致
- [ ] description 清晰描述使用场景
- [ ] 内容简洁，避免冗长说明
- [ ] 包含具体的使用示例
- [ ] 在 marketplace.json 中正确注册
- [ ] 在实际场景中测试技能激活和执行

## 反面示例

❌ **不要这样做：**

```markdown
# Git 智能提交助手

这个技能帮助你更高效、规范地进行 Git 提交操作。

## 用途

此技能用于：
- 自动分析代码变更并生成符合规范的 commit message
- 智能暂存文件（支持选择性暂存）
- 遵循 Conventional Commits 规范
- 提供 commit 最佳实践建议
- 快速执行常见的 Git 工作流

## 使用说明

用户可以通过以下方式触发此技能：
- "提交代码"
- "git commit"
...（还有 300 多行详细说明）
```

**问题：**
- 过于冗长（332 行）
- 包含大量背景知识和教程内容
- 结构复杂，章节过多

✅ **正确做法：**

```markdown
# Git 智能提交助手

自动分析代码变更并生成符合规范的 Git 提交。

## 核心功能

1. 分析变更
   - 运行 git status 和 git diff
   - 理解变更的性质

2. 生成 Commit Message
   - 遵循 Conventional Commits
   - 格式：<type>(<scope>): <subject>

3. 执行提交
   - 询问是否暂存未暂存的文件
   - 执行 git commit

## 示例

feat(auth): add OAuth2 login support
fix(api): resolve memory leak

## 注意事项

- 提交前检查敏感信息
- 每个 commit 应该是独立的工作单元
```

**优点：**
- 简洁明了（约 50 行）
- 直接可执行的指令
- 通过示例展示用法

## 参考资源

- [Anthropic Skills 官方仓库](https://github.com/anthropics/skills)
- [Conventional Commits 规范](https://www.conventionalcommits.org/)

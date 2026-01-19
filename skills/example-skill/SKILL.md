---
name: example-skill
description: 这是一个示例技能，展示如何创建自定义 Claude 技能。当用户需要了解技能结构或创建新技能时使用。
---

# 示例技能

演示 Claude Skills 的基本结构和最佳实践。

## 技能文件结构

每个技能包含两部分：

1. **YAML Frontmatter（元数据）**
   - `name`: 技能唯一标识符（小写，用连字符分隔）
   - `description`: 详细说明技能功能和使用场景

2. **Markdown Body（指令内容）**
   - 简洁的功能说明
   - 清晰的执行步骤
   - 具体的使用示例

## 创建新技能的步骤

1. 复制 `template/SKILL.md` 到 `skills/your-skill-name/SKILL.md`
2. 修改 frontmatter 中的 name 和 description
3. 编写简洁的指令（避免冗长的说明文档）
4. 在 `.claude-plugin/marketplace.json` 中注册技能路径
5. 测试技能是否正常激活

## 最佳实践

- **简洁明了**：指令要直接可执行，不是教科书
- **聚焦核心**：只描述必要的步骤，避免过度说明
- **示例优先**：通过示例展示用法比长篇描述更有效
- **清晰触发**：description 要准确描述何时使用此技能

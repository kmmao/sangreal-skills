# Sangreal Skills

Sangreal 的自定义 Claude 技能集合。

## 项目结构

```
sangreal-skills/
├── .claude-plugin/
│   └── marketplace.json      # 插件市场配置
├── skills/                   # 技能库
│   ├── example-skill/        # 示例技能
│   └── git-commit/           # Git 提交助手
├── spec/                     # 技能规范文档
├── template/                 # 技能模板
│   └── SKILL.md
└── README.md
```

## 安装方法

### 从 GitHub 安装

1. 添加 marketplace：
```bash
/plugin marketplace add your-github-username/sangreal-skills
```

2. 安装技能包：
```bash
/plugin install sangreal-basic-skills@sangreal-skills
```

### 本地开发安装

```bash
/plugin install /path/to/sangreal-skills
```

## 可用技能

### sangreal-basic-skills

基础技能合集：

- **example-skill**: 展示如何创建自定义 Claude 技能
- **git-commit**: 智能 Git 提交助手，自动生成符合规范的 commit message

## 创建新技能

1. 从模板创建技能文件：
```bash
mkdir -p skills/your-skill-name
cp template/SKILL.md skills/your-skill-name/SKILL.md
```

2. 编辑 `skills/your-skill-name/SKILL.md`：
   - 修改 frontmatter 中的 `name` 和 `description`
   - 编写简洁的执行指令（不是说明文档）
   - 提供具体的使用示例

3. 在 `.claude-plugin/marketplace.json` 中注册：
```json
{
  "skills": [
    "./skills/your-skill-name"
  ]
}
```

4. 测试技能激活和执行

## 技能文件格式

```markdown
---
name: skill-name
description: 清晰描述技能功能和使用场景
---

# 技能名称

[简短介绍]

## 核心功能

[执行步骤]

## 示例

[具体示例]
```

## 最佳实践

- **简洁优先**：技能指令要直接可执行，避免冗长说明
- **示例驱动**：通过示例展示用法，而不是长篇文字
- **明确触发**：description 要准确描述何时激活此技能
- **测试验证**：创建后在实际场景中测试技能是否正常工作

## 许可证

Apache 2.0

## 贡献

欢迎提交 Issue 和 Pull Request。

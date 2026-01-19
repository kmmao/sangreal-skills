---
name: git-commit
description: This skill should be used when the user wants to "提交代码", "commit", "生成 commit message", "git 提交", or needs help with Git version control operations including analyzing code changes, creating conventional commit messages, and staging files.
version: 1.0.0
---

# Git 智能提交助手

自动分析代码变更并生成符合规范的 Git 提交。

## 核心功能

当用户请求提交代码时，按以下步骤执行：

### 1. 分析变更
- 运行 `git status` 查看工作区状态
- 运行 `git diff` 查看未暂存变更
- 运行 `git diff --staged` 查看已暂存变更
- 理解变更的性质和影响范围

### 2. 生成 Commit Message

遵循 Conventional Commits 规范：

```
<type>(<scope>): <subject>

<body>

<footer>
```

**Type 类型：**
- `feat`: 新功能
- `fix`: 修复 bug
- `docs`: 文档更新
- `style`: 代码格式（不影响代码运行）
- `refactor`: 重构
- `perf`: 性能优化
- `test`: 测试相关
- `chore`: 构建过程或辅助工具的变动
- `ci`: CI 配置文件和脚本的变动
- `build`: 影响构建系统或外部依赖的更改

**Subject 规范：**
- 使用祈使句，现在时态（"add" 不是 "added"）
- 不要大写首字母
- 结尾不加句号
- 限制在 50 个字符内

**Body 规范（可选）：**
- 详细说明 what 和 why，而不是 how
- 每行不超过 72 个字符
- 使用列表说明多个变更点

**Footer 规范（可选）：**
- 引用相关的 issue：`Closes #123` 或 `Fixes #456`
- 标注破坏性变更：`BREAKING CHANGE: description`

### 3. 执行提交

- 如果有未暂存的文件，询问用户是否需要暂存
- 使用生成的 message 执行 `git commit`
- 确认提交成功

## 示例

**功能开发：**
```
feat(auth): add OAuth2 login support

- Implement OAuth2 authentication flow
- Add Google and GitHub providers
- Update user model to support social login
```

**Bug 修复：**
```
fix(api): resolve memory leak in data processing

The previous implementation didn't properly release resources
after processing large datasets.

Fixes #456
```

**破坏性变更：**
```
feat(api)!: change authentication endpoint structure

BREAKING CHANGE: The /auth endpoint now returns a different response format.

Before: { token: "..." }
After: { access_token: "...", refresh_token: "..." }
```

## 提交前检查

在提交前确认：
- ✓ 代码没有语法错误
- ✓ 没有调试代码（console.log、debugger 等）
- ✓ 没有敏感信息（密钥、密码等）
- ✓ 提交信息清晰准确

## 注意事项

- 频繁提交小的、逻辑完整的变更
- 每个 commit 应该是一个独立的、可工作的单元
- 避免一次性提交大量不相关的变更
- 不要提交编译产物（应该在 .gitignore 中）
- 不要写无意义的 message（如 "update"、"fix"）

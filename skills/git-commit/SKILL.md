---
name: git-commit
description: 智能 Git 提交助手。当用户需要提交代码、生成 commit message 或进行版本控制操作时使用。支持分析代码变更、生成符合规范的提交信息、暂存文件等 Git 工作流。
---

# Git 智能提交助手

这个技能帮助你更高效、规范地进行 Git 提交操作。

## 用途

此技能用于：
- 自动分析代码变更并生成符合规范的 commit message
- 智能暂存文件（支持选择性暂存）
- 遵循 Conventional Commits 规范
- 提供 commit 最佳实践建议
- 快速执行常见的 Git 工作流

## 核心功能

### 1. 智能提交流程

当用户请求提交代码时，按以下步骤执行：

1. **检查工作区状态**
   ```bash
   git status
   ```

2. **分析变更内容**
   - 使用 `git diff` 查看未暂存的变更
   - 使用 `git diff --staged` 查看已暂存的变更
   - 理解变更的性质和影响范围

3. **生成 Commit Message**

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
   - `refactor`: 重构（既不是新功能也不是修复bug）
   - `perf`: 性能优化
   - `test`: 测试相关
   - `chore`: 构建过程或辅助工具的变动
   - `ci`: CI配置文件和脚本的变动
   - `build`: 影响构建系统或外部依赖的更改

4. **执行提交**
   - 如果有未暂存的文件，先询问用户是否需要暂存
   - 使用生成的 message 提交
   - 确认提交成功

### 2. 提交信息规范

**好的 Commit Message 示例：**
```
feat(auth): add OAuth2 login support

- Implement OAuth2 authentication flow
- Add Google and GitHub providers
- Update user model to support social login

Closes #123
```

```
fix(api): resolve memory leak in data processing

The previous implementation didn't properly release resources
after processing large datasets.

Fixes #456
```

**Subject 规范：**
- 使用祈使句，现在时态（"add" 不是 "added" 或 "adds"）
- 不要大写首字母
- 结尾不加句号
- 限制在 50 个字符内
- 清晰描述做了什么

**Body 规范：**
- 详细说明 what 和 why，而不是 how
- 每行不超过 72 个字符
- 可以包含多个段落
- 使用列表说明多个变更点

**Footer 规范：**
- 引用相关的 issue：`Closes #123` 或 `Fixes #456`
- 标注破坏性变更：`BREAKING CHANGE: description`

### 3. 文件暂存策略

当有多个未暂存文件时：
- 询问用户是暂存全部还是选择性暂存
- 对于选择性暂存，列出文件清单让用户选择
- 支持 `git add -p` 进行部分暂存

### 4. 提交前检查

在提交前确认：
- ✓ 代码是否有语法错误
- ✓ 是否有调试代码（console.log、debugger等）
- ✓ 是否有敏感信息（密钥、密码等）
- ✓ 提交信息是否清晰准确
- ✓ 是否需要更新相关文档

## 使用说明

### 基础使用

用户可以通过以下方式触发此技能：
- "提交代码"
- "git commit"
- "帮我写个 commit message"
- "提交这些变更"
- "生成提交信息"

### 高级用法

**快速提交（跳过分析）：**
```
"快速提交：修复登录bug"
```

**修改上次提交：**
```
"修改上次提交的message"
```

**暂存并提交特定文件：**
```
"只提交 src/auth.ts 和 src/login.ts"
```

## 工作流示例

### 示例 1：标准提交流程

```
用户："帮我提交代码"

助手：
1. 检查 git status
2. 发现有 3 个修改的文件
3. 使用 git diff 分析变更
4. 生成提交信息：
   feat(user): add profile update functionality

   - Add updateProfile API endpoint
   - Implement profile form validation
   - Add unit tests for profile updates
5. 询问用户是否确认
6. 执行 git add . && git commit
```

### 示例 2：选择性提交

```
用户："只提交认证相关的文件"

助手：
1. 列出所有变更文件
2. 识别认证相关文件（auth.ts, login.ts等）
3. 暂存这些文件
4. 生成针对性的 commit message
5. 执行提交
```

### 示例 3：修复紧急 Bug

```
用户："紧急修复：用户无法登出"

助手：
识别为 bug 修复，生成：
fix(auth): resolve logout session cleanup issue

The logout function wasn't properly clearing the session token,
causing users to remain logged in after clicking logout.

Fixes #789
```

## 最佳实践

### 提交频率
- 频繁提交小的、逻辑完整的变更
- 每个 commit 应该是一个独立的、可工作的单元
- 避免一次性提交大量不相关的变更

### 提交粒度
- 一个功能 = 多个小 commit（开发过程中）
- 准备 merge 时可以 squash 相关 commit
- 每个 commit 都应该能通过测试

### 消息质量
- 写清晰的 subject，让人一眼看懂做了什么
- 对于复杂变更，在 body 中详细说明
- 引用相关的 issue 和 PR

### 避免事项
- ❌ 不要提交调试代码
- ❌ 不要提交编译产物（应该在 .gitignore 中）
- ❌ 不要提交敏感信息
- ❌ 不要写无意义的 message（如"update"、"fix"）
- ❌ 不要在一个 commit 中混合多个不相关的变更

## 特殊场景处理

### 破坏性变更（Breaking Changes）

当变更会破坏向后兼容性时：
```
feat(api)!: change authentication endpoint structure

BREAKING CHANGE: The /auth endpoint now returns a different response format.
Migration guide: update your client code to use the new token structure.

Before: { token: "..." }
After: { access_token: "...", refresh_token: "..." }
```

### 回滚提交（Revert）

```
revert: feat(user): add profile update functionality

This reverts commit abc123def456.

Reason: The feature caused performance issues in production.
```

### WIP 提交（临时保存）

```
wip: user profile implementation

Temporary commit to save progress. Not ready for review.
```

## 集成工具建议

### 配置 Git Hooks

建议配置以下 hooks：
- `pre-commit`: 运行 linter 和格式化工具
- `commit-msg`: 验证 commit message 格式
- `pre-push`: 运行测试套件

### 使用 Commitlint

配置 commitlint 确保 commit message 规范：
```bash
npm install --save-dev @commitlint/cli @commitlint/config-conventional
```

## 快捷命令

执行此技能时会智能判断并使用以下命令：

- `git status` - 查看工作区状态
- `git diff` - 查看未暂存变更
- `git diff --staged` - 查看已暂存变更
- `git add <files>` - 暂存文件
- `git add .` - 暂存所有变更
- `git add -p` - 交互式暂存
- `git commit -m "message"` - 提交
- `git commit --amend` - 修改上次提交
- `git log --oneline -n 5` - 查看最近提交

## 交互模式

当用户需要更多控制时，提供交互式选项：

1. **暂存选项：**
   - 全部暂存
   - 选择性暂存（列出文件清单）
   - 交互式暂存（git add -p）

2. **Commit Message 选项：**
   - 使用生成的 message
   - 手动编辑 message
   - 选择 commit type

3. **提交后操作：**
   - 立即 push
   - 继续在本地工作
   - 创建 pull request

## 错误处理

遇到以下情况时的处理方式：

- **工作区干净（无变更）：** 提示用户当前没有需要提交的内容
- **有未暂存的文件：** 询问是否需要暂存
- **Commit message 不规范：** 提供修正建议
- **检测到敏感信息：** 警告并阻止提交
- **提交失败：** 分析错误原因并提供解决方案

## 注意事项

1. **安全第一**
   - 始终检查是否有敏感信息
   - 确认 .gitignore 正确配置
   - 避免提交大文件

2. **保持清晰**
   - Commit message 要让团队成员一眼看懂
   - 复杂变更需要详细说明
   - 引用相关的 issue 和文档

3. **遵循团队规范**
   - 如果团队有自定义的 commit 规范，优先遵循
   - 保持与团队一致的提交粒度
   - 遵守分支策略

4. **测试优先**
   - 确保提交的代码能够工作
   - 相关测试已通过
   - 不要提交破坏构建的代码

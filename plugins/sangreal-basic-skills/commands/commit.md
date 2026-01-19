---
description: 智能分析代码变更并创建符合规范的 Git 提交
argument-hint: [commit-message]
allowed-tools: Bash(git add:*), Bash(git status:*), Bash(git commit:*), Bash(git diff:*), Bash(git log:*)
---

# Git 智能提交命令

快速创建符合 Conventional Commits 规范的 Git 提交。

## 上下文信息

* 当前 Git 状态: !`git status`
* 当前变更（已暂存和未暂存）: !`git diff HEAD`
* 当前分支: !`git branch --show-current`
* 最近提交: !`git log --oneline -10`

## 参数

用户提供的参数: $ARGUMENTS

## 执行任务

根据上述变更，创建一个符合规范的 Git 提交。

### 步骤：

1. **分析变更**：理解代码变更的性质（新功能、修复、重构等）
2. **暂存文件**：如果有未暂存的文件，使用 `git add` 暂存相关文件
3. **生成提交信息**：
   - 如果用户提供了参数（$ARGUMENTS），使用它作为 commit message
   - 否则，根据变更自动生成符合 Conventional Commits 的 message
   - 格式：`<type>(<scope>): <subject>`
   - Type: feat, fix, docs, style, refactor, perf, test, chore, ci, build
4. **执行提交**：使用生成的 message 创建提交
5. **确认结果**：运行 `git status` 确认提交成功

## 提交信息规范

- 使用祈使句（"add" 而非 "added"）
- Subject 不大写首字母
- Subject 不加句号
- 限制在 50 个字符内
- 添加 Co-Authored-By: Claude <noreply@anthropic.com>

## 注意事项

- 不要提交敏感信息（密钥、密码等）
- 不要提交调试代码（console.log、debugger 等）
- 确保每个 commit 是一个独立的、可工作的单元

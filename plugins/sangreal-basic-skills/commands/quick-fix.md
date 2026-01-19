---
description: 快速修复常见代码问题（格式化、lint 错误等）
argument-hint: [file-path]
allowed-tools: Read, Edit, Bash, Glob, Grep
---

# 快速修复命令

自动检测并修复常见的代码问题。

## 参数

目标文件或目录: $ARGUMENTS

## 执行任务

1. **识别问题**：
   - 运行 linter（如果项目有配置）
   - 检查常见格式问题
   - 查找明显的代码错误

2. **自动修复**：
   - 修复可自动修复的 lint 错误
   - 统一代码格式
   - 移除无用的 import
   - 修正明显的拼写错误

3. **报告结果**：
   - 列出已修复的问题
   - 列出需要手动修复的问题
   - 显示修改的文件列表

## 示例用法

```
/quick-fix src/components/Button.tsx
/quick-fix src/
/quick-fix
```

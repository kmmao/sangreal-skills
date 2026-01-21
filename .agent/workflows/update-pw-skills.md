---
description: 检查并同步 pw-skills 上游仓库的更新
---

# 同步 pw-skills 上游更新

此工作流用于检查并同步 `plugins-world/pw-skills` 仓库的最新更新到本地的 `pw-image-skills` 插件。

## 📋 步骤

### 1. 克隆最新的上游仓库

```bash
cd /tmp
rm -rf pw-skills
git clone https://github.com/plugins-world/pw-skills.git
cd pw-skills
```

### 2. 查看上游变更历史

```bash
# 查看提交历史
git log --oneline --graph --all -20

# 查看自上次同步以来的变更（需要替换日期）
git log --since="2026-01-22" --oneline --pretty=format:"%h - %s (%cd)" --date=short
```

### 3. 对比差异

```bash
# 对比 pw-image-generation 技能的差异
diff -r /tmp/pw-skills/pw-image-generation /Users/sangreal/Documents/GitHub/sangreal-skills/plugins/pw-image-skills/skills/pw-image-generation

# 对比 pw-redbook-image 技能的差异
diff -r /tmp/pw-skills/pw-redbook-image /Users/sangreal/Documents/GitHub/sangreal-skills/plugins/pw-image-skills/skills/pw-redbook-image
```

### 4. 检查重要文件变更

```bash
# 检查 package.json 是否有变更
diff /tmp/pw-skills/pw-image-generation/package.json /Users/sangreal/Documents/GitHub/sangreal-skills/plugins/pw-image-skills/skills/pw-image-generation/package.json

# 检查 SKILL.md 是否有变更
diff /tmp/pw-skills/pw-image-generation/SKILL.md /Users/sangreal/Documents/GitHub/sangreal-skills/plugins/pw-image-skills/skills/pw-image-generation/SKILL.md
```

### 5. 备份当前版本

```bash
cd /Users/sangreal/Documents/GitHub/sangreal-skills
cp -r plugins/pw-image-skills plugins/pw-image-skills.backup.$(date +%Y%m%d)
```

### 6. 应用更新

```bash
# 复制更新的文件
cp -r /tmp/pw-skills/pw-image-generation /Users/sangreal/Documents/GitHub/sangreal-skills/plugins/pw-image-skills/skills/
cp -r /tmp/pw-skills/pw-redbook-image /Users/sangreal/Documents/GitHub/sangreal-skills/plugins/pw-image-skills/skills/

# 如果 package.json 有更新，重新安装依赖
cd /Users/sangreal/Documents/GitHub/sangreal-skills/plugins/pw-image-skills/skills/pw-image-generation
npm install
```

### 7. 更新版本号和文档

更新 `.claude-plugin/plugin.json` 中的版本号：

```json
{
  "version": "1.x.x",  // 相应递增
  "upstream": {
    "lastSync": "YYYY-MM-DD"
  }
}
```

在 `UPSTREAM.md` 中添加同步记录：

```markdown
### 📅 YYYY-MM-DD - 更新说明

**同步类型**: 增量更新

**变更内容**:
- [列出主要变更]

**上游提交**: [git commit hash]

**破坏性变更**: 无
```

### 8. 测试功能

// turbo
```bash
# 在 Claude Code 中测试技能是否正常工作
echo "请测试以下功能："
echo "1. 使用 pw-image-generation 生成一张测试图片"
echo "2. 使用 pw-redbook-image 生成小红书风格图片"
```

### 9. 提交变更

```bash
cd /Users/sangreal/Documents/GitHub/sangreal-skills
git add plugins/pw-image-skills/
git commit -m "chore(pw-image-skills): 同步上游更新 - $(date +%Y-%m-%d)"
```

## 💡 快速命令

如果让 Claude 帮你执行，可以说：

```
请执行 /update-pw-skills 工作流，检查并同步 pw-skills 的最新更新
```

## ⚠️ 注意事项

1. **保留配置文件**: 确保不要覆盖本地的 API Key 配置
2. **检查依赖变更**: 如果 `package.json` 有更新，务必运行 `npm install`
3. **测试后提交**: 确保更新后功能正常再提交到 git
4. **记录变更**: 在 `UPSTREAM.md` 中详细记录本次同步的内容

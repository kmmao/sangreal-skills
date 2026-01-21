# 上游同步记录

此文档记录 `pw-image-skills` 插件与上游仓库 [plugins-world/pw-skills](https://github.com/plugins-world/pw-skills) 的同步历史。

## 📌 上游仓库信息

- **仓库地址**: https://github.com/plugins-world/pw-skills
- **作者**: 牟勇 (plugins-world)
- **联系方式**: 
  - 网站: https://ai-router.plugins-world.cn
  - 微信: 1254074921

## 📋 同步历史

### 🆕 2026-01-22 - 初始导入

**同步类型**: 全量导入

**导入内容**:
- ✅ `pw-image-generation` 技能（包含所有脚本和配置）
- ✅ `pw-redbook-image` 技能（包含模板和参考文件）
- ✅ 原始 README.md 和文档

**上游提交**: 初始克隆

**本地修改**:
- 创建 `.claude-plugin/plugin.json` 配置文件
- 创建 `README.md` 插件说明文档
- 创建 `UPSTREAM.md` 同步跟踪文档

**注意事项**:
- npm 依赖需要在 `pw-image-generation` 目录下执行 `npm install`
- 需要配置 ai-router API Key 才能使用

---

## 🔄 如何同步最新版本

### 方法一：手动同步（推荐）

1. **克隆最新的上游仓库**
```bash
cd /tmp
git clone https://github.com/plugins-world/pw-skills.git
cd pw-skills
```

2. **查看变更**
```bash
# 查看提交历史，找出自上次同步以来的变更
git log --since="2026-01-22" --oneline
```

3. **对比差异**
```bash
# 对比 pw-image-generation 的变更
diff -r /tmp/pw-skills/pw-image-generation ~/.claude/plugins/pw-image-skills/skills/pw-image-generation

# 对比 pw-redbook-image 的变更
diff -r /tmp/pw-skills/pw-redbook-image ~/.claude/plugins/pw-image-skills/skills/pw-redbook-image
```

4. **应用更新**
```bash
# 备份当前版本
cp -r ~/.claude/plugins/pw-image-skills ~/.claude/plugins/pw-image-skills.backup

# 复制新版本
cp -r /tmp/pw-skills/pw-image-generation ~/.claude/plugins/pw-image-skills/skills/
cp -r /tmp/pw-skills/pw-redbook-image ~/.claude/plugins/pw-image-skills/skills/

# 重新安装依赖（如果 package.json 有更新）
cd ~/.claude/plugins/pw-image-skills/skills/pw-image-generation
npm install
```

5. **更新记录**

在本文档中添加新的同步记录，格式如下：

```markdown
### 📅 YYYY-MM-DD - 更新说明

**同步类型**: 增量更新 / 重大更新

**变更内容**:
- [具体变更说明]

**上游提交**: [commit hash]

**本地修改**:
- [如果有本地修改的话]

**破坏性变更**:
- [如果有的话]
```

### 方法二：使用 Git Submodule（未来考虑）

如果希望自动跟踪上游更新，可以考虑使用 git submodule：

```bash
# 将上游仓库作为 submodule 添加
cd /Users/sangreal/Documents/GitHub/sangreal-skills
git submodule add https://github.com/plugins-world/pw-skills.git .upstream/pw-skills

# 定期更新
git submodule update --remote .upstream/pw-skills
```

### 方法三：让 Claude 帮忙

直接告诉 Claude：

```
请帮我检查 pw-skills 上游仓库是否有更新，并同步到我的 pw-image-skills 插件
```

## ⚠️ 同步注意事项

1. **保留本地配置**: 同步时注意保留本地的 API Key 配置文件
2. **检查依赖变更**: 如果 `package.json` 有更新，需要重新运行 `npm install`
3. **测试功能**: 更新后测试各个技能是否正常工作
4. **更新文档**: 同步后更新本文档的同步记录
5. **版本号管理**: 更新 `.claude-plugin/plugin.json` 中的版本号

## 📝 本地修改追踪

如果对技能进行了本地定制，请在此记录：

### 本地定制列表

目前无本地定制。

---

**最后更新**: 2026-01-22
**维护者**: Sangreal

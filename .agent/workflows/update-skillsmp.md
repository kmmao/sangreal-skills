---
description: 浏览和同步 SkillsMP 网站上的 AI Agent Skills
---

# 同步 SkillsMP Skills

此工作流用于从 [SkillsMP](https://skillsmp.com/) 发现和同步优质的 AI Agent Skills。

## 📋 步骤

### 1. 浏览热门技能

使用浏览器访问以下页面：

```
https://skillsmp.com/en/categories
```

热门分类推荐：
- **LLM & AI**: `/en/categories/llm-ai`
- **Productivity**: `/en/categories/productivity-integration`
- **CLI Tools**: `/en/categories/cli-tools`

### 2. 搜索特定技能

访问首页使用搜索功能：

```
https://skillsmp.com/
```

点击 `ai --search` 按钮进行语义搜索。

### 3. 查看技能详情

找到感兴趣的技能后：
1. 点击进入详情页
2. 查看 SKILL.md 源码
3. 获取 GitHub 源链接

### 4. 下载技能

// turbo
```bash
# 使用 CLI 安装（如果知道路径）
npx @skillsmp/cli install <skill-path>
```

或手动从 GitHub 克隆：

```bash
cd /tmp
git clone <github-repo-url>
```

### 5. 同步到本地

```bash
# 将技能复制到项目中
cp -r /tmp/<skill-name> /Users/sangreal/Documents/GitHub/sangreal-skills/plugins/sangreal-basic-skills/skills/
```

### 6. 记录同步

在相关的 UPSTREAM.md 中添加记录：

```markdown
### 📅 YYYY-MM-DD - 从 SkillsMP 同步

**来源**: SkillsMP / <原始仓库>
**技能**: <技能名称>
**描述**: <简要描述>
```

### 7. 验证技能

确认技能文件结构正确：
- 包含 SKILL.md 或符合规范的配置
- 必要的依赖已安装

## 💡 快速命令

```
请执行 /update-skillsmp 工作流，帮我从 SkillsMP 寻找 <关键词> 相关的技能
```

## ⚠️ 注意事项

1. **检查许可证**: 确保技能的开源许可证允许使用
2. **测试功能**: 同步后测试技能是否正常工作
3. **保持更新**: 定期查看技能源仓库的更新
4. **本地修改**: 如有本地定制，记录在 UPSTREAM.md 中

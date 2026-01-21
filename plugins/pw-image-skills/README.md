# PW Image Skills

AI 图像生成工作流技能集，包含文生图、图生图、批量生成和小红书风格图片生成功能。

## 📦 包含的技能

### 1. pw-image-generation
**AI 图像生成工作流** - 全面的图像生成解决方案

**功能特性：**
- 🎨 **文生图**：根据文本描述生成图像
- 🖼️ **图生图**：基于参考图生成新图像
- 📚 **批量生成**：一次性生成多张图片
- 🔗 **图片拼接**：创建长图
- 📊 **PPT 支持**：基础的 PPT 生成功能

**工作流程：**
1. 分析风格需求
2. 设计提示词
3. 安装依赖
4. 配置 API
5. 生成并保存图像

### 2. pw-redbook-image
**小红书风格图片生成** - 专门为小红书内容创作设计

**功能特性：**
- 📱 小红书风格图片系列生成
- 📄 将文章/文本拆分为图片系列
- 🎯 包含封面、内容页、结尾页
- 🎨 专业的提示词模板

**依赖：**
需要 `pw-image-generation` 技能进行实际的图像生成。

## 🚀 安装

### 前置要求
- Node.js 环境
- ai-router API Key

### 安装步骤

1. **从 marketplace 安装插件**
```bash
/plugin install pw-image-skills@sangreal-skills
```

2. **安装 npm 依赖**
```bash
cd ~/.claude/plugins/pw-image-skills/skills/pw-image-generation
npm install
```

3. **配置 API Key**

在 `pw-image-generation/config/` 目录下创建配置文件，参考 `config.example/` 中的示例。

**获取 API Key**：https://ai-router.plugins-world.cn/console/token

**注意事项：**
- API Key 是 ai-router 的密钥，支持多种模型
- 需要 GitHub 登录，请确保 GitHub 账号已开放邮箱展示

## 🎯 快速开始

### 生成图片示例

让 Claude 帮你生成图片：

```
请使用 pw-image-generation 生成一张图片：
- 内容：赛博朋克风格的城市夜景
- 尺寸：1024x1024
- 风格：科幻、霓虹灯、未来感
```

### 生成小红书风格图片

```
请使用 pw-redbook-image 帮我生成小红书图片系列：
- 主题：健康饮食指南
- 包含：封面 + 3 个内容页 + 结尾页
```

## 🔧 支持的模型

- **gemini-3-pro-image-preview**: Google Gemini 3 Pro 图像预览模型（生成）
- **gemini-2.0-flash-exp**: Google Gemini 2.0 Flash 实验模型（分析）
- 其他支持图像生成的模型

## 📚 详细文档

- [pw-image-generation 详细文档](./skills/pw-image-generation/SKILL.md)
- [pw-redbook-image 详细文档](./skills/pw-redbook-image/SKILL.md)

## 👤 原作者

**牟勇**
- 网站：https://ai-router.plugins-world.cn
- 微信：1254074921

## 📄 上游信息

- **原始仓库**：https://github.com/plugins-world/pw-skills
- **最后同步**：2026-01-22
- **维护者**：Sangreal

## 🔄 更新说明

此插件从 `plugins-world/pw-skills` 仓库同步。如需更新到最新版本，请参考 [UPSTREAM.md](./UPSTREAM.md) 文档。

## 📝 许可证

遵循原项目许可证。详见原仓库：https://github.com/plugins-world/pw-skills

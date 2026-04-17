# 贡献指南

> 如何为 Open Skills 项目贡献新技能、修复问题、提出建议

---

## 贡献方式

欢迎以以下方式参与贡献：

- 🐛 **提交 Issue** - 反馈问题或提出新技能建议
- 🔧 **提交 PR** - 修复问题或新增技能
- 📢 **分享传播** - 推荐给更多需要的朋友
- ⭐ **点亮 Star** - 支持项目持续更新

---

## 提交 Issue

### 反馈问题

在 [GitHub Issues](https://github.com/javastarboy/open-skills/issues) 提交：

**标题格式**：
```
[技能名称] 问题简述
```

**示例**：
```
[blog-rewriter] 链接抓取失败，提示 403 错误
```

**内容包含**：
- 问题描述
- 使用环境（ClawHub 版本、系统）
- 重现步骤
- 期望结果
- 实际结果

---

### 提出新技能建议

**标题格式**：
```
[Feature Request] 新技能名称 - 简短描述
```

**示例**：
```
[Feature Request] video-script-writer - 视频脚本创作技能
```

**内容包含**：
- 技能定位和目标
- 核心功能列表
- 使用场景
- 期望输出
- 参考资料（如有）

---

## 提交 PR

### 贡献流程

```
1. Fork 本仓库
2. 创建新分支 (feature/your-skill-name)
3. 开发技能
4. 测试验证
5. 提交更改
6. 发起 Pull Request
```

---

### 新技能开发步骤

#### 1. 创建技能目录

```bash
mkdir -p your-skill-name/scripts your-skill-name/references your-skill-name/output
```

#### 2. 编写 SKILL.md

创建 `your-skill-name/SKILL.md`：

```yaml
---
name: your-skill-name
description: 技能简短描述（<50字，用于 ClawHub 搜索）
---

# 技能标题

一句话定位说明

## 核心能力
...

## 快速开始
...

## 工作流程
...

## 输出格式
...

## 用户自定义配置
...

## 异常处理
...

## 质量检查清单
...
```

参考：[技能开发最佳实践](../concepts/skill-development.md)

#### 3. 开发脚本（如需要）

创建 `scripts/main.js` 或其他脚本文件。

#### 4. 编写参考文档

在 `references/` 目录添加配置文件、指南文档。

#### 5. 测试验证

在 ClawHub 环境测试：
- 导入技能
- 执行任务
- 检查输出
- 验证配置

---

### PR 提交规范

**标题格式**：
```
[Add/Fix/Update] 简短描述
```

**示例**：
```
[Add] 新增 video-script-writer 技能
[Fix] 修复 blog-rewriter 链接抓取失败问题
[Update] 更新 ai-news-xiaohongshu 配置说明
```

**内容包含**：
- 变更内容说明
- 测试验证结果
- 相关 Issue（如有）
- 技能使用示例（新技能）

---

## 技能开发规范

### 目录结构

```
skill-name/
├── SKILL.md           # 必需
├── README.md          # 推荐
├── scripts/           # 按需
├── references/        # 按需
│   └── user-config.md # 用户配置
├── assets/            # 按需
└── output/            # 自动生成
```

### SKILL.md 要求

必须包含：
- YAML frontmatter（name、description）
- 技能定位说明
- 核心能力列表
- 使用步骤
- 输出格式
- 配置说明（如有）

### 工具集成说明

明确说明使用的 ClawHub 工具：
- web_search
- tavily-search
- browser
- web_fetch

参考：[ClawHub 平台集成](../concepts/clawhub-integration.md)

---

## 分享传播

### 推荐方式

- 分享到社交媒体
- 推荐给有需要的朋友
- 在技术社区介绍项目
- 写使用体验文章

---

## 点亮 Star

在 [GitHub 仓库](https://github.com/javastarboy/open-skills) 点击 Star ⭐

支持项目持续更新和优化。

---

## 获取帮助

开发过程中遇到问题：

- 💬 联系微信：LHYYH0001
- 📝 作者博客：https://www.yuque.com/lhyyh
- 🔗 联系作者：https://www.yuque.com/lhyyh/ai/conactus
- 📝 查看 [Issues](https://github.com/javastarboy/open-skills/issues)

---

## 相关页面

- [技能开发最佳实践](../concepts/skill-development.md)
- [ClawHub 平台集成](../concepts/clawhub-integration.md)
- [快速开始](getting-started.md)
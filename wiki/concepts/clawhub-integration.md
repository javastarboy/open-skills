# ClawHub 平台集成

![ClawHub](https://img.shields.io/badge/Platform-ClawHub-orange)

> Open Skills 所有技能基于 ClawHub 平台开发，集成平台工具和工作流程

---

## ClawHub 平台简介

**ClawHub** 是 AI 技能部署和管理平台，提供：
- 技能运行环境（OpenClaw）
- 工具集成（web_search、tavily-search 等）
- 技能配置规范（SKILL.md）
- 工作流程自动化

平台地址：https://clawhub.ai

---

## 技能集成方式

### SKILL.md 配置文件

每个技能目录包含 `SKILL.md` 文件，定义：
- 技能名称和描述（YAML frontmatter）
- 核心能力和定位
- 工作流程
- 工具调用方式
- 输出格式规范
- 使用示例

**示例**：
```yaml
---
name: blog-rewriter
description: 博客文章润色改写专家
---
# 博客文章润色改写专家
...
```

### 目录结构规范

```
skill-name/
├── SKILL.md           # 技能配置（OpenClaw 加载）
├── README.md          # 使用说明（可选）
├── scripts/           # 自动化脚本
├── references/        # 参考文档
├── assets/            # 静态资源
└── output/            # 输出文件
```

---

## 工具集成

### web_search 工具

用于联网搜索实时信息。

**调用方式**：
```javascript
const results = await web_search({
  query: "AI 大模型 24 小时 新闻",
  count: 10
});
```

**应用场景**：
- AI News Xiaohongshu：检索最新资讯
- Social Creator：获取产品最新动态
- Blog Rewriter：事实核实验证

### tavily-search 技能

Tavily 搜索引擎集成。

**使用方式**：
```bash
npx skills tavily-search "AI 大模型 24 小时 新闻"
```

**应用场景**：
- Blog Rewriter：事实核实
- AI News Xiaohongshu：资讯检索

### browser 工具

处理复杂网页内容（动态加载、登录态）。

**应用场景**：
- Blog Rewriter：抓取链接内容

### web_fetch 工具

简单网页内容抓取（提取 markdown）。

**应用场景**：
- Blog Rewriter：抓取静态网页内容

---

## 工作流程集成

### OpenClaw 主流程调用

OpenClaw 作为主流程调用技能脚本：

**示例 1：AI News Xiaohongshu**
```javascript
// OpenClaw 主流程
const searchResults = await web_search({
  query: "AI 大模型 24 小时 新闻",
  count: 10
});

// 转换数据格式
const newsData = searchResults.results.map(r => ({
  title: r.title,
  content: r.snippet,
  url: r.url,
  time: "X 小时前",
  source: new URL(r.url).hostname
}));

// 调用技能脚本
execSync(`node scripts/create-xiaohongshu-content.js --news-json '${JSON.stringify(newsData)}'`);
```

**示例 2：Blog Rewriter**
```javascript
// OpenClaw 处理流程
const content = await web_fetch({ url: articleUrl });
// OpenClaw 执行改写逻辑
// 生成 HTML 封面并输出
```

---

## 技能导入和使用

### 导入步骤

1. 登录 ClawHub 平台
2. 搜索技能名称（如 "blog-rewriter"）
3. 导入技能到工作空间
4. 按技能说明配置参数
5. 开始使用

### 使用方式

**方式 1：直接对话**
```
请帮我改写这篇文章：[链接]
```

**方式 2：指定参数**
```
请帮我改写这篇文章：[链接]
引流话术：[你的话术]
文章类型：技术干货
```

---

## 输出管理

### 输出目录

技能输出文件统一存储在技能目录的 `output/` 下：

```
skill-name/
└── output/
    └── YYYY-MM-DD/      # 日期目录
        ├── file1.md
        └── file2.html
```

### 文件自动打开

脚本执行完成后自动打开输出目录：
```bash
open ~/.openclaw/workspace/skills/skill-name/output/YYYY-MM-DD/
```

---

## 技能开发规范

### YAML Frontmatter

必须包含 `name` 和 `description`：
```yaml
---
name: skill-name
description: 技能简短描述（用于 ClawHub 搜索）
---
```

### 工具调用说明

SKILL.md 中必须明确说明：
- 使用哪些工具
- 调用时机和方式
- 参数格式

### 输出格式规范

明确定义输出文件：
- 文件名称和格式
- 内容结构
- 保存路径

---

## 相关页面

- [技能开发最佳实践](skill-development.md)
- [Blog Rewriter 技能](../skills/blog-rewriter.md)
- [Social Creator 技能](../skills/social-creator.md)
- [AI News Xiaohongshu 技能](../skills/ai-news-xiaohongshu.md)
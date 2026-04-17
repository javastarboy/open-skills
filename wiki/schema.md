---
name: open-skills-wiki
description: Open Skills 项目知识库 wiki 配置和规范
type: project
---

# Open Skills Wiki Schema

本文档定义了 open-skills 项目的 wiki 结构、规范和工作流程。

## 目录结构

```
open-skills/
├── wiki/                    # Wiki 主目录（LLM 维护）
│   ├── index.md            # 内容索引目录
│   ├── log.md              # 操作日志（按时间）
│   ├── overview.md         # 项目概览
│   ├── skills/             # 各技能详情页
│   │   ├── blog-rewriter.md
│   │   ├── social-creator.md
│   │   └── ai-news-xiaohongshu.md
│   ├── concepts/           # 核心概念解释
│   │   ├── clawhub-integration.md
│   │   ├── skill-development.md
│   │   └── content-creation.md
│   ├── guides/             # 使用指南
│   │   ├── getting-started.md
│   │   ├── skill-usage.md
│   │   └── contribution.md
│   └── technical/          # 技术文档
│   │   ├── html-templates.md
│       ├── cover-generation.md
│       └── workflow-automation.md
├── raw/                    # 原始文档源（不可修改）
│   └── sources/            # 源文件存储
└── llm-wiki/               # Wiki 技能说明（固定）
    └── SKILL.md
```

## 页面规范

### 通用格式

每个 wiki 页面应包含：

1. **YAML frontmatter**（可选）：
```yaml
---
tags: [skill, blog-rewriter]
created: 2026-04-17
updated: 2026-04-17
sources: [source1.md, source2.md]
---
```

2. **标题和摘要**：页面顶部一句话概述

3. **正文内容**：使用 Obsidian 风格的内部链接
   - `[blog-rewriter](wiki/skills/blog-rewriter.md)` - 链接到其他 wiki 页面
   - `[[concepts/clawhub-integration]]` - Obsidian 双链语法（可选）

4. **相关链接**：页面底部列出相关页面

### 分类页面说明

**skills/*.md** - 每个技能的详细说明：
- 技能定位和目标
- 功能特性列表
- 使用流程
- 配置参数
- 输出示例
- 技术实现要点
- 限制和注意事项

**concepts/*.md** - 核心概念解释：
- ClawHub 平台集成方式
- Skill 开发最佳实践
- 内容创作方法论

**guides/*.md** - 操作指南：
- 快速开始
- 使用步骤
- 常见问题
- 贡献流程

**technical/*.md** - 技术实现：
- HTML 封面模板设计
- 自动化脚本说明
- 工作流程详解

## 工作流程

### Ingest 流程

当有新文档或更新时：

1. **准备源文件**：将源文档放入 `raw/sources/`
2. **触发 ingest**：告知 Claude "处理新文档 [文件名]"
3. **LLM 执行**：
   - 读取源文件
   - 提取关键信息
   - 创建/更新相关 wiki 页面
   - 更新 `index.md`
   - 在 `log.md` 记录操作

### Query 流程

查询知识时：

1. **直接提问**："blog-rewriter 技能如何使用？"
2. **LLM 执行**：
   - 读取 `index.md` 定位相关页面
   - 深入读取具体页面
   - 综合回答并引用链接

### Lint 流程

定期检查（建议每 10 次 ingest 后）：

1. **触发 lint**："检查 wiki 健康状态"
2. **LLM 检查**：
   - 是否有孤立页面（无入链）
   - 是否有概念缺失页面
   - 是否有矛盾信息
   - 是否需要更新索引

## 特殊约定

### ClawHub 集成标注

所有涉及 ClawHub 的页面应在 frontmatter 标记：
```yaml
tags: [clawhub, integration]
```

并在页面顶部添加徽章：
`![ClawHub](https://img.shields.io/badge/Platform-ClawHub-orange)`

### 技能页面模板

```markdown
# [技能名称]

![Status](https://img.shields.io/badge/status-active-success)

> 一句话概述

## 定位与目标

## 核心功能

## 使用流程

## 配置说明

## 输出示例

## 技术要点

## 相关页面
- [[guides/skill-usage]]
- [[technical/cover-generation]]
```

## 维护策略

- **手动触发**：每次有新文档/PR 更新时手动执行 ingest
- **小规模优化**：使用 `index.md` 作为主要导航，无需搜索工具
- **版本控制**：wiki 通过 git 管理，每次更新提交 commit
- **协作友好**：其他贡献者可通过 PR 更新 wiki

## 为什么这个结构适合本项目

- **项目聚焦**：针对 open-skills 的三个技能，结构清晰
- **文档导向**：技能说明、指南、技术文档分层管理
- **ClawHub 集成**：专门标注平台集成相关信息
- **扩展友好**：新增技能时只需在 skills/ 添加页面
- **维护简单**：小规模 wiki，index.md 足够导航
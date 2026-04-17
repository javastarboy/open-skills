# Open Skills 项目概览

![Status](https://img.shields.io/badge/status-active-success)
![License](https://img.shields.io/badge/license-MIT-blue)
![ClawHub](https://img.shields.io/badge/Platform-ClawHub-orange)

> 基于 ClawHub 生态的开源技能集合,提供实用高效的 AI 技能

---

## 项目定位

**Open Skills** 是一个开源技能仓库,基于 ClawHub 平台构建,专注于开发实用、高效的 AI 技能,覆盖内容创作、社交媒体、资讯整理等多种应用场景。

**核心特点**：
- 🆓 开源免费 - 所有技能代码公开
- 🔄 持续更新 - 定期发布新技能
- 🤝 社区贡献 - 支持提交改进建议
- ⚡ 开箱即用 - 基于 ClawHub 快速部署

---

## 已发布技能

目前包含 3 个核心技能：

### 1. Blog Rewriter（博客文章润色改写专家）

**定位**：资深内容改写专家 + 视觉设计师

**核心能力**：
- 🔍 链接内容抓取
- ✍️ 深度改写降重（目标相似度<30%）
- 🎨 HTML 封面设计（4:3 比例）
- 📊 事实核实（联网搜索验证）
- 🧹 去 AI 化处理

**使用场景**：文章改写降重、社交媒体封面生成、去 AI 化润色、事实核实验证

**详细文档**：[skills/blog-rewriter.md](skills/blog-rewriter.md)

---

### 2. Social Creator（社交媒体爆款内容创作工具）

**定位**：AI 行业洞察 + 爆款文案创作 + 视觉设计

**核心能力**：
- 🧠 AI 行业实时洞察（联网搜索）
- 📱 爆款文案创作（高互动率）
- 🎨 3:4 视觉封面设计（小红书友好）
- 💬 互动引导优化

**使用场景**：小红书/抖音/视频号内容创作、AI 科技主题文案、产品对比评测

**详细文档**：[skills/social-creator.md](skills/social-creator.md)

---

### 3. AI News Xiaohongshu（AI 资讯小红书创作）

**定位**：AI 行业资讯专家 + 小红书内容创作 + 移动端视觉设计

**核心能力**：
- 🔍 检索 24 小时内最新 AI 资讯
- 📝 梳理汇总生成摘要
- ✍️ 创作小红书文案
- 🎨 设计 3:4 比例 HTML 封面

**重点关注**：大模型发布、OpenClaw、Skill 工具、Agent 智能体、VibeCoding、企业突破

**使用场景**：每日 AI 资讯汇总、小红书图文笔记创作、大模型发布/融资/技术突破资讯整理

**详细文档**：[skills/ai-news-xiaohongshu.md](skills/ai-news-xiaohongshu.md)

---

## 技术架构

### 平台集成

所有技能基于 **ClawHub** 平台开发：
- 使用 ClawHub 技能规范（SKILL.md 配置）
- 集成 ClawHub 工具（web_search、tavily-search 等）
- 支持 OpenClaw 工作流程调用

详细集成说明：[concepts/clawhub-integration.md](concepts/clawhub-integration.md)

### 开发规范

技能开发遵循统一规范：
- SKILL.md 配置文件格式
- references/ 参考文档目录
- scripts/ 自动化脚本
- output/ 输出文件管理

开发指南：[concepts/skill-development.md](concepts/skill-development.md)

---

## 使用方式

### 快速开始

1. 注册并登录 [ClawHub 平台](https://clawhub.ai)
2. 在 ClawHub 搜索技能名称（如 "blog-rewriter"）
3. 导入技能并按说明配置参数
4. 开始使用 AI 技能提升效率

详细指南：[guides/getting-started.md](guides/getting-started.md)

### 技能使用

各技能的使用方法、参数配置、输出示例详见：
- [guides/skill-usage.md](guides/skill-usage.md)

---

## 贡献方式

欢迎社区贡献：

- 🐛 提交 Issue - 反馈问题或建议
- 🔧 提交 PR - 修复问题或新增技能
- 📢 分享传播 - 推荐给更多朋友
- ⭐ 点亮 Star - 支持项目持续更新

贡献流程：[guides/contribution.md](guides/contribution.md)

---

## 项目信息

**作者**：AGI舰长

**联系方式**：
- 微信：LHYYH0001
- 博客：https://www.yuque.com/lhyyh
- GitHub：https://github.com/javastarboy/open-skills

**许可证**：MIT License

---

## 相关页面

- [技能列表](skills/)
- [核心概念](concepts/)
- [使用指南](guides/)
- [技术文档](technical/)
- [Wiki 索引](index.md)
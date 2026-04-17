# AI News Xiaohongshu - AI 资讯小红书创作

![Status](https://img.shields.io/badge/status-active-success)
![ClawHub](https://img.shields.io/badge/Platform-ClawHub-orange)

> AI 行业资讯专家 + 小红书内容创作 + 移动端视觉设计，检索最新资讯生成小红书图文笔记

---

## 技能定位

**核心价值**：快速检索最新 AI 资讯，提炼核心信息，生成适合小红书平台的图文笔记内容。

**核心能力**：
- 🔍 检索 24 小时内最新 AI 资讯
- 📝 梳理汇总生成摘要
- ✍️ 创作小红书文案
- 🎨 设计 3:4 比例 HTML 封面（1-3 屏可滑动）
- 📁 自动输出到 `output/日期` 目录

**适用场景**：
- 每日 AI 资讯汇总
- 小红书图文笔记创作
- 大模型发布/融资/技术突破等资讯整理

---

## 核心任务

### 工作流程

```
0. 获取当前时间
   ↓
1. 检索 24 小时内最新 AI 资讯（tavily-search）
   ↓
2. 梳理汇总生成摘要
   ↓
3. 创作小红书文案
   ↓
4. 设计 3:4 比例 HTML 页面（1-3 屏可滑动）
   ↓
5. 输出到 output/日期-序号 目录并打开
```

---

## 重点关注领域

| 类别 | 关键词 |
|------|--------|
| 大模型发布 | 新版本、升级、参数、性能 |
| OpenClaw 相关 | 开源协议、模型开源、WorkBuddy |
| Skill 相关 | 技能、工具、插件 |
| Agent 智能体 | 自主 Agent、多 Agent 协作 |
| VibeCoding | Claude Code、Trae、Cursor、OpenCode、CodeBuddy |
| 企业突破 | 技术突破、融资、合作 |

**重点关注公司**：
阿里千问、MiniMax、OpenAI、Anthropic、Google Gemini、智谱 GLM、腾讯、字节、百度、科大讯飞、Moonshot、DeepSeek 等

---

## 资讯检索策略

### 搜索查询示例

```
- "AI 大模型 24 小时 新闻"
- "OpenAI new release yesterday"
- "阿里千问 最新 24 小时"
- "MiniMax 融资 2026"
- "Anthropic Claude 更新"
- "Google Gemini 新版本"
```

### 时间过滤规则

- 只保留 24 小时内发布的内容
- 检查发布时间戳/相对时间（"X 小时前"、"yesterday"等）
- 优先选择权威来源

---

## 小红书文案创作

### 文案结构

```markdown
【标题】（20 字内，含 emoji，制造悬念/利益点）

【正文】
🔥 开头：3 句话抓住注意力（震惊/反差/利益）

📌 核心资讯（3-5 条，每条含 emoji）
• 资讯 1 + 简短解读
• 资讯 2 + 简短解读
• 资讯 3 + 简短解读

💡 我的观点/解读（1-2 句，增加个人色彩）

👇 互动引导
【用户固定引流话术】

【标签】
#AI #大模型 #人工智能 #科技资讯 #AIGC
```

### 文案风格要求

| 要素 | 要求 |
|------|------|
| 语气 | 活泼、有网感、像朋友分享 |
| emoji | 每段 2-3 个，增强视觉 |
| 段落 | 短段落，每段 1-3 行 |
| 关键词 | 前置，便于搜索 |
| 互动 | 结尾引导评论/收藏/关注 |

### 去 AI 化检查

- [ ] 避免"首先/其次/最后"
- [ ] 避免"综上所述/总之"
- [ ] 避免过于工整的排比
- [ ] 加入个人化表达
- [ ] 口语化、有情绪

---

## HTML 封面设计

### 设计规范

- **比例**：3:4（移动端友好）
- **尺寸**：1080x1440 px（或等比例缩放）
- **页数**：1-3 屏（可上下滑动查看）
- **风格**：科技感、简洁、重点突出

### 设计要点

| 元素 | 建议 |
|------|------|
| 背景 | 渐变色（紫/蓝/橙科技感） |
| 主标题 | 72px+，加粗，高对比 |
| 副标题 | 36-48px，补充说明 |
| 数据 | 用色块/边框突出 |
| 留白 | 避免信息过载 |

---

## 输出文件

运行后会在 `output/日期-序号/` 目录生成：

| 文件 | 说明 |
|------|------|
| `xiaohongshu-copy.md` | 小红书文案（可直接复制发布） |
| `cover.html` | 3:4 比例 HTML 封面（浏览器打开截图） |
| `news-summary.md` | 资讯汇总表格 |
| `sources.md` | 原始来源链接 |

---

## 真实数据 vs 演示数据

### 重要说明

Node.js 脚本无法直接调用 OpenClaw 的 `web_search` 工具。

**正确用法**：
1. **OpenClaw 主流程**先使用 `web_search` 工具搜索真实资讯
2. 将搜索结果转换为 JSON 格式传入脚本
3. 脚本接收数据后生成文案和 HTML

### 调用示例

```javascript
// OpenClaw 主流程搜索后，调用脚本生成内容
node scripts/create-xiaohongshu-content.js --news-json '[{"title":"...", "url":"...", ...}]'
```

### 演示模式（无传入数据时自动使用）

```bash
node scripts/create-xiaohongshu-content.js
# 或
node scripts/create-xiaohongshu-content.js --use-demo
```

---

## 用户自定义配置

编辑 `references/user-config.md`：

### 引流话术模板

```
📌 关注我，每日更新 AI 前沿资讯
👉 评论区留言"资料"获取 AI 工具包
```

### 资讯偏好

- 侧重国内/国外资讯
- 侧重技术/商业资讯
- 核心资讯数量（默认 3-5 条）
- HTML 屏数（默认 2 屏）

---

## 异常处理

| 情况 | 处理方式 |
|------|---------|
| 24 小时内无重磅资讯 | 扩展至 48 小时，标注时间范围 |
| 某些链接无法访问 | 跳过，用其他来源替代 |
| 资讯数量不足 | 降低筛选标准，保证输出 |
| HTML 预览失败 | 提供代码让用户本地打开 |
| web_search 不可用 | 使用演示数据降级，标注"演示模式" |

---

## 质量检查清单

发布前自检：
- [ ] 所有资讯均在 24 小时内（或已标注）
- [ ] 核心事实准确，来源可靠
- [ ] 文案有网感，非 AI 风格
- [ ] emoji 使用适度（每段 2-3 个）
- [ ] HTML 比例 3:4，可滑动
- [ ] 引流话术已替换为用户指定内容
- [ ] 标签包含热门关键词

---

## 相关页面

- [项目概览](overview.md)
- [ClawHub 集成](concepts/clawhub-integration.md)
- [技能使用指南](guides/skill-usage.md)
- [封面生成流程](technical/cover-generation.md)

---

**来源文档**：`raw/sources/ai-news-xiaohongshu-SKILL.md`
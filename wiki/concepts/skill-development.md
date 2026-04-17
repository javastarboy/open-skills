# Skill 开发最佳实践

> Open Skills 技能开发规范、目录结构、配置文件、工具集成指南

---

## 技能开发流程

### 1. 需求分析

确定技能定位：
- 目标用户群体
- 解决的核心问题
- 使用场景
- 输出期望

### 2. 技能设计

设计技能架构：
- 工作流程步骤
- 工具调用方式
- 输出文件格式
- 用户配置参数

### 3. 文件创建

创建技能目录结构：
```
skill-name/
├── SKILL.md           # 必需
├── README.md          # 推荐
├── scripts/           # 按需
│   └── main.js
├── references/        # 按需
│   ├── config.md
│   └── guide.md
├── assets/            # 按需
│   └── template.html
└── output/            # 自动生成
    └── YYYY-MM-DD/
```

---

## SKILL.md 配置规范

### YAML Frontmatter

必需字段：
```yaml
---
name: skill-name                      # 技能唯一标识
description: 技能简短描述（<50字）     # ClawHub 搜索显示
---
```

### 正文结构

推荐结构：
```markdown
# 技能标题

一句话定位说明

## 核心能力
（列出主要能力）

## 快速开始
（使用步骤）

## 工作流程
（详细流程说明）

## 输出格式
（输出文件示例）

## 用户自定义配置
（可配置参数）

## 异常处理
（错误处理方式）

## 质量检查清单
（发布前自检）
```

---

## 工具集成方式

### ClawHub 工具调用

在 SKILL.md 中明确说明工具调用：

**示例**：
```markdown
## 工具调用规范

| 场景 | 工具 | 说明 |
|------|------|------|
| 简单链接抓取 | `web_fetch` | 提取 markdown |
| 复杂页面处理 | `browser` | 执行 JS |
| 事实核实搜索 | `tavily-search` | 验证数据 |
```

### OpenClaw 主流程集成

Node.js 脚本无法直接调用 OpenClaw 工具，需要：
1. OpenClaw 主流程先使用工具
2. 将结果传入脚本

**示例**：
```javascript
// OpenClaw 主流程
const results = await web_search({ query: "..." });

// 调用脚本
execSync(`node scripts/main.js --data '${JSON.stringify(results)}'`);
```

---

## 输出文件规范

### 输出目录命名

推荐使用日期或日期-序号：
```
output/
├── 2026-03-25/
├── 2026-03-25-01/
└── task-name-0324/
```

### 文件命名规范

- 小红书文案：`xiaohongshu-copy.md`
- HTML 封面：`cover.html` / `cover-1.html`
- 资讯汇总：`news-summary.md`
- 来源链接：`sources.md`

### 自动打开输出目录

脚本执行完成后自动打开：
```javascript
const outputDir = path.join(__dirname, 'output', dateStr);
execSync(`open "${outputDir}"`);
```

---

## 用户配置管理

### 配置文件位置

用户可配置参数放在 `references/user-config.md`：

**示例**：
```markdown
# 引流话术
📌 关注我，每日更新 AI 前沿资讯
👉 评论区留言"资料"获取 AI 工具包

# 核心资讯数量
5

# HTML 屏数
2
```

### 脚本读取配置

```javascript
const configPath = path.join(__dirname, 'references', 'user-config.md');
const configContent = fs.readFileSync(configPath, 'utf-8');
// 解析配置内容
```

---

## 质量检查清单

每个技能应包含发布前自检清单：

**示例**：
```markdown
## 质量检查清单

发布前自检：
- [ ] 核心事实是否准确
- [ ] 是否符合平台规范
- [ ] 文件是否已输出
- [ ] 输出文件命名是否正确
- [ ] HTML 是否符合比例要求
- [ ] 用户配置是否可替换
```

---

## 开发注意事项

### 1. 事实准确性

- 使用真实存在的产品/模型名称
- 版本信息需准确
- 不编造不存在的功能
- 无法确认时标注"待核实"

### 2. 去 AI 化处理

避免 AI 痕迹：
- "首先/其次/最后"
- "综上所述/总之"
- 过于工整的排比
- 缺乏情绪表达

### 3. 用户友好性

- 提供快速开始指南
- 输出文件可直接使用
- 自动打开输出目录
- 提供截图方式说明

### 4. 异常处理

处理常见异常：
- 链接无法访问
- 工具不可用
- 数据格式错误
- 输出目录不存在

---

## 技能示例参考

现有技能提供最佳实践参考：

- **Blog Rewriter**：工具调用规范、去 AI 化处理
- **Social Creator**：视觉设计规范、文案创作策略
- **AI News Xiaohongshu**：数据集成方式、时间过滤

---

## 相关页面

- [ClawHub 平台集成](clawhub-integration.md)
- [项目概览](../overview.md)
- [技能使用指南](../guides/skill-usage.md)
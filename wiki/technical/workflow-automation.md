# 工作流程自动化

> Open Skills 技能中的自动化脚本、工作流程集成、批量处理方法

---

## 自动化方式

### 方式 1：OpenClaw 主流程

OpenClaw 作为主流程调用技能：

**流程**：
```
用户请求
  ↓
OpenClaw 接收
  ↓
使用工具（web_search、tavily-search 等）
  ↓
调用技能脚本（可选）
  ↓
生成输出文件
  ↓
返回结果
```

**应用场景**：
- blog-rewriter：OpenClaw 处理改写流程
- ai-news-xiaohongshu：OpenClaw 搜索资讯→调用脚本生成内容

---

### 方式 2：独立脚本运行

直接运行技能脚本：

**流程**：
```
用户执行脚本
  ↓
脚本处理数据（演示数据或传入数据）
  ↓
生成输出文件
  ↓
打开预览和输出目录
```

**应用场景**：
- ai-news-xiaohongshu：演示模式测试
- social-creator：批量生成封面（可选）

---

## OpenClaw 主流程集成

### Blog Rewriter 流程

**OpenClaw 自动处理**：
```
1. 接收用户输入（链接或文本）
2. web_fetch/browser 抓取内容
3. AI 分析原文
4. tavily-search 事实核实
5. AI 深度改写
6. ui-ux-pro-max + write 生成 HTML 封面
7. 输出完整结果
```

用户无需运行脚本，OpenClaw 自动完成全流程。

---

### AI News Xiaohongshu 流程

**OpenClaw 主流程 + 脚本调用**：

```javascript
// 1. OpenClaw 搜索资讯
const searchResults = await web_search({
  query: "AI 大模型 24 小时 新闻",
  count: 10
});

// 2. 转换数据格式
const newsData = searchResults.results.map(r => ({
  title: r.title,
  content: r.snippet,
  url: r.url,
  time: "X 小时前",
  source: new URL(r.url).hostname
}));

// 3. 调用技能脚本
execSync(`node scripts/create-xiaohongshu-content.js --news-json '${JSON.stringify(newsData)}'`);
```

**关键点**：Node.js 脚本无法直接调用 OpenClaw 工具，需要主流程先处理数据再传入。

---

## 独立脚本运行

### AI News Xiaohongshu 脚本

**演示模式**：
```bash
cd ~/.openclaw/workspace/skills/ai-news-xiaohongshu
node scripts/create-xiaohongshu-content.js
```

使用内置演示数据生成示例内容。

**真实数据模式**：
```bash
node scripts/create-xiaohongshu-content.js --news-json '[{"title":"...", "url":"...", ...}]'
```

传入真实资讯数据生成内容。

---

### Social Creator 脚本

**Python 封面生成脚本**：
```bash
python scripts/generate-cover-html.py \
  --text "文案内容" \
  --highlight "关键字" \
  --style "tech" \
  --output cover.html
```

批量生成多个封面：
```bash
for i in 1 2 3; do
  python scripts/generate-cover-html.py \
    --text "文案 $i" \
    --output "cover-$i.html"
done
```

---

## 批量处理

### 批量资讯生成

创建多个日期的资讯内容：

```bash
for date in 2026-03-24 2026-03-25 2026-03-26; do
  node scripts/create-xiaohongshu-content.js --date "$date"
done
```

---

### 批量封面生成

为多条文案批量生成封面：

```javascript
const copywritings = [
  "文案 1",
  "文案 2",
  "文案 3"
];

copywritings.forEach((text, index) => {
  execSync(`python scripts/generate-cover-html.py --text "${text}" --output cover-${index + 1}.html`);
});
```

---

## 定时自动化

### Cron 定时任务

设置定时任务自动生成内容：

```bash
# 每天早上 9 点生成 AI 资讯
0 9 * * * cd ~/.openclaw/workspace/skills/ai-news-xiaohongshu && node scripts/create-xiaohongshu-content.js >> /tmp/ai-news.log 2>&1
```

---

## 输出自动化

### 自动打开输出目录

脚本执行完成后自动打开：

**macOS**：
```javascript
const outputDir = path.join(__dirname, 'output', dateStr);
execSync(`open "${outputDir}"`);
```

**Windows**：
```javascript
execSync(`start "" "${outputDir}"`);
```

---

### 自动打开 HTML 预览

```javascript
const htmlPath = path.join(outputDir, 'cover.html');
execSync(`open "${htmlPath}"`);
```

---

## 异常处理

### 工具不可用降级

**web_search 不可用**：
- 使用演示数据降级
- 标注"演示模式"
- 提示用户由 OpenClaw 主流程调用

**示例**：
```javascript
if (!webSearchAvailable) {
  console.log("⚠️ web_search 不可用，使用演示数据");
  newsData = getDemoData();
}
```

---

### 输出目录不存在

自动创建输出目录：
```javascript
const outputDir = path.join(__dirname, 'output', dateStr);
if (!fs.existsSync(outputDir)) {
  fs.mkdirSync(outputDir, { recursive: true });
}
```

---

## 配置管理

### 用户配置文件

读取用户配置：
```javascript
const configPath = path.join(__dirname, 'references', 'user-config.md');
const configContent = fs.readFileSync(configPath, 'utf-8');

// 解析配置
const引流话术 = extractSection(configContent, '引流话术');
const资讯数量 = extractSection(configContent, '核心资讯数量');
```

---

## 相关页面

- [ClawHub 平台集成](../concepts/clawhub-integration.md)
- [封面生成流程](cover-generation.md)
- [技能使用指南](../guides/skill-usage.md)
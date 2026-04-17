# 封面生成流程

> Open Skills 技能中 HTML 封面的生成方法、脚本调用、自动化流程

---

## 封面生成方式

### 方式 1：AI 直接生成

OpenClaw 使用 AI 能力直接生成 HTML：

**流程**：
```
1. OpenClaw 执行任务
2. AI 生成 HTML 代码
3. 使用 write 工具保存为 HTML 文件
4. 在浏览器中打开预览
```

**应用技能**：
- blog-rewriter：生成 4:3 封面
- social-creator：生成多条 3:4 封面

---

### 方式 2：脚本生成

使用 Python/Node.js 脚本生成 HTML：

**流程**：
```
1. 用户提供文案内容
2. 脚本接收参数
3. 填充模板生成 HTML
4. 输出到文件
5. 在浏览器中打开
```

**应用技能**：
- ai-news-xiaohongshu：Node.js 脚本生成 3:4 封面
- social-creator：Python 脚本生成封面（可选）

---

## Social Creator 封面生成

### AI 直接生成

OpenClaw 调用 `ui-ux-pro-max` 技能：

```
请生成 3 条爆款文案

输出：
- 文案内容
- HTML 封面文件（cover-1.html, cover-2.html, cover-3.html）
```

---

### Python 脚本生成

使用 `scripts/generate-cover-html.py`：

```bash
python scripts/generate-cover-html.py \
  --text "你的文案内容" \
  --highlight "关键字" \
  --style "tech" \
  --output cover.html
```

**参数说明**：
- `--text`：文案内容（必填）
- `--highlight`：高亮关键字（可选）
- `--style`：视觉风格（tech/dark/minimal，默认 tech）
- `--output`：输出文件名（默认 cover.html）

---

## AI News Xiaohongshu 封面生成

### Node.js 脚本

使用 `scripts/create-xiaohongshu-content.js`：

```bash
node scripts/create-xiaohongshu-content.js --news-json '[...]'
```

**脚本功能**：
- 接收资讯数据（JSON）
- 生成小红书文案
- 生成 3:4 HTML 封面（1-3 屏可滑动）
- 输出到 `output/日期-序号/` 目录
- 在浏览器中打开 HTML
- 打开输出目录访达

---

### 演示模式

无传入数据时使用演示数据：

```bash
node scripts/create-xiaohongshu-content.js
```

---

## 封面设计规范

### 比例要求

| 技能 | 比例 | 尺寸 | 页数 |
|------|------|------|------|
| blog-rewriter | 4:3 | 1200x900 px | 1 页 |
| social-creator | 3:4 | viewport 单位 | 每条文案 1 页 |
| ai-news-xiaohongshu | 3:4 | viewport 单位 | 1-3 屏可滑动 |

---

### 设计要点

| 技能 | 设计重点 |
|------|---------|
| blog-rewriter | 文章主标题 + 副标题 + 视觉冲击力 |
| social-creator | 文案居中，极简设计，关键词高亮 |
| ai-news-xiaohongshu | 标题 + 日期 + 资讯列表，多屏滑动 |

---

## 输出文件管理

### 输出目录

```
skill-name/output/
├── 2026-03-25/
│   ├── cover-1.html
│   ├── cover-2.html
│   └── cover-3.html
└── 2026-03-25-01/
    ├── cover.html
    ├── xiaohongshu-copy.md
    └── ...
```

---

### 自动打开

脚本执行完成后自动打开输出目录：

**macOS**：
```javascript
execSync(`open "${outputDir}"`);
```

**Windows**：
```javascript
execSync(`start "" "${outputDir}"`);
```

---

## 封面预览和截图

### 预览方式

浏览器打开 HTML 文件：
```javascript
execSync(`open "${htmlPath}"`);
```

---

### 截图方式

**电脑浏览器 + F12 手机模式**（推荐）：
1. 打开 HTML 文件
2. F12 → 切换设备工具栏（Ctrl+Shift+M）
3. 选择手机型号
4. 截图

**手动调整窗口**：
- 调整浏览器窗口为指定比例
- 截图

**手机浏览器**：
- HTML 发送到手机
- 手机浏览器打开
- 截图

---

## HTML 模板参考

详细模板结构和样式见：
- [HTML 封面模板设计](html-templates.md)

---

## 异常处理

| 情况 | 处理方式 |
|------|---------|
| HTML 生成失败 | 提供文字版设计建议 |
| 浏览器打开失败 | 提示用户手动打开 |
| 截图比例不对 | 提示 F12 手机模式 |

---

## 相关页面

- [HTML 封面模板设计](html-templates.md)
- [Blog Rewriter 技能](../skills/blog-rewriter.md)
- [Social Creator 技能](../skills/social-creator.md)
- [AI News Xiaohongshu 技能](../skills/ai-news-xiaohongshu.md)
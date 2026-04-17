# HTML 封面模板设计

> Open Skills 技能中的 HTML 封面设计规范、模板结构、样式指南

---

## 封面设计规范

### 比例要求

不同平台的封面比例：

| 平台 | 比例 | 尺寸 | 技能 |
|------|------|------|------|
| 微信公众号 | 4:3 | 1200x900 px | blog-rewriter |
| 小红书 | 3:4 | 1080x1440 px | social-creator, ai-news-xiaohongshu |
| 抖音 | 9:16 | 1080x1920 px | - |

---

## 设计原则

### 核心理念

**少即是多**：
- 元素极简，突出文案内容
- 文字成为视觉焦点
- 留白充足，避免拥挤

### 关键要素

| 元素 | 要求 |
|------|------|
| 背景 | 纯色或简单渐变 |
| 文案 | 居中，字号醒目（36-48px） |
| 关键词 | 高亮突出（色块/对比色） |
| 留白 | 四周≥15% |
| 装饰 | 可选 1-3 个 emoji |

---

## HTML 结构模板

### 4:3 比例模板（微信公众号）

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>封面</title>
  <style>
    * { margin: 0; padding: 0; box-sizing: border-box; }

    body {
      width: 1200px;
      height: 900px;
      display: flex;
      align-items: center;
      justify-content: center;
      background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
      font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
    }

    .container {
      text-align: center;
      padding: 40px;
    }

    h1 {
      font-size: 64px;
      font-weight: bold;
      color: #fff;
      margin-bottom: 20px;
      line-height: 1.4;
    }

    h2 {
      font-size: 36px;
      color: rgba(255, 255, 255, 0.9);
      margin-bottom: 30px;
    }

    .highlight {
      background: rgba(255, 255, 255, 0.2);
      padding: 10px 20px;
      border-radius: 12px;
      color: #fff;
      font-size: 28px;
      display: inline-block;
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>🔥 主标题</h1>
    <h2>副标题说明</h2>
    <div class="highlight">关键数据</div>
  </div>
</body>
</html>
```

---

### 3:4 比例模板（小红书）

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>小红书封面</title>
  <style>
    * { margin: 0; padding: 0; box-sizing: border-box; }

    body {
      width: 100vw;
      height: 100vh;
      aspect-ratio: 3/4;
      display: flex;
      align-items: center;
      justify-content: center;
      background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
      font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
    }

    .container {
      text-align: center;
      padding: 15%;
    }

    .content {
      font-size: 42px;
      font-weight: bold;
      color: #fff;
      line-height: 1.8;
      margin-bottom: 20px;
    }

    .highlight {
      background: rgba(255, 255, 255, 0.3);
      padding: 8px 16px;
      border-radius: 12px;
      display: inline-block;
    }

    .cta {
      font-size: 28px;
      color: rgba(255, 255, 255, 0.9);
      background: rgba(0, 0, 0, 0.2);
      padding: 10px 20px;
      border-radius: 20px;
      display: inline-block;
      margin-top: 20px;
    }
  </style>
</head>
<body>
  <div class="container">
    <div class="content">
      <span class="highlight">Claude 3.5</span> 和 <span class="highlight">GPT-4o</span> 写代码
      真实体验差距有多大
    </div>
    <div class="cta">求用过的大佬说说！</div>
  </div>
</body>
</html>
```

---

## 样式指南

### 背景设计

**渐变色方案**：
```css
/* 科技蓝紫 */
background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);

/* 深色极简 */
background: linear-gradient(135deg, #2c3e50 0%, #34495e 100%);

/* 小红书红 */
background: linear-gradient(135deg, #ff6b6b 0%, #ee5a6f 100%);

/* 橙色活力 */
background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%);
```

**纯色方案**：
```css
background: #1a1a1a; /* 深色 */
background: #ffffff; /* 浅色 */
```

---

### 文字样式

**主标题**：
```css
h1 {
  font-size: 64-72px;
  font-weight: bold;
  color: #fff;
  line-height: 1.4;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.2);
}
```

**副标题**：
```css
h2 {
  font-size: 36-48px;
  color: rgba(255, 255, 255, 0.9);
  line-height: 1.6;
}
```

**关键词高亮**：
```css
.highlight {
  background: rgba(255, 255, 255, 0.3);
  padding: 8px 16px;
  border-radius: 12px;
  display: inline-block;
}
```

---

### 响应式适配

使用 viewport 单位和 aspect-ratio：

```css
body {
  width: 100vw;
  height: 100vh;
  aspect-ratio: 3/4;
}
```

---

## 多屏滑动设计

AI News Xiaohongshu 需要 1-3 屏可滑动的 HTML：

```html
<div class="pages">
  <!-- 第 1 屏：标题 -->
  <div class="page" style="background: linear-gradient(...);">
    <h1>🔥 AI 日报</h1>
    <h2>2026.03.25</h2>
  </div>

  <!-- 分屏线 -->
  <hr class="divider">

  <!-- 第 2 屏：资讯列表 -->
  <div class="page" style="background: #fff;">
    <ul>
      <li>资讯 1</li>
      <li>资讯 2</li>
    </ul>
  </div>
</div>

<style>
.pages {
  width: 100vw;
  height: auto;
}

.page {
  width: 100vw;
  height: 100vh;
  aspect-ratio: 3/4;
}

.divider {
  border: none;
  height: 10px;
  background: #f0f0f0;
}
</style>
```

---

## 禁止元素

避免以下设计：
- ❌ "干货分享""学习笔记"等标签
- ❌ "点赞""收藏""关注"等引导
- ❌ 多条文案堆砌（social-creator 要求每条文案独立页面）
- ❌ 复杂边框/花纹/图案
- ❌ 底部互动引导区（除非必要）

---

## 截图方式

### 电脑浏览器 + F12 手机模式

1. 浏览器打开 HTML 文件
2. F12 → 切换设备工具栏
3. 选择手机型号（如 iPhone 12 Pro）
4. 截图（确保无背景缝隙）

---

## 相关页面

- [封面生成流程](cover-generation.md)
- [Social Creator 技能](../skills/social-creator.md)
- [AI News Xiaohongshu 技能](../skills/ai-news-xiaohongshu.md)
- [内容创作方法论](../concepts/content-creation.md)
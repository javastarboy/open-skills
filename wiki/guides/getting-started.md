# 快速开始指南

> Open Skills 技能快速上手指南，从注册到使用的完整流程

---

## 前置条件

### 1. 注册 ClawHub 平台

访问 [ClawHub](https://clawhub.ai) 并注册账号。

### 2. 了解基本使用

熟悉 ClawHub 技能的基本使用方式。

---

## 使用步骤

### 第一步：浏览技能

在本项目查看已发布技能：

| 技能名称 | 功能 | 适用场景 |
|---------|------|---------|
| blog-rewriter | 博客文章润色改写 | 文章降重、封面生成 |
| social-creator | 社交媒体爆款内容 | 小红书/抖音文案创作 |
| ai-news-xiaohongshu | AI 资讯小红书创作 | 每日资讯汇总整理 |

详细技能说明：[技能列表](../skills/)

---

### 第二步：导入技能

在 ClawHub 平台导入技能：

1. 登录 ClawHub
2. 搜索技能名称（如 "blog-rewriter"）
3. 点击导入到工作空间

---

### 第三步：配置使用

按技能说明进行参数配置：

**Blog Rewriter 配置示例**：
```
请帮我改写这篇文章：[链接]

我的引流话术：
📌 关注【我的公众号】，对话框点击"AI 交流"
👉 添加微信：LHYYH0001

文章类型：技术干货
```

**AI News Xiaohongshu 配置示例**：

编辑 `references/user-config.md`：
```markdown
# 引流话术
📌 关注我，每日更新 AI 前沿资讯
👉 评论区留言"资料"获取 AI 工具包

# 核心资讯数量
5

# HTML 屏数
2
```

---

### 第四步：开始创作

使用技能生成内容：

**方式 1：直接对话**
```
请帮我改写这篇文章：https://example.com/article
```

**方式 2：运行脚本**
```bash
cd ~/.openclaw/workspace/skills/ai-news-xiaohongshu
node scripts/create-xiaohongshu-content.js
```

---

## 输出文件使用

### 输出目录位置

技能输出文件存储在：
```
~/.openclaw/workspace/skills/skill-name/output/YYYY-MM-DD/
```

### 文件类型

常见输出文件：
- `xiaohongshu-copy.md` - 小红书文案（可直接复制发布）
- `cover.html` - HTML 封面（浏览器打开截图）
- `news-summary.md` - 资讯汇总表格
- `sources.md` - 来源链接

---

## HTML 截图方式

### 方式 1：电脑浏览器 + F12 手机模式（推荐）

1. 浏览器打开 HTML 文件
2. 按 F12 打开开发者工具
3. 点击"切换设备工具栏"（Ctrl+Shift+M）
4. 选择手机型号（如 iPhone 12 Pro）
5. 直接截图

### 方式 2：电脑浏览器 + 手动调整窗口

- 调整浏览器窗口为指定比例
- 直接截图

### 方式 3：手机浏览器

- 将 HTML 文件发送到手机
- 手机浏览器打开并截图

---

## 常见问题

### Q: 技能搜索不到？

**A**: 确认技能名称拼写正确：
- blog-rewriter
- social-creator
- ai-news-xiaohongshu

### Q: 输出文件在哪里？

**A**: 脚本执行完成后会自动打开输出目录访达窗口。

### Q: HTML 文件如何使用？

**A**: 浏览器打开 HTML 文件，使用上述截图方式生成图片，然后发布到社交媒体。

### Q: 如何修改配置？

**A**: 编辑技能目录下的 `references/user-config.md` 文件。

---

## 下一步

- [技能使用指南](skill-usage.md) - 详细使用方法
- [贡献指南](contribution.md) - 如何贡献新技能
- [技能列表](../skills/) - 查看所有技能详情

---

## 获取帮助

遇到问题时：
- 📝 查看 [Issues](https://github.com/javastarboy/open-skills/issues)
- 💬 联系微信：LHYYH0001
- 📝 作者博客：https://www.yuque.com/lhyyh
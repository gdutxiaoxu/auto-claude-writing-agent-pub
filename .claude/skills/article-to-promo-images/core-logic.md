# Article to Promo Images - 核心逻辑详解

## 一、内容提取与分析

### 1.1 读取内容

**本地MD文件**：使用 `Read` 工具直接读取

**文章URL**：使用 `mcp__web_reader__webReader` 工具抓取
```javascript
// 参数示例
{
  url: "https://example.com/article",
  return_format: "markdown"
}
```

### 1.2 解析结构

从Markdown中提取：

```javascript
{
  title: "一级标题或第一个#标题",
  subtitle: "二级标题或首段摘要",
  tags: ["标签1", "标签2"],  // 从内容推断
  keyPoints: [],    // 无序列表、加粗要点
  sections: [],     // 二级标题结构
  quotes: [],       // 引用块、金句
  articleType: ""   // tutorial/technical/opinion/news
}
```

### 1.3 文章类型判断

| 特征 | 类型 |
|------|------|
| 包含"教程"、"入门"、"指南" | tutorial |
| 包含代码块、技术术语 | technical |
| 包含"我认为"、"观点" | opinion |
| 有明确时间、新闻要素 | news |

---

## 二、模板选择策略

### 2.1 默认模板组合

根据 `count` 参数自动选择：

| count | 默认组合 |
|-------|----------|
| 1 | cover |
| 2 | cover + key-points |
| 3 | cover + key-points + quote |
| 4 | cover + key-points + comparison + quote |
| 5+ | cover + key-points + comparison + roadmap + quote |

### 2.2 按文章类型定制

```javascript
const typeTemplates = {
  tutorial: ['cover', 'roadmap', 'key-points', 'quote'],
  technical: ['cover', 'key-points', 'comparison', 'quote'],
  opinion: ['cover', 'quote', 'key-points'],
  news: ['cover', 'key-points', 'quote']
};
```

---

## 三、内容映射规则

### 3.1 封面图 (cover)

| 字段 | 来源 |
|------|------|
| 主标题 | `title` |
| 副标题 | `subtitle` 或 前50字摘要 |
| 标签 | `tags` 或 自动提取关键词 |
| 图标 | 根据文章类型选择 |

### 3.2 要点图 (key-points)

```javascript
// 提取规则
1. 找到所有无序列表 (- *)
2. 找到所有加粗文本 (**文本**)
3. 优先选择列表，最多5个
4. 每个要点不超过30字
```

### 3.3 对比图 (comparison)

```javascript
// 自动检测对比结构
- "问题" vs "方案"
- "Before" vs "After"
- "传统" vs "创新"
- "痛点" vs "价值"
```

### 3.4 路线图 (roadmap)

```javascript
// 从二级标题提取
## 第一章 -> 入门阶段
## 第二章 -> 进阶阶段
## 第三章 -> 高级阶段
```

### 3.5 金句图 (quote)

```javascript
// 提取优先级
1. 引用块 (> 文本)
2. 包含引号的句子
3. 段落首句（如简短有力）
```

---

## 四、HTML生成流程

### 4.1 模板结构

```html
<!DOCTYPE html>
<html>
<head>
  <style>{{BASE_STYLES}}</style>
  <style>{{THEME_STYLES}}</style>
</head>
<body>
  <div class="container">
    <!-- 动态生成的图片卡片 -->
  </div>
  <div class="modal">...</div>
  <div class="toast">...</div>
  <script>{{SCRIPTS}}</script>
</body>
</html>
```

### 4.2 样式主题

```javascript
const themes = {
  cyber: {
    background: '#0a0e17',
    primary: '#00fff2',
    secondary: '#ff6b35',
    accent: '#7b2cbf',
    fontTitle: 'Orbitron',
    fontBody: 'Noto Sans SC',
    fontMono: 'JetBrains Mono'
  },
  minimal: {
    background: '#ffffff',
    primary: '#1a1a1a',
    secondary: '#666666',
    accent: '#000000',
    fontTitle: 'Helvetica',
    fontBody: 'Georgia',
    fontMono: 'Consolas'
  },
  warm: {
    background: '#fff8f0',
    primary: '#ff6b35',
    secondary: '#f7931e',
    accent: '#2d3436',
    fontTitle: 'Poppins',
    fontBody: 'Open Sans',
    fontMono: 'Fira Code'
  },
  nature: {
    background: '#f0f9f4',
    primary: '#00b894',
    secondary: '#55a3ff',
    accent: '#2d3436',
    fontTitle: 'Montserrat',
    fontBody: 'Lato',
    fontMono: 'Source Code Pro'
  }
};
```

### 4.3 动态生成示例

```javascript
// 生成封面图
const coverHTML = `
<div class="image-card">
  <div class="img-cover-container" id="img-cover">
    <div class="img-cover-bg"></div>
    <div class="img-cover-content">
      <h1 class="img-cover-title">${data.title}</h1>
      <p class="img-cover-subtitle">${data.subtitle}</p>
      <div class="img-cover-tags">
        ${data.tags.map(tag => `<span class="tag">${tag}</span>`).join('')}
      </div>
    </div>
  </div>
</div>
`;
```

---

## 五、输出规范

### 5.1 文件命名

```
promo-images-{timestamp}.html
或
{article-slug}-promo.html
```

### 5.2 使用说明

生成后在HTML文件顶部添加注释：

```html
<!--
使用说明：
1. 在浏览器中打开此文件
2. 点击"预览"查看大图
3. 点击"下载"保存PNG图片
4. ESC键关闭预览

生成时间：{timestamp}
文章来源：{source}
图片数量：{count}
设计风格：{style}
-->
```

---

## 六、错误处理

| 场景 | 处理方式 |
|------|----------|
| 文件不存在 | 提示用户检查路径 |
| URL无法访问 | 提示使用备用链接或本地文件 |
| 内容过少 | 警告但继续生成（可能只有封面图） |
| 提取失败 | 使用默认内容，告知用户 |

---

## 七、优化建议

### 7.1 性能优化

- 内联所有CSS和JS，单文件运行
- 使用国内CDN镜像
- 字体添加备用方案
- 按需加载html2canvas

### 7.2 兼容性

- 支持现代浏览器
- 降级方案：字体加载失败时使用系统字体
- 移动端响应式适配

---

## 八、扩展方向

未来可添加的功能：

1. **更多模板** - 数据图表、流程图、思维导图
2. **AI增强** - 自动生成配图描述、AI绘图
3. **批量处理** - 一次处理多篇文章
4. **自定义样式** - 用户上传CSS覆盖默认样式
5. **多语言支持** - 英文、日文等其他语言

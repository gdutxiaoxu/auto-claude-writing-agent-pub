# Step 3: 内容解析与结构化

**优先级**: ⭐⭐⭐ | **必做**: 是

---

## 目标

从爬取的原始内容中提取关键信息，输出结构化数据。

---

## 提取字段

### 必需字段

| 字段 | 说明 | 示例 |
|------|------|------|
| `title` | 文章标题 | "Claude Code 2.1 发布" |
| `content` | 正文内容 | 原始 Markdown 格式 |
| `source` | 来源网站 | "机器之心" |

### 可选字段

| 字段 | 说明 | 示例 |
|------|------|------|
| `author` | 作者 | "张三" |
| `published_at` | 发布时间 | "2026-01-24 10:30" |
| `url` | 原始链接 | "https://..." |
| `tags` | 标签 | ["AI", "编程"] |
| `summary` | 摘要 | "本文介绍..." |

---

## 解析策略

### 策略 1: 基于 HTML 结构识别

```python
# 伪代码示例
def parse_article(raw_html):
    article = {
        'title': extract_title(raw_html),
        'author': extract_author(raw_html),
        'content': extract_content(raw_html),
        'published_at': extract_time(raw_html),
    }
    return article
```

### 策略 2: 基于常见模式

使用 LLM 理解内容结构：

```markdown
请从以下内容中提取：
1. 标题（通常在最前面，# 号包裹）
2. 作者（寻找"作者"、"文"等关键词）
3. 发布时间（寻找日期格式）
4. 正文（去除导航、广告、推荐等内容）
```

### 策略 3: 网站特定规则

不同网站的解析规则：

**机器之心**:
- 标题: `<h1 class="article-title">`
- 正文: `<div class="article-content">`

**量子位**:
- 标题: `class="title"`
- 正文: `id="content"`

**36氪**:
- 标题: `class="article-title"`
- 正文: `class="article-content"`

---

## 内容清洗

### 需要移除的内容

```markdown
# 移除广告
- [广告]、[赞助]
- 推荐阅读、相关文章
- 二维码、关注提示

# 移除导航
- 返回顶部
- 分享按钮
- 评论引导

# 移除脚本
- <script> 标签
- 内联 JavaScript
```

### 保留的内容

```markdown
# 保留正文
- 段落文本
- 列表内容
- 引用块
- 代码块

# 保留关键信息
- 时间戳
- 作者署名
- 来源标注
```

---

## 输出格式

### Markdown 格式（默认）

```markdown
# Claude Code 2.1 发布：30+ 新功能详解

**来源**: 机器之心
**作者**: 李四
**时间**: 2026-01-24 10:30
**链接**: https://www.jiqizhixin.com/article/12345

---

## 正文

Claude 今日发布了 Claude Code 2.1 版本...
（完整内容）

---

## 关键要点

1. Skills 热重载功能
2. Tab 智能补全优化
3. 性能提升 30%
```

### JSON 格式（可选）

```json
{
  "title": "Claude Code 2.1 发布：30+ 新功能详解",
  "source": "机器之心",
  "author": "李四",
  "published_at": "2026-01-24T10:30:00+08:00",
  "url": "https://www.jiqizhixin.com/article/12345",
  "content": "Claude 今日发布了...",
  "summary": "本文介绍了 Claude Code 2.1 的主要新功能...",
  "tags": ["AI", "Claude", "编程工具"]
}
```

---

## 质量检查

解析完成后，进行质量检查：

```markdown
✅ 内容质量检查
- 标题完整: 是
- 正文长度: 2000 字
- 去除广告: 完成
- 格式规范: Markdown
```

如质量不合格，返回 Step 2 重新获取或手动修正。

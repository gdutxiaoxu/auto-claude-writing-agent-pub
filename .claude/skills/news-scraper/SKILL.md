---
name: news-scraper
description: 从新闻网站爬取和解析内容。支持中文科技媒体（机器之心、量子位、36氪）和英文媒体（Hacker News、TechCrunch、The Verge）。使用 WebReader MCP 工具直接爬取页面内容，自动提取标题、正文、发布时间等关键信息。
---

# 新闻内容爬取 Skill

> **版本**: v1.0 | **更新时间**: 2026-01-24
> **触发方式**: 手动触发 | **输出**: 结构化的新闻内容

---

## 触发条件

当用户说以下内容时，自动触发此 Skill：

- "爬取这个新闻网站"
- "获取这篇新闻的完整内容"
- "提取 [URL] 的新闻内容"
- "抓取 [网站名] 的文章"
- 或类似的爬取请求

---

## 核心工具：WebReader MCP ⭐⭐⭐

### 工具名称

`mcp__web_reader__webReader`

### 参数说明

| 参数 | 类型 | 必填 | 说明 |
|------|------|------|------|
| `url` | string | ✅ | 目标新闻页面URL |
| `return_format` | string | ❌ | 返回格式：markdown（默认）/ text |
| `retain_images` | boolean | ❌ | 保留图片：true（默认）/ false |
| `no_cache` | boolean | ❌ | 禁用缓存：false（默认）/ true |
| `timeout` | int | ❌ | 超时时间（秒），默认20 |

### 基本用法

```markdown
mcp__web_reader__webReader(
  url="https://www.jiqizhixin.com/article/xxxxx"
  return_format="markdown"
  retain_images="false"
)
```

---

## 支持的新闻网站

### 中文科技媒体

| 网站 | URL | 特点 |
|------|-----|------|
| 机器之心 | jiqizhixin.com | AI深度报道 |
| 量子位 | qbitai.com | AI前沿资讯 |
| 36氪 | 36kr.com | 科技创业 |
| 虎嗅 | huxiu.com | 商业科技 |
| 钛媒体 | tmtpost.com | 深度分析 |

### 英文科技媒体

| 网站 | URL | 特点 |
|------|-----|------|
| Hacker News | news.ycombinator.com | 技术讨论 |
| TechCrunch | techcrunch.com | 创业科技 |
| The Verge | theverge.com | 科技产品 |
| Ars Technica | arstechnica.com | 深度技术 |

---

## 使用流程

### Step 1: 确认 URL

用户提供URL或新闻标题，先确认目标链接。

### Step 2: 爬取内容

使用 WebReader MCP 爬取页面。

### Step 3: 解析结构

提取关键信息：
- 标题
- 作者/来源
- 发布时间
- 正文内容
- 图片（如需要）

### Step 4: 格式化输出

按用户需求输出结构化内容。

---

## 输出格式

### 默认格式（Markdown）

```markdown
# [标题]

**来源**: [网站名]
**作者**: [作者名]
**时间**: [发布时间]
**链接**: [原始URL]

---

## 正文内容

[提取的正文内容]

---

## 关键要点

- 要点1
- 要点2
- 要点3
```

### 简洁格式

```markdown
[标题]
[来源] | [时间]
[正文摘要]
```

### JSON 格式（可选）

```json
{
  "title": "文章标题",
  "source": "来源网站",
  "author": "作者",
  "published_at": "发布时间",
  "url": "原始链接",
  "content": "正文内容",
  "summary": "摘要"
}
```

---

## 示例

### 示例 1: 爬取单篇文章

**用户**: "爬取这篇新闻 https://www.jiqizhixin.com/article/12345"

**Claude执行**:
1. 确认URL有效
2. 调用 WebReader MCP
3. 解析并输出结构化内容

### 示例 2: 批量爬取

**用户**: "爬取今天量子位的前5篇AI新闻"

**Claude执行**:
1. 先用搜索获取文章列表
2. 逐篇爬取内容
3. 汇总输出

---

## 错误处理

### 常见错误及解决

| 错误 | 原因 | 解决方案 |
|------|------|----------|
| 404 Not Found | URL无效 | 检查URL或搜索正确的链接 |
| 403 Forbidden | 反爬虫限制 | 尝试添加请求头或使用备用方案 |
| Timeout | 网站响应慢 | 增加 timeout 参数 |
| 内容解析失败 | 结构变化 | 手动检查页面结构 |

### 备用方案

如 WebReader 不可用：

1. **Bash + curl**
   ```bash
   curl -s "URL" | grep -o "<title>.*</title>"
   ```

2. **建议用户手动复制**
   - 请用户直接复制正文内容
   - 协助格式化整理

---

## 注意事项

- ⚠️ 遵守网站的 robots.txt 规则
- ⚠️ 不要过于频繁请求，避免给目标网站造成压力
- ⚠️ 尊重版权，仅用于个人学习和研究
- ⚠️ 敏感内容需要用户确认是否处理

---

## 与其他 Skill 配合

- **daily-ai-news**: 爬取新闻详情用于写作
- **mp-wechat-flow**: 获取新闻素材用于公众号文章
- **doc-coauthoring**: 整理新闻内容用于文档

---

## 技巧与优化

### 提高成功率

1. **优先使用 HTTPS**
2. **移除不必要的查询参数**
3. **使用桌面版 UA**（部分网站区分移动/桌面）
4. **处理反爬虫**：遇到验证码时提示用户手动操作

### 内容清洗

爬取后自动清理：
- 移除广告内容
- 删除相关推荐
- 清理导航元素
- 过滤脚本代码

---

## 版本历史

**v1.0 (2026-01-24)**
- 初始版本
- 支持 WebReader MCP
- 覆盖主流中英文科技媒体

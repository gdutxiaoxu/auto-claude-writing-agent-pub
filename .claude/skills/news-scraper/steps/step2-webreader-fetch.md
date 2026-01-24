# Step 2: 使用 WebReader MCP 爬取内容

**优先级**: ⭐⭐⭐ | **必做**: 是

---

## 目标

使用 WebReader MCP 工具获取新闻页面的完整内容。

---

## 核心工具调用

### 标准调用

```markdown
mcp__web_reader__webReader(
  url="https://www.jiqizhixin.com/article/xxxxx"
  return_format="markdown"
  retain_images="false"
  timeout="20"
)
```

### 参数详解

| 参数 | 推荐值 | 说明 |
|------|--------|------|
| `url` | 清理后的URL | 必须是完整URL |
| `return_format` | "markdown" | 保持原有格式 |
| `retain_images` | "false" | 新闻爬取通常不需要图片 |
| `timeout` | 20-30 | 根据网站响应调整 |
| `no_cache` | "false" | 首次爬取使用缓存 |

---

## 不同场景的调用策略

### 场景 1: 标准新闻文章

```markdown
mcp__web_reader__webReader(
  url="https://www.jiqizhixin.com/article/xxxxx"
  return_format="markdown"
  retain_images="false"
)
```

### 场景 2: 需要保留图片

```markdown
mcp__web_reader__webReader(
  url="https://www.example.com/article/xxxxx"
  return_format="markdown"
  retain_images="true"
  keep_img_data_url="true"
)
```

### 场景 3: 获取图片和链接摘要

```markdown
mcp__web_reader__webReader(
  url="https://www.example.com/article/xxxxx"
  return_format="markdown"
  with_images_summary="true"
  with_links_summary="true"
)
```

### 场景 4: 禁用 GitHub Flavored Markdown

```markdown
mcp__web_reader__webReader(
  url="https://www.example.com/article/xxxxx"
  return_format="markdown"
  no_gfm="true"
)
```

---

## 错误处理

### 错误 1: 超时

**现象**: 工具调用超时无响应

**解决方案**:
```markdown
# 增加超时时间
mcp__web_reader__webReader(
  url="..."
  timeout="30"
)
```

### 错误 2: 配额限制

**现象**: 429 错误或配额提示

**解决方案**:
- 等待配额重置
- 使用备用工具（Bash + curl）
- 建议用户提供内容

### 错误 3: 内容不完整

**现象**: 返回内容截断

**解决方案**:
- 检查是否需要登录
- 尝试增加 content_size 参数
- 使用备用方案

---

## 备用工具

如 WebReader 不可用，使用 Bash + curl：

```bash
# 获取页面 HTML
curl -s "URL" | \
  # 提取正文内容（简化示例）
  grep -oP '<div class="article-content">.*?</div>' | \
  # 转换为 Markdown
  pandoc -f html -t markdown
```

---

## 输出验证

获取内容后，快速验证：

```markdown
✅ 内容获取成功
- 字数: 约 2000 字
- 段落数: 15 段
- 图片数: 5 张
- 链接数: 8 个
```

如内容异常，提示用户并确认是否继续。

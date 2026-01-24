# Step 1: 新闻来源获取

**优先级**: ⭐⭐⭐ | **必做**: 是

---

## 目标

从多个来源获取今日AI编程相关新闻，确保信息真实可靠。

---

## 主要工具：DuckSearch MCP ⭐⭐⭐

### DuckSearch 搜索指令（优先）

**工具名称**: `mcp__web-search-prime__webSearchPrime`

**参数说明**:
- `search_query`: 搜索关键词（建议不超过70字符）
- `search_recency_filter`: 时间范围（oneDay/oneWeek/oneMonth/noLimit）
- `location`: 区域（cn=中文, us=英文）
- `content_size`: 内容长度（medium=均衡, high=详细）

**搜索今日AI编程新闻**:
```markdown
mcp__web-search-prime__webSearchPrime(
  search_query="AI编程 Claude Code Copilot 工具更新"
  location="cn"
  search_recency_filter="oneDay"
  content_size="high"
)
```

**搜索 Hacker News**:
```markdown
mcp__web-search-prime__webSearchPrime(
  search_query="site:news.ycombinator.com AI programming Claude"
  location="us"
  search_recency_filter="oneDay"
  content_size="high"
)
```

**搜索 GitHub Trending**:
```markdown
mcp__web-search-prime__webSearchPrime(
  search_query="GitHub trending AI LLM coding assistant"
  location="us"
  search_recency_filter="oneDay"
  content_size="high"
)
```

**搜索中文科技媒体**:
```markdown
mcp__web-search-prime__webSearchPrime(
  search_query="AI编程工具 36氪 机器之心 量子位"
  location="cn"
  search_recency_filter="oneDay"
  content_size="high"
)
```

### 注意：配额限制

DuckSearch 有月度配额限制，如遇 429 错误，切换到备用工具。

---

## 备用工具

如果 DuckSearch 遇到配额限制，按以下顺序使用备用工具：

### 1. WebReader MCP（爬取新闻网站内容）⭐⭐

**工具名称**: `mcp__web_reader__webReader`

**适用场景**: 当有具体新闻URL时，直接爬取页面内容

```markdown
mcp__web_reader__webReader(
  url="https://www.jiqizhixin.com/article/xxxxx"
  return_format="markdown"
  retain_images="false"
)
```

### 2. Bash + curl（Hacker News API）

```bash
# 获取最新故事ID
curl -s "https://hacker-news.firebaseio.com/v0/newstories.json" | head -20

# 获取具体故事详情
curl -s "https://hacker-news.firebaseio.com/v0/item/{id}.json"
```

### 3. WebSearch / WebFetch

作为最后的备用方案。

---

## 新闻筛选标准

### 必须包含
- ✅ AI编程工具更新/发布
- ✅ 重大技术突破
- ✅ 行业动态（收购、投资、人事变动）
- ✅ 实用工具/技巧

### 排除内容
- ❌ 纯营销新闻
- ❌ 重复报道
- ❌ 过时信息（超过3天）
- ❌ 与AI编程无关的内容

---

## 操作步骤

### 1. 使用 DuckSearch MCP 搜索

执行以下搜索（按优先级）：

**搜索 1 - 主流AI编程工具**:
```
search_query="AI编程 Claude Code Copilot Windsurf 今日新闻"
location="cn"
search_recency_filter="oneDay"
content_size="high"
```

**搜索 2 - Hacker News**:
```
search_query="site:news.ycombinator.com AI programming tool"
location="us"
search_recency_filter="oneDay"
content_size="high"
```

**搜索 3 - GitHub Trending**:
```
search_query="GitHub trending AI LLM coding assistant"
location="us"
search_recency_filter="oneDay"
content_size="high"
```

**搜索 4 - 中文科技媒体**:
```
search_query="AI编程工具 36氪 虎嗅 机器之心"
location="cn"
search_recency_filter="oneDay"
content_size="high"
```

### 2. 整理新闻列表

创建临时列表（10-15条候选新闻）：

```markdown
候选新闻列表（2026-01-24）：
1. [标题] - [来源] - [时间] - [简要说明]
2. [标题] - [来源] - [时间] - [简要说明]
...
```

### 3. 初步筛选

- 去重
- 排除低质量内容
- 保留高质量新闻（8-10条）

### 4. 进入下一步

带着筛选后的新闻列表进入 Step 2，学习用户风格。

---

## 搜索结果示例

好的搜索结果应该包含：

- 标题清晰
- 来源可靠
- 时间新鲜（24小时内）
- 内容与AI编程直接相关

**示例**:
```
1. [Claude Code 2.1发布] - Hacker News - 2小时前
   - 1096次提交，30+新功能
   - Skills热重载、Tab智能补全
```

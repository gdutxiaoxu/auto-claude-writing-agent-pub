# Step 1: URL 确认与验证

**优先级**: ⭐⭐⭐ | **必做**: 是

---

## 目标

确保目标 URL 可访问且来自支持的新闻网站。

---

## 操作步骤

### 1. URL 清理

用户提供 URL 后，进行以下清理：

```python
# 伪代码示例
def clean_url(url):
    # 移除追踪参数
    url = remove_query_params(url, ['utm_source', 'utm_medium', 'ref'])
    # 确保 HTTPS
    if url.startswith('http:'):
        url = url.replace('http:', 'https:', 1)
    return url
```

### 2. 域名验证

检查是否来自支持的网站：

**中文网站**:
- jiqizhixin.com
- qbitai.com
- 36kr.com
- huxiu.com
- tmtpost.com

**英文网站**:
- news.ycombinator.com
- techcrunch.com
- theverge.com
- arstechnica.com

### 3. 可访问性检查

使用快速 HEAD 请求检查：

```bash
curl -I -s "https://www.example.com/article/123" | head -1
```

**预期结果**:
- `200 OK` - 可继续
- `301/302` - 跟随重定向
- `404` - 提示用户检查链接
- `403` - 可能需要特殊处理

---

## 用户交互

### 情况 1: URL 有效

```
✅ URL 验证通过
来源: 机器之心
预计格式: 标准新闻文章
准备爬取...
```

### 情况 2: URL 无效

```
⚠️ 无法访问该 URL (404)
可能原因：
- 文章已被删除
- URL 输入有误

建议：
1. 检查 URL 是否完整
2. 尝试在浏览器中打开确认
```

### 情况 3: 不支持的网站

```
⚠️ 该网站暂不在支持列表中

当前支持：机器之心、量子位、36氪、Hacker News 等

建议：
1. 尝试使用 WebReader 通用模式
2. 手动复制文章内容
```

---

## 注意事项

- 不要假设 URL 总是有效的
- 给用户清晰的错误提示
- 提供可操作的解决方案

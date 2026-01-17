# 配图 Prompt（带独特理解版）

## 配图计划（4-5张）

### 1. 问题场景：上下文爆炸
**用途**：展示规则太多导致上下文爆炸的痛点

**Prompt：**
```
minimalist illustration showing a conversation window being flooded with text documents, hundreds of rules loading into a small chat interface, visual representation of context overflow, clean tech aesthetic, soft warning colors, white background, --style raw --v 6 --ar 16:9
```

---

### 2. Skills 的懒加载机制
**用途**：展示"只加载元数据 + 按需加载"的核心概念

**Prompt：**
```
clean infographic showing two tiers of data loading: top layer shows small metadata cards being loaded (low token usage), bottom layer shows detailed rule documents that only load when triggered, with arrows showing on-demand loading, minimalist design, soft blue colors, white background, --style raw --v 6 --ar 16:9
```

---

### 3. 三者对比图
**用途**：清晰展示 Skills vs CLAUDE.md vs 知识库的区别

**Prompt：**
```
clean three-column comparison infographic. Left: CLAUDE.md - all rules load every time (showing heavy load). Middle: Knowledge base - search-based loading (showing partial load). Right: Skills - metadata only + lazy loading (showing minimal load). Use visual metaphors like heavy vs light weights, clear labels, minimalist design, soft colors, white background, --style raw --v 6 --ar 16:9
```

---

### 4. 文件结构示例
**用途**：展示 Skill 文件的简单结构

**Prompt：**
```
clean code editor screenshot showing a simple file structure, a folder named "commit-helper" containing a single SKILL.md file, the file is open showing clean markdown code with YAML frontmatter, minimal interface, professional IDE aesthetic, --style raw --v 6 --ar 16:9
```

---

### 5. 核心价值总结
**用途**：总结 Skills 的独特价值

**Prompt：**
```
clean illustration showing a lightweight system scaling efficiently, concept of "write once, use forever, save tokens", visual representation of efficiency and scalability, minimalist tech style, soft green/blue colors (success colors), white background, --style raw --v 6 --ar 16:9
```

---

## 快速生成（Midjourney）

```
1. /imagine minimalist illustration showing a conversation window being flooded with text documents, hundreds of rules loading into a small chat interface, visual representation of context overflow, clean tech aesthetic, soft warning colors, white background, --style raw --v 6 --ar 16:9

2. /imagine clean infographic showing two tiers of data loading: top layer shows small metadata cards being loaded (low token usage), bottom layer shows detailed rule documents that only load when triggered, with arrows showing on-demand loading, minimalist design, soft blue colors, white background, --style raw --v 6 --ar 16:9

3. /imagine clean three-column comparison infographic. Left: CLAUDE.md - all rules load every time (heavy load). Middle: Knowledge base - search-based loading (partial load). Right: Skills - metadata only + lazy loading (minimal load). Use visual metaphors like heavy vs light weights, clear labels, minimalist design, soft colors, white background, --style raw --v 6 --ar 16:9

4. /imagine clean code editor screenshot showing a simple file structure, a folder named "commit-helper" containing a single SKILL.md file, the file is open showing clean markdown code with YAML frontmatter, minimal interface, professional IDE aesthetic, --style raw --v 6 --ar 16:9

5. /imagine clean illustration showing a lightweight system scaling efficiently, concept of "write once, use forever, save tokens", visual representation of efficiency and scalability, minimalist tech style, soft green/blue colors, white background, --style raw --v 6 --ar 16:9
```

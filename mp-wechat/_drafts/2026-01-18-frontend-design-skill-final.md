# 紫色渐变看吐了？这个 skill 拯救 AI 的审美

---

你是不是也遇到过这种事：

让 AI 帮你做个落地页、Dashboard 或者产品官网。

满怀期待地等它生成，结果——

白色背景、紫色渐变、Inter 字体、蓝绿配色。

又来。

---

真的，我快被这种"AI 标配"看吐了。

你也一样吧？

这就是现在 AI 生成界面的通病：**同质化严重，千篇一律，毫无灵魂**。

知乎上有人专门写了篇文章，标题就叫《紫色渐变UI看吐了？用Claude Skills轻松解决》，评论区全是共鸣。

直到我发现了一个东西。

---

## 一个 400 tokens 的文件

它是 Anthropic 官方出的，叫 `frontend-design` skill。

GitHub 链接放这：`https://github.com/anthropics/skills`

直接搜索 "anthropics frontend-design" 就能找到。

这个 skill 做了什么？

简单说：**它告诉 AI 什么才是"好的前端设计"，让 AI 做出正确的选择。**

你可以这么理解：

> AI 见过无数优秀设计，它不缺知识。
> 它缺的是判断标准。
>
> 这个 skill，就是把判断标准写清楚。

---

## 效果怎么样？

先给你看个真实案例。

有人在 CSDN 上分享了他的实战经验：

**第一步**：用 Frontend Design skill 生成初版登录页，重点验证"设计风格"和"结构布局"。

**第二步**：让 Claude 在同一 skill 指导下迭代优化。

结果呢？

整个页面的质感上升了一个量级。

不是那种"紫色渐变"的通用模板，而是有设计感、有品牌调性的页面。

---

还有个案例。

51CTO 的一篇文章里，作者直接用这个 skill 优化了 Waytoagi 的首页。

只用了一句话提示：

> "使用 frontend-design skill，优化一下 https://www.waytoagi.com"

效果？

从平庸的"AI 风格"，变成了有设计感的专业页面。

---

## 这个 skill 到底说了什么？

我去 GitHub 把这个 skill 的内容扒下来看了。

核心就几条原则：

### 01 字体
❌ 别用 Inter、Roboto、Arial 这些"安全字体"
✅ 用有性格的、独特的字体组合

### 02 配色
❌ 别用紫色渐变
✅ 用大胆的主色 + 尖锐的点缀色

### 03 动效
❌ 别到处散乱地加微交互
✅ 做精心编排的页面加载动画

### 04 布局
❌ 别用对称、可预测的网格
✅ 用非对称、重叠、破格元素

### 05 细节
❌ 别用纯色背景
✅ 用渐变网格、噪点纹理、几何图案

一句话：**拒绝通用，拥抱独特。**

---

## 怎么用？超简单

方法一：命令行安装（推荐）

打开终端，一行命令搞定：

```bash
npx skills-installer install @anthropics/claude-code/frontend-design --client claude-code
```

如果你用 Codex，把 `--client` 改成 `codex`。

如果你用 Cursor：

```bash
npx skills-installer install @anthropics/claude-code/frontend-design --local --client cursor
```

---

方法二：手动下载

1. 打开 `https://github.com/anthropics/skills`
2. 找到 `skills/frontend-design` 文件夹
3. 下载整个文件夹
4. 放到 `~/.claude/skills/` 目录下
5. 重启 Claude Code

---

方法三：用 skill0 市场

国内有个团队做了个 Skills 聚合平台，叫 skill0。

地址：`https://skill0.atypica.ai`

搜索 "frontend-design"，直接点击下载。

---

安装好后，怎么用？

在你的提示词里加一句：

> "使用 frontend-design skill 来完成前端设计"

就这么简单。

---

## 什么时候用？

不是所有情况都需要。

做简单的 CRUD 后台、内部工具，用不用差别不大。

但当你做这些的时候：

- **产品官网**
- **营销落地页**
- **SaaS 产品界面**
- **数据可视化 Dashboard**
- **需要惊艳效果的展示页**

这个 skill 就能派上用场。

---

## 进阶玩法

你可以在这个 skill 的基础上，加自己的东西。

比如：

- 你的品牌主色
- 你偏好的字体
- 你的圆角风格
- 你的阴影参数

这样，每次生成都符合你的品牌调性。

火山引擎有篇文章专门讲了这点：定制后的 skill 效果更稳定。

---

## 为什么 400 tokens 这么管用？

LinkedIn 上，Claude 官方账号发过一条动态：

> "我们发布了一个新的前端设计 skill。它专注于几个目标提示效果良好的领域：字体、动画、配色、布局……"

核心在于：**它不是教 AI "怎么做"，而是教 AI "怎么选"。**

AI 已经见过无数优秀设计。

它缺的，是判断标准。

有了标准，AI 就能调用它已有的知识库，做出正确的选择。

**不是注入新能力，而是激活已有能力。**

---

## 最后

2025 年是 MCP 元年。

2026 年，是 Skills 元年。

这一次，真正的分水岭不在「能不能做」。

而在「能不能把判断写成系统、让交付稳定发生」。

对于前端设计这件事，`frontend-design` skill 就是这样一个系统。

而且，这是官方出品，完全免费，现在就能用。

**去试试吧。**

---

**参考资源**：

- GitHub 官方仓库：[anthropics/skills](https://github.com/anthropics/skills/tree/main/skills/frontend-design)
- LinkedIn 官方动态：[Improving frontend design with Skills](https://www.linkedin.com/posts/claude_improving-frontend-design-with-skills-activity-7397709178083115008-Y7CC)
- 知乎教程：[紫色渐变UI看吐了？用Claude Skills轻松解决](https://zhuanlan.zhihu.com/p/1974526722738262176)
- 51CTO 教程：[【强烈推荐】这个skill 让你的claude code 构建UI 能力提升](https://developer.volcengine.com/articles/7577300725672509490)
- 火山引擎：[五个让Claude Code效率翻倍的Skill！](https://www.51cto.com/article/834077.html)

# Claude 终于会做设计了？一个 skill 搞定


上周，我让 AI 帮我做个落地页。

十分钟过去了，生成出来的东西——

白色背景，紫色渐变，Inter 字体。

我直接关了。

![image-20260119230347828](https://img.it1314.top/i2/696e47e1dad9f.png)


你也遇到过吧？

用 AI 生前端，出来的东西都长一个样。

背景非白即黑，标题栏永远是紫色渐变，字体不是 Inter 就是 Roboto，配色永远是那套蓝绿红黄。

不是说不能用，但——

**太像 AI 了。**

一眼看过去就是"机器生成"，没有灵魂，没有个性。


直到昨天，我发现了一个东西。

Anthropic 官方出的一个 skill，叫 `frontend-design`。

让我再试一次。

![img](https://pica.zhimg.com/v2-1f0744fb55da43fe8cc0f6239ad2e54c_b.jpg)


## 这次不一样了

同样的提示词，同样的模型。

我只加了一句话：

> "使用 frontend-design skill"

结果呢？

深色工业风背景，等宽科技字体，黄青撞色。

数据卡片有微妙的发光效果，图表有精心设计的动效。

布局不对称，元素有重叠。

一眼看过去——**这像人做的。**


## skill 是什么？

你可以把它理解成一个"插件"。

一个包含 `SKILL.md` 文件的文件夹，里面写着告诉 AI「在特定场景下该怎么做」的指令。

`frontend-design` 这个 skill 做的事很简单：

**把"什么是好的前端设计"这个判断标准，写清楚。**


## 官方怎么说？

LinkedIn 上，Claude 官方账号发过一条动态：

> "我们发布了一个新的前端设计 skill。它专注于几个目标提示效果良好的领域：字体、动画、配色、布局……"

GitHub 在这：[github.com/anthropics/skills](https://github.com/anthropics/skills/tree/main/skills/frontend-design)

搜 "frontend-design skill" 就能找到。


## 五个原则

我去 GitHub 看了下这个 skill 的内容。

核心就五条：

### 字体
❌ Inter、Roboto、Arial
✅ 有性格的、独特的字体组合

### 配色
❌ 紫色渐变、均匀分布的配色
✅ 大胆的主色 + 尖锐的点缀色

### 动效
❌ 零散的微交互
✅ 精心编排的页面加载动画

### 布局
❌ 对称、可预测的网格
✅ 非对称、重叠、破格元素

### 细节
❌ 纯色背景
✅ 渐变网格、噪点纹理、几何图案

**一句话：拒绝通用，拥抱独特。**


## 怎么装？三种方法

### 方法一：命令行（推荐）

打开终端，一行命令：

```bash
npx skills-installer install @anthropics/claude-code/frontend-design --client claude-code
```

如果你用 Codex，把 `--client` 改成 `codex`。

如果你用 Cursor：

```bash
npx skills-installer install @anthropics/claude-code/frontend-design --local --client cursor
```


### 方法二：手动下载

1. 打开 [github.com/anthropics/skills](https://github.com/anthropics/skills)
2. 找到 `skills/frontend-design` 文件夹
3. 下载整个文件夹
4. 放到 `~/.claude/skills/` 目录下
5. 重启工具


### 方法三：skill0 市场

国内有个团队做了个 Skills 聚合平台，叫 skill0。

地址：[skill0.atypica.ai](https://skill0.atypica.ai)

搜索 "frontend-design"，直接点击下载。


## 怎么用？

装好后，提示词里加一句就行：

> "使用 frontend-design skill 来完成前端设计"

就这么简单。


## 真实案例

有人在开发者社区分享过实战经验：

第一步，用这个 skill 生成初版登录页，重点看"设计风格"和"结构布局"对不对。

第二步，在同一 skill 指导下迭代优化。

最后整个页面的质感直接上升了一个量级。

不是那种"紫色渐变"的通用模板，而是有设计感、有品牌调性的页面。


还有个案例。

作者直接用这个 skill 优化 Waytoagi 的首页。

提示词就一句：

> "使用 frontend-design skill，优化一下 https://www.waytoagi.com"

从平庸的"AI 风格"，变成了有设计感的专业页面。


## 什么时候用？

不是所有情况都需要。

做简单的 CRUD 后台、内部工具，用不用差别不大。

但你做这些的时候：

- 产品官网
- 营销落地页
- SaaS 产品界面
- 数据可视化 Dashboard
- 需要惊艳效果的展示页

这个 skill 就能派上用场。


## 进阶玩法

你可以在原版 skill 的基础上，加自己的东西。

比如品牌主色、偏好的字体、圆角风格、阴影参数。

这样每次生成都符合你的品牌调性，效果更稳定。


## 为什么这么管用？

**它不是教 AI "怎么做"，而是教 AI "怎么选"。**

AI 已经见过无数优秀设计。

它缺的，是判断标准。

有了标准，AI 就能调用它已有的知识库，做出正确的选择。

**不是注入新能力，而是激活已有能力。**


## 最后

2025 年是 MCP 元年，2026 年是 Skills 元年。

真正的分水岭不在「能不能做」，而在「能不能把判断写成系统、让交付稳定发生」。

`frontend-design` skill 就是这样一个系统。

官方出品，完全免费，现在就能用。

**去试试吧。**


**参考资源**：

GitHub 官方仓库：anthropics/skills/frontend-design
https://github.com/anthropics/skills/tree/main/skills/frontend-design

LinkedIn 官方动态：Improving frontend design with Skills
https://www.linkedin.com/posts/claude_improving-frontend-design-with-skills-activity-7397709178083115008-Y7CC

知乎教程：紫色渐变UI看吐了？用Claude Skills轻松解决
https://zhuanlan.zhihu.com/p/1974526722738262176

51CTO 教程：【强烈推荐】这个skill 让你的claude code 构建UI 能力提升
https://developer.volcengine.com/articles/7577300725672509490

火山引擎：五个让Claude Code效率翻倍的Skill！
https://www.51cto.com/article/834077.html

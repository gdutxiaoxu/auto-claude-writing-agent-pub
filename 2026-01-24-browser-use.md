# browser-use：让 AI 真正"会用"浏览器

大家好，我是徐公，这几天刷 GitHub，看到一个项目让我眼前一亮——browser-use。

简单说，它让 AI 能够像人一样操控浏览器。听起来没什么特别的？但当你真正上手之后，会发现这东西解决了一个很实际的问题：AI 模型再聪明，也没法和网页交互。而 browser-use 填上了这个坑。

目前项目在 GitHub 上已经拿了 7.6 万星。



![browser-use 概念图](https://s.coze.cn/image/S5ZGAaEn8Mo/)



核心理念：用自然语言告诉 AI 要做什么，  剩下的让它自己搞定

</div>

## 它能做什么

先说最核心的几个功能，看完你就知道为什么它火了。

### 不用写选择器了

用过 Selenium 或 Playwright 的都 知道，定位页面元素是最头疼的。CSS 选择器、XPath 写一堆，页面一改就全废。

browser-use 的做法是：让 AI 自己理解页面结构，找到它要操作的元素。按钮、输入框、链接，它都能认出来，而且是根据语义和内容来判断，不是靠硬编码的路径。

![元素识别流程](https://s.coze.cn/image/_KMi-bkogSs/)

AI 分析页面 DOM，自动找到目标元素

### 说人话就能用

你只需要告诉它"帮我在亚马逊找个 500 块以下的蓝牙耳机加入购物车"，它会自己把任务拆成一系列操作：打开网站 → 搜索 → 筛选价格 → 选择商品 → 加入购物车。

整个过程不需要你写一行代码控制浏览器，AI 会自己规划和执行。

### 支持多种模型

GPT-4、Claude 都能用。官方还专门优化了一个 ChatBrowserUse 模型，号称比通用模型快 3-5 倍。我实测下来，确实差距挺明显的。

### 登录状态能保持

支持导入 Chrome 的配置文件，这意味着你登录过的网站、Cookie 都在。对于那些必须登录才能操作的网站（比如社交媒体、内部系统），这个功能省了不少事。

### 云服务 + 本地部署

可以用它家的云服务 Browser Use Cloud，省得自己配置环境，还带了防指纹和代理轮换。对数据敏感的话，本地 Docker 部署也支持。

### 能扩展

如果你想让它做点别的，比如操作数据库、调用 API，可以写自定义工具。这样就不限于浏览器操作了，整个业务流程都能自动化。

## 怎么做到的

技术栈其实不复杂，但组合得挺巧妙。

底层用的是 Playwright（做浏览器自动化的老牌工具），中间加了一层页面解析，把 HTML 转成结构化的 DOM 树。最核心的是元素识别层——这里用了两种策略：传统的 DOM 查询 + AI 语义理解。

简单说，它会先用文本匹配、属性过滤等方式找到候选元素，再用 AI 算一下哪个最像你要找的。多层过滤，准确率就上来了。

最上层是决策层，用大模型把你的自然语言拆成一步步操作，出错还能重试。

![技术架构](https://s.coze.cn/image/wAyV_EgGKss/)

五层架构：从浏览器控制到 AI 决策





## 怎么用

### 安装

```bash
uv init
uv add browser-use
uv sync
uvx browser-use install
```

需要 Python 3.11+。

### 一个简单的例子

```python
from browser_use import Agent, Browser, ChatBrowserUse
import asyncio

async def example():
    browser = Browser()
    llm = ChatBrowserUse()

    agent = Agent(
        task="Find the number of stars of the browser-use repo",
        llm=llm,
        browser=browser,
    )

    history = await agent.run()
    return history

if __name__ == "__main__":
    history = asyncio.run(example())
```

跑一下，它会自动打开浏览器、上 GitHub、找 browser-use 仓库、返回 star 数（目前 7.6 万左右）。

整个过程不用你写一行定位代码，全靠 AI 自己理解页面。

## 小结

browser-use 解决了一个实际问题：让 AI 能真正和网页交互。

和 Selenium、Playwright 这些传统工具比，最大的区别是不用研究页面结构，不用写选择器，你告诉它要干什么，剩下的 AI 自己搞定。


这类"AI + 自动化"的工具，以后会是 RPA 的主流方向。browser-use 算是这波浪潮里做得比较早、也比较好的一个。如果你有重复性的网页操作要自动化，值得试试。

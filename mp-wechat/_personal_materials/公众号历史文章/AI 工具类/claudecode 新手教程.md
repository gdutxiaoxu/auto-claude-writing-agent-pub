如果要问现在AI编程工具里谁是天花板，我的答案绝对是**ClaudeCode**——它的代码能力目前在业界绝对是T0级别的存在，甚至可以说是断档领先！国外已经有无数的开发者从Cursor转向ClaudeCode，而我本人也早就正式取消了Cursor的订阅，全面切换到ClaudeCode。

接下来，我将推出一系列关于ClaudeCode的介绍，而今天这期是：ClaudeCode的上手使用与自带命令详解。说实话，用过之后才发现它有多强大，很多功能完全超出预期！话不多说，直接上干货～

# **新手友好：安装两步搞定**

ClaudeCode的安装没有任何门槛，简单两步就能搞定：

1. 运行对应命令完成安装：

```
npm install -g @anthropic-ai/claude-code
```

1. 进入需要开发的项目目录，直接运行`claude`命令即可启动。

   

![图片](https://mmbiz.qpic.cn/mmbiz_png/tNu3CQGiabtryBCicsa2ibsABuIdHE2pM38QS7SPqFwofvjtxRhahHQMGibfgCSOpnicKEU5mkRh0iacYGTd9JLBRoHg/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1#imgIndex=1)

# **核心初始化命令：init**

第一次用ClaudeCode开发项目，建议先运行**`init`**命令——这是初始化命令，会自动生成一个Claude.MD文件。

![图片](https://mmbiz.qpic.cn/mmbiz_png/tNu3CQGiabtryBCicsa2ibsABuIdHE2pM383YGbMzn1bkrLbqKhaLfEeOXRhcNia6icIajF0I92bic1xTFwpPQWCKSpA/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1#imgIndex=2)

它的作用是：自动读取你项目的所有代码，然后帮你填充项目的基础结构信息最终生成的Claude.MD文件里，包含了项目Overview、常用开发命令、项目基本架构、技术选型详情、相关开发笔记等信息。这基本上就是一个完整的项目文档总览，为后续开发打下了坚实基础。

# **自带命令全解析：强大到你意想不到**

初始化完成后，我们来逐个拆解ClaudeCode的自带命令。有些命令比较基础，有些则是隐藏的实用神器，建议收藏慢慢看～

- `add-dir`：添加其他目录为工作目录。个人觉得用得不多，对于大多数项目来说，在根目录操作就足够了。

- `bug`：提交ClaudeCode bug的命令。

- `clear`：清除历史记录和上下文。这个功能非常实用，特别是对于使用API计费模式的用户。清除上下文后，ClaudeCode将不再携带历史对话信息，可以显著减少token使用量。

- `compact`：压缩上下文（清除冗余信息，但保留核心内容）。这个命令可以在清除上下文的同时，保留一份浓缩的关键信息。你甚至可以指定保留特定类型的信息。

- `config`：配置一些主题

  - Auto-compact：自动浓缩上下文，无需手动运行compact，达到阈值后自动压缩；

  - Use todo list：开启后，init生成的文件会包含项目待办清单，方便管理任务；

  - Verbose output：输入的冗长的程度；

  - Auto-updates：自动更新工具版本，确保使用最新功能；

  - Theme：设置代码Diff的颜色主题，我常用dark mode；

  - Notifications：通知；

  - Edit mode：可切换为vim模式；

  - Model：选择模型，我一般用的的Sonnet 4，Opus价格过高。

    

![图片](https://mmbiz.qpic.cn/mmbiz_png/tNu3CQGiabtryBCicsa2ibsABuIdHE2pM38ia4ia34PICxZZaa4QSicJrpfj6XLlpdIGCz5ZSOW7jG2zdRClUKEpgQMA/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1#imgIndex=3)

- `cost`：查看使用用量和消费金额。

- `doctor`：检查ClaudeCode的安装是否有问题，会输出详细的诊断信息。

- `exit`：退出命令。

- `help`：帮助命令。

- `hooks`：这是最近推出的新功能，允许你在ClaudeCode执行特定动作时插入自定义行为。支持的触发节点包括：工具使用前/后、发送通知后、停止工作后、子任务结束后。这个功能潜力巨大，我后续会探索其实用用法。

  

![图片](https://mmbiz.qpic.cn/mmbiz_png/tNu3CQGiabtryBCicsa2ibsABuIdHE2pM38M8ibkib1dYX9v5lXoWRib173YM9sdmClJuCh3DjbwmCPIvicicGxicsg5mOw/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1#imgIndex=4)

- `ide`：ClaudeCode可以连接IDE，使用IDE的各种功能（如获取打开的文件状态等）。这个功能相对复杂，我将在后续介绍中专门讲解。

- `install-github-app`：在ClaudeCode中安装GitHub应用，安装后可以在pull request中@ClaudeCode来做一些事情，比如：代码审查、解决问题。

- `login/logout`：登录/退出账号。

- `MCP`：管理MCP服务器。

- `memory`：类似Cursor的rules/memory功能，记忆文件存放在项目目录或上一层目录的CLAUDE.MD中（就是init生成的文件），帮你保留关键开发信息。

  

![图片](https://mmbiz.qpic.cn/mmbiz_png/tNu3CQGiabtryBCicsa2ibsABuIdHE2pM3801ia9TwibcDPgI88DCDSOibXXYPzqZhcVRxRTdOicmOUVQqibIJNR1mv0Bg/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1#imgIndex=5)

- `model`：快速切换模型。

- `permission`：记录ClaudeCode允许使用的命令行工具和MCP服务器（比如curl、find、git clone、ls open等）。

- `pr-comments`：从GitHub获取pull request的一些comments。

- `release-notes`：查看版本更新日志。

- `resume`：切换上下文/聊天记录。你可以切换不同的ClaudeCode会话上下文，即使不小心退出了，也能轻松恢复到之前的对话状态。

- `status`：查看详细状态，包括版本号、当前目录、MCP服务器状态、账户信息等，方便排查环境问题。

- `vim`：切换为vim编辑模式。

  

# **ClaudeCode最大亮点：自定义命令**

今天梳理的这些自带命令，已经能覆盖大部分基础开发场景，解决很多实际问题，但ClaudeCode最强大的地方，其实是**自定义命令功能**——这相当于打开了无限可能，几乎能实现你想要的所有高级玩法！

关于自定义命令的用法，以及我整理的常用实用自定义命令，后续会持续更新文章，感兴趣的同学一定要点赞关注，别错过～
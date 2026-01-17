哈喽，大家好，我是徐公。

目前，如果我们啥都不做，在不额外给风格规范/设计系统/示例参考的情况下，说得上有审美能力的编程模型只有Gemini 3 Pro、Gemini 3 Flash、Claude Opus 4.5、Claude Sonnet 4.5四款。

当我们看到GPT-5.2-Codex等明明其他方便都挺厉害、但是唯独前端审美不行的模型的时候，尝尝感叹“哀其不幸、怒其不争”。

如果我们想要包括GPT-5.2-Codex、GLM-4.7、M2.1在内的其他主流模型也拥有审美能力，怎么办？是否有快速提升他们前端审美能力的方法呢？

有。

答案是：skill

近期发布的主流编程大模型全都已经原生支持skill协议，我们为其安装Anthropic官方提供的frontend-design skill，即可立即提升所有主流模型的前端审美能力。

不信？我们先看看效果对比。

效果对比

对于

```
重新设计 https://raphael.app 的首页
```

这条简单的指令。

如果我们直接下达任务给GPT-5.2-Codex，效果如下。

![图片](https://mmbiz.qpic.cn/mmbiz_png/607DKnuWzlGAQErqjLpWZcKFJ3Tx3ujgEl45AcEiaGLRdxWnHVqlSTBCFUvnzQiboejT7TtG24FgPBOJOwpFgqVQ/640?wx_fmt=png&from=appmsg&tp=wxpic&wxfrom=5&wx_lazy=1#imgIndex=0)

![图片](https://mmbiz.qpic.cn/mmbiz_png/607DKnuWzlGAQErqjLpWZcKFJ3Tx3ujg409V2swDTaKwELpYeaOD1v6pgRXBOkvchR9qhffXtBzf9mj3uNZOicw/640?wx_fmt=png&from=appmsg&tp=wxpic&wxfrom=5&wx_lazy=1#imgIndex=1)

不是我黑它，下图右边那个奇怪的圆圈，它就长那样，根本不工作。你看到的，已经是完整截图了。看上去好像是有动效的样子，其实没有。

如果我们使用skill，效果如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/607DKnuWzlGAQErqjLpWZcKFJ3Tx3ujgvcje57BnwRLLNjdlGibscokSHlMyzXXqPQrQOtu99LtvIKYRK6Kn0hg/640?wx_fmt=png&from=appmsg&tp=wxpic&wxfrom=5&wx_lazy=1#imgIndex=2)

![图片](https://mmbiz.qpic.cn/mmbiz_png/607DKnuWzlGAQErqjLpWZcKFJ3Tx3ujgricwS4sG1NbrEUU0ibexJKJ05uIaBreHKTCGdm7CH9syXyUEDLysAdIw/640?wx_fmt=png&from=appmsg&tp=wxpic&wxfrom=5&wx_lazy=1#imgIndex=3)

我们可以看到，使用front-design skill后，无论是字体、一致性、动画效果、质感、排版，都有质的飞跃。

嘿嘿，神奇吗？



什么原理？

其实并不神奇。

你可以这么理解：大模型就像一个拥有全世界菜谱的顶级厨师。

普通指令“给我做顿饭”， 厨师为了保险、或者为了偷懒、或者**受限于它自身的品味**，它会给你做一盘西红柿炒鸡蛋，虽然能吃，但很普通。

使用Frontend-design Skill，等同于额外强调了 “你是米其林三星主厨，请务必使用分子料理技术，做一道展现‘深海孤独感’的创意菜，拒绝使用常规调料”并且详细给出了什么是“分子料理技术”、什么是“深海孤独感”、还有哪些注意事项，厨师就会调动他毕生所学，给你做出一道艺术品。

Anthroipic的Frontend-design skill的工作方式正是如此，它特别强调了动效、质感、字体、一致性、情感化连接、大胆美学(Bold Aesthetic)、意图表达(Intentionality)等等，而大模型完全可以理解这个skill给出的要求和菜谱。

我认为，Frontend-design skill是一款教科书级的skill，虽然简短，但是它是完全针对大模型工作原理和底层工作方法来写的，能够稳定发挥化腐朽为神奇、四两拨千斤的效果，充分调用了大模型自身已经蕴含的强大能力。



如何使用？

很简单，一句命令行的事。

如果你用Claude Code，执行这条命令。

我知道我有很多读者朋友使用国产模型GLM-4.7、M2.1来驱动Claude Code，嗯，也是可以的，只要是Claude Code，都可以。

```
npx skills-installer install @anthropics/claude-code/frontend-design --client claude-code
```

如果你用Codex，执行这条命令。它同时对Codex CLI和Codex IDE Extension生效。在上面的演示中，其实我用的是Codex IDE Extension。

```
npx skills-installer install @anthropics/claude-code/frontend-design --client codex
```

如果你使用的是Cursor

```
npx skills-installer install @anthropics/claude-code/frontend-design --local --client cursor
```

安装完成后，在我们Vibe Coding需要用到前端设计能力的时候，只需要稍微强调一句“使用frontend-design skill来完成前端设计工作”，就能够召唤它了。

对了，额外嘱咐几句：

- 如果是新项目、不加任何约束，这个Skill会不安装任何依赖，快速完成html； 
- 如果是老项目或者显式强调依赖，它会按照你要求的技术栈来完成工作。
- 你还可以做一些修改：在原版frontend-design skill的基础上，把你自己的品味（主色/字体/圆角/阴影/按钮风格）等等写进去，成为一个 新的skill，让模型每次都按你的品牌调性出图，表现更好。



------



好的，分享完了，到你了。

去试试吧！欢迎到评论区交流！
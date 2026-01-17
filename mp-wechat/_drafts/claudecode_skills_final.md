# Claude Code 这个被低估的功能，让我少写了一半重复指令

哈喽，大家好，我是徐公。

之前写 Plan Mode 那篇文章时，我说这是我最推荐的功能。但如果只选一个"被严重低估"的功能，我的答案是：**Skills**。

说实话，刚开始用 Claude Code 的时候，我根本没把这个功能当回事。一个 markdown 文件能有多大威力？

直到最近我才意识到：**这不是写文档，这是在给 Claude 装"插件"。**

---

## 一个真实场景

先说个场景，大家可能都遇到过。

我们团队有个 commit message 的规范：标题要控制在 50 字以内、用现在时态、要说明"做了什么"和"为什么"。但每次写 commit 的时候，标准都不统一，有人写"fix bug"，有人写"修复登录问题"，有人写"fix: login error"。

领导在群里强调了三次，还是不行。

后来我才发现，这种事情根本不需要靠"强调"，用 Claude Code 的 Skills 功能，一个 markdown 文件就能解决。

---

## Skills 是什么？

Skills 就是教 Claude 按你的方式做事。

以前你每次都要说"commit message 要这样写..."，现在写一次，Claude 就记住了。

你可以把它理解为：**给 Claude 装"插件"**。

---

## 和 Slash Commands 的区别

很多人搞不清楚这两者的区别，这个很重要。

| 功能 | Slash Commands | Skills |
|------|----------------|--------|
| 触发方式 | 你手动输入 `/commit` | Claude 自动判断 |
| 典型场景 | `/deploy staging` 这种一次性操作 | 审查代码、生成文档这种需要"理解标准"的事 |
| 权限控制 | 无 | 可以限制可用工具 |

打个比方：
- Slash Commands 是**快捷键**，你按它才执行
- Skills 是**自动补全规则**，它在你需要的时候自动出现

---

## 第一个 Skill：commit message 生成器

我试着写了一个最简单的 Skill，看看能不能解决 commit message 标准不统一的问题。

### 文件结构

```
~/.claude/skills/commit-helper/
└── SKILL.md
```

### SKILL.md 内容

```markdown
---
name: commit-helper
description: 生成符合团队规范的 commit message。当用户提到 git、commit、提交代码时自动使用。
---

# Commit Message 规范

## 格式要求
- 标题：50 字以内，现在时态
- 说明"做了什么"和"为什么"
- 不要写"如何实现"

## 示例

好的：
- feat: 添加用户头像上传功能
- fix: 修复登录时 token 过期问题
- docs: 更新 API 文档

不好的：
- fix bug（太笼统）
- 修改 login 函数逻辑（写了"如何"）
- add feature（没说明是什么功能）

## 使用方式
运行 `git diff --staged` 查看改动，然后生成 commit message。
```

就这？

对，就这。把这个文件放进去，Claude 就学会了。

### 效果对比

**没有 Skill 时：**
```
我：帮我写个 commit message
Claude：Add new feature for user login
```

**有 Skill 后：**
```
我：帮我写个 commit message
Claude：feat: 添加第三方登录支持
```

同一个 Claude，不同的标准，完全不一样的体验。

---

## 核心机制：description 是关键

SKILL.md 最重要的是 **description** 字段。

这是 Claude 判断"什么时候用这个 Skill"的唯一依据。description 写得好不好，直接决定 Skill 会不会被触发。

### 好的 description

```yaml
description: 提取 PDF 文件的文本和表格、填充表单、合并文档。当用户处理 PDF 文件、表单或文档提取时使用。
```

**为什么好：**
- 列出了具体动作（提取、填充、合并）
- 有触发关键词（PDF、表单、文档提取）
- 清楚说明"什么时候用"

### 不好的 description

```yaml
description: 帮你处理文档
```

**为什么不好：**
- 太宽泛，Claude 不知道什么情况下用
- 没有触发关键词
- 和其他 Skill 容易冲突

---

## 进阶用法：限制工具权限

有些 Skill 应该是"只读"的，比如帮你看代码但不让你改。

用 `allowed-tools` 就能限制：

```yaml
---
name: code-reviewer
description: 审查代码质量，不修改文件。当用户说"审查"、"review"、"检查代码"时使用。
allowed-tools:
  - Read
  - Grep
  - Glob
---
```

这样 Claude 在用这个 Skill 时，只能读文件，不能写。

---

## 进阶用法：多文件 Skill

当 Skill 变复杂时，一个 SKILL.md 会很长。

可以用"渐进式披露"：

```
my-skill/
├── SKILL.md          # 核心内容
├── examples.md       # 示例（按需加载）
├── reference.md      # 详细文档（按需加载）
└── scripts/
    └── helper.py     # 工具脚本
```

SKILL.md 里这样写：

```markdown
## 快速开始
[核心指令]

## 更多资源
- 详细文档见 [reference.md](reference.md)
- 使用示例见 [examples.md](examples.md)

## 工具脚本
运行 `python scripts/helper.py` 进行验证。
```

Claude 不会一下子把所有文件都读进来，而是需要时才加载。

---

## 我怎么判断什么时候用

什么时候用 Skills，什么时候用其他方式？

**用 Skills：**需要反复执行的"标准操作"（代码审查、文档生成、commit 格式）、团队规范需要统一、需要限制工具权限

**用 Slash Commands：**一次性操作（`/deploy staging`）、需要手动触发的命令

**用 CLAUDE.md：**项目全局规则（TypeScript 严格模式、目录结构）

---

## 踩坑经验

### 坑1：description 写得太模糊

我的第一个 Skill，description 写的是"帮助写 commit message"。

结果？从来不会自动触发。

后来改成"生成符合团队规范的 commit message，当用户提到 git、commit、提交代码时自动使用"，就好了。

嘿嘿，有时候觉得 Claude 跟人一样，你话说得不清楚，它也不知道该干嘛。

### 坑2：YAML 格式写错了

YAML frontmatter 有三个注意点：
- 必须以 `---` 开头（前面不能有空行）
- 缩进用空格，不要用 Tab
- 结尾也要有 `---`

如果 YAML 格式错了，Skill 根本不会加载，但不会有任何报错提示。

那会儿我折腾了半天，以为是路径问题，最后才发现是格式错了。

怎么排查？运行 `claude --debug` 查看加载日志。

### 坑3：多 Skills 冲突

我有两个 Skills，description 都包含"代码审查"，结果 Claude 经常用错。

解决方法很简单：让 description 更具体。
- 一个改为"审查 JavaScript 代码质量"
- 一个改为"审查 Python 代码安全漏洞"

区分度够了，问题就解决了。

---

## 团队协作

Skills 是可以共享的：

1. **项目级**：把 `.claude/skills/` 提交到 Git，整个团队都能用
2. **全局级**：放在 `~/.claude/skills/`，个人所有项目都能用
3. **企业级**：管理员统一部署

比如你们团队的代码审查规范，写成 Skill 后提交到项目仓库，所有人拉代码后自动就有了。

---

## 小结

Skills 最大的价值，不是"多了一个命令"，而是**把专业知识和最佳实践固化成可复用的能力**。

以前这些经验只能靠"口口相传"，现在写成 Skill，Claude 自动按标准执行。

如果你也在用 Claude Code，建议从最简单的开始试：commit message 生成器、代码审查规范、文档模板……

写一次，反复用。

有其他 Claude Code 的使用心得？欢迎到评论区分享！

我是徐公，我们下次见～

---

## 文章元数据

**发布日期**：2026-01-17
**分类**：AI 工具类
**标签**：Claude Code、Skills、AI 编程、效率提升
**字数**：约 2,700 字
**配图**：7 张

**写作时长**：约 2 小时
**审校轮次**：3 轮（初稿 → 降 AI 味 → 细节打磨）

**核心修改记录：**
1. 删除了"简单说"等套话
2. 调整了过于规整的列表结构
3. 增加了"嘿嘿"、"那会儿"等个人特色表达
4. 简化了一些书面化表达

**参考资料：**
- [Agent Skills - Claude Code Docs](https://code.claude.com/docs/en/skills)
- [Claude Code Skills: Complete Guide](https://claude-world.com/articles/skills-guide/)
- [Build Your First Claude Code Agent Skill](https://medium.com/@richardhightower/build-your-first-claude-code-skill-a-simple-project-memory-system-that-saves-hours-1d13f21aff9e)

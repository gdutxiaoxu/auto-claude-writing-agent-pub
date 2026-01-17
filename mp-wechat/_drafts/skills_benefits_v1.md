# Claude Code 的 Skills：写一次规则，让 AI 记一辈子

哈喽，大家好，我是徐公。

今天说个很多人没注意到，但用了就回不去的功能：**Skills**。

---

## 问题：每次都要说一遍规则

用 Claude Code 的时候，你有没有遇到过这种情况：

每次让它生成 commit message，它都写得不合你规范。每次你都要说：
- 标题要控制在 50 字以内
- 用现在时态
- 说明"做了什么"和"为什么"

一次两次还好，次数多了真的很烦。

---

## 解决方案：Skills

Skills 的想法很简单：**把规则写一次，Claude 就学会了。**

你只需要创建一个 markdown 文件，告诉 Claude 你的规范。以后它每次都会按这个标准来。

再也不用重复说了。

---

## 一个简单例子

### 第一步：创建文件夹

在 `~/.claude/skills/` 下创建一个文件夹：

```
~/.claude/skills/commit-helper/
```

### 第二步：创建 SKILL.md

在这个文件夹里创建 `SKILL.md`：

```markdown
---
name: commit-helper
description: 生成符合规范的 commit message。当用户提到 git、commit、提交代码时自动使用。
---

# Commit Message 规范

## 格式要求
- 标题：50 字以内，现在时态
- 说明"做了什么"和"为什么"
- 不要写"如何实现"

## 好的例子
- feat: 添加用户头像上传功能
- fix: 修复登录时 token 过期问题
- docs: 更新 API 文档

## 不好的例子
- fix bug（太笼统）
- 修改 login 函数逻辑（写了"如何"）
- add feature（没说明是什么功能）
```

### 第三步：完成

就这？

对，就这。

现在你只要说"帮我写个 commit message"，Claude 就会按照你的规范来生成。

---

## Skills 的好处

### 1. 不用重复说

写一次，反复用。以后再也不用每次都解释一遍规则。

### 2. 团队规范统一

把 Skill 提交到项目仓库，整个团队都能用。所有人生成的 commit message 格式都一样。

### 3. 自动触发

你不需要手动调用，Claude 会根据你的请求自动选择合适的 Skill。

### 4. 可以限制权限

有些 Skill 可以设置为"只读"，比如代码审查。Claude 只能看代码，不能改。

### 5. 支持复杂规则

不只是 commit message，代码审查规范、API 文档风格、数据库查询模式……任何需要"按标准办事"的场景都适用。

---

## 什么时候用 Skills

**用 Skills：**需要反复执行的"标准操作"（代码审查、文档生成、commit 格式）、团队规范需要统一

**用 Slash Commands：**一次性操作（`/deploy staging`）、需要手动触发的命令

**用 CLAUDE.md：**项目全局规则（TypeScript 严格模式、目录结构）

---

## 小结

Skills 最大的价值，是**把专业知识和最佳实践固化成可复用的能力**。

以前这些经验只能靠"口口相传"，现在写成 Skill，Claude 自动按标准执行。

写一次，反复用。这种感觉很爽。

有其他 Claude Code 的使用心得？欢迎到评论区分享！

我是徐公，我们下次见～

---

**参考资料：**
- [Agent Skills - Claude Code Docs](https://code.claude.com/docs/en/skills)

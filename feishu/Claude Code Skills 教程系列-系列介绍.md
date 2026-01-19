# **Claude Code Skills 教程**，从零到实践的完整指南

本 PDF 内容可能不是最新的，为了方便大家及时获取最新的教程，请大家点击下面链接获取最新的**Claude Code Skills 教程**，从零到实践的完整指南

[Claude Code Skills 教程系列：从零到实践的完整指南](https://my.feishu.cn/wiki/space/7596622993011248349?ccm_open_type=lark_wiki_spaceLink&open_tab_from=wiki_home)

[Claude Code Skills 教程系列：从零到实践的完整指南](https://my.feishu.cn/wiki/space/7596622993011248349?ccm_open_type=lark_wiki_spaceLink&open_tab_from=wiki_home)

[Claude Code Skills 教程系列：从零到实践的完整指南](https://my.feishu.cn/wiki/space/7596622993011248349?ccm_open_type=lark_wiki_spaceLink&open_tab_from=wiki_home)

## 为什么需要 Skills？

### 痛点一：重复输入指令

每次用 Claude 都要重新描述背景：
```
我用 TypeScript + React，代码规范是...
文档要用中文，格式要...
```
一天 5 次，一年浪费数十万 tokens。

**解决**：创建技能，一次配置，自动调用。

### 痛点二：专业知识难以复用

你的项目架构、业务规则、代码规范，Claude 记不住。每次都要重新解释，还可能说错。

**解决**：技能可以把这些知识"打包"，需要时自动加载。

### 痛点三：团队没有统一标准

A 同事的代码风格、B 同事的文档格式、C 同事的测试标准...各不相同。

**解决**：技能放 Git 仓库，团队共享，标准统一。

---

## Skills 是什么？

**简单说**：用 Markdown 写的一个配置文件，告诉 Claude 什么时候做什么。

**最简结构**：
```
my-skill/
└── SKILL.md
```

**SKILL.md 示例**：
```yaml
---
name: prd-generator
description: 从会议记录生成产品需求文档
---

# PRD 生成器

## 执行步骤
1. 提取需求要点
2. 补充背景信息
3. 生成标准 PRD 格式
```

就这么简单。

---

## 核心机制：渐进式披露

这是 Skills 最关键的设计。

**问题**：50 个技能，每个 3000 tokens，一次加载就是 15 万 tokens，上下文窗口直接爆满。

**解决**：三级加载
- **第一级**：只加载技能名称和描述（~100 tokens）
- **第二级**：需要时才加载完整 SKILL.md（~3000 tokens）
- **第三级**：具体使用时才加载参考文件

**效果**：初始加载节省 90%+ tokens。

---

## 本系列文章

### 入门（1-3）
1. **Claude Code Skills 入门**：基本概念和价值
2. **5分钟上手**：手把手创建第一个技能
3. **Skills vs 斜杠命令 vs MCP**：三种机制对比

### 进阶（4-6）
4. **渐进式披露**：核心机制深度剖析
5. **SKILL.md 编写指南**：如何写好技能描述
6. **高级模式**：让技能更强大的组织方式

### 实战（7-9）
7. **实战案例**：3 个真实案例展示效率提升
8. **5 个必装 Skills**：官方和社区精选技能
9. **从零创建自定义技能**：六步完整流程

### 展望（10）
10. **生态与未来**：个人 Agent 的基石

---

## 适用人群

- **开发者**：代码规范、API 文档生成
- **产品经理**：PRD 生成、需求整理
- **内容创作者**：多平台内容自动适配
- **团队协作**：知识沉淀、标准统一

---

## 学习建议

**零基础**：按顺序阅读，第 1-2 篇必看

**有经验**：直接看第 5 篇（编写指南）和第 9 篇（自定义技能）

**快速应用**：看第 2 篇（5分钟上手）+ 第 8 篇（必装技能）

---

## 系列目录

1. [Claude Code Skills 入门：什么是 Skills，为什么你需要它](./Claude%20Code%20Skills%20入门：什么是%20Skills，为什么你需要它.md)
2. [5分钟上手Claude Skills：从零到第一个技能](./5分钟上手Claude%20Skills：从零到第一个技能.md)
3. [Skills vs 斜杠命令 vs MCP：你应该用哪个？](./Skills%20vs%20斜杠命令%20vs%20MCP：你应该用哪个？.md)
4. [渐进式披露：Claude Skills的核心秘密](./渐进式披露：Claude%20Skills的核心秘密.md)
5. [SKILL.md编写指南：写好技能描述是成功的一半](./SKILL.md编写指南：写好技能描述是成功的一半.md)
6. [Claude Code Skills 高级模式：让技能更强大的组织方式](./Claude%20Code%20Skills%20高级模式：让技能更强大的组织方式.md)
7. [实战案例：用5分钟完成半天的工作量](./实战案例：用5分钟完成半天的工作量.md)
8. [5个必装的Claude Skills，效率直接翻倍](./5个必装的Claude%20Skills，效率直接翻倍.md)
9. [从零创建自定义技能：六步完整流程](./从零创建自定义技能：六步完整流程.md)
10. [Claude Skills 生态与未来：个人 Agent 的基石](./Claude%20Skills%20生态与未来：个人%20Agent%20的基石.md)

---

**开始构建你的知识空间。**

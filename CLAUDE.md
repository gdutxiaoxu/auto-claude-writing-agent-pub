# 自动化写作 Agent - 总控文档

> **版本**：v3.0 | **更新时间**：2026-01-17
> **作用**：多平台写作Agent的总控规则和导航中心
> **架构**：官方Claude Skills系统（自动触发）

---

## ⚡ 新架构：官方 Claude Skills

**v3.0 重要更新**：现已采用官方Claude Skills规范，Claude会根据任务自动触发对应Skills。

### 工作方式

Skills是**自动触发**的：
- 当用户提出写作相关请求时，Claude自动加载相关Skills
- 无需手动指定，Claude根据`description`字段判断何时使用
- 支持渐进式披露：主SKILL.md可链接到详细文档

### 官方Skills目录结构

```
.claude/skills/                  # 项目Skills目录
├── task-judgment/               # 任务类型判断
│   └── SKILL.md
├── writing-principles/          # 写作核心原则
│   └── SKILL.md
├── think-aloud/                 # Think Aloud规范
│   └── SKILL.md
└── mp-wechat-flow/              # 微信公众号完整流程
    ├── SKILL.md                 # 流程总览
    └── steps/                   # 渐进式披露：详细步骤
        ├── step1-brief.md
        ├── step2-research.md
        ├── step3-topic.md
        └── ...（共10步）
```

### 架构优势

- ✅ **自动触发**：Claude根据任务自动选择Skills
- ✅ **渐进式披露**：核心信息在SKILL.md，详情在链接文件
- ✅ **易于维护**：每个skill独立文件夹，修改方便
- ✅ **可扩展**：新增平台只需添加新skill目录

---

## 🎯 这是什么？

这是一个**多平台自动化写作系统**，帮助您高效创作不同平台的内容。

**核心理念**：
- 流程是指南，不是教条
- 核心原则不可妥协
- Think Aloud贯穿始终
- 真实性 > 完美性

---

## 📂 项目结构

```
/writing/
├── CLAUDE.md                    # 【你在这里】总控文档
├── .claude/
│   └── skills/                  # 【新增】官方Skills目录
│       ├── task-judgment/       # 任务判断
│       ├── writing-principles/  # 核心原则
│       ├── think-aloud/         # 思考规范
│       └── mp-wechat-flow/      # 公众号流程
│           ├── SKILL.md
│           └── steps/
├── mp-wechat/                   # 微信公众号写作工作区
│   ├── _briefs/                 # 需求文档
│   ├── _drafts/                 # 草稿文件
│   ├── _published/              # 已发布文章
│   ├── _personal_materials/     # 个人素材库
│   ├── _writing_reference/      # 写作参考
│   ├── _knowledge_base/         # 知识库
│   └── images/                  # 图片资源
├── x-twitter/                   # X（Twitter）写作【待创建】
├── xiaohongshu/                 # 小红书写作【待创建】
└── ...                          # 其他平台
```

---

## 🚀 如何使用

### 自动触发机制

当您提出写作相关请求时，Claude会：

1. **自动识别任务类型**
   - 加载 `task-judgment` skill
   - 判断是：新写作/修改文章/审校降AI味/快速咨询

2. **自动应用核心原则**
   - 加载 `writing-principles` skill
   - 确保不编造数据、不使用过时信息等

3. **自动使用Think Aloud**
   - 加载 `think-aloud` skill
   - 在关键决策时透明化思考过程

4. **自动执行平台流程**
   - 如是公众号任务，加载 `mp-wechat-flow` skill
   - 按流程执行，按需读取详细步骤文档

### 示例对话

**用户**："帮我写一篇关于Claude Code的公众号文章"

**Claude自动**：
1. 触发 `task-judgment` → 判断为类型A（新写作任务）
2. 触发 `think-aloud` → 说明思考过程
3. 触发 `mp-wechat-flow` → 加载公众号10步流程
4. 执行Step 3（选题讨论） → 提供3-4个选题方案
5. 等待用户确认...

---

## 📖 可用Skills

### 核心Skills

| Skill | 触发条件 | 作用 |
|-------|---------|------|
| `task-judgment` | 收到写作请求 | 判断任务类型（A/B/C/D/E） |
| `writing-principles` | 任何写作任务 | 应用四大核心原则 |
| `think-aloud` | 关键决策时刻 | 透明化思考过程 |

### 平台Skills

| Skill | 触发条件 | 作用 |
|-------|---------|------|
| `mp-wechat-flow` | 公众号写作任务 | 完整10步写作流程 |

---

## ⚠️ 核心原则（不可妥协）

### 1. 绝不编造数据 ❌
### 2. 绝不使用过时信息 ❌
### 3. 绝不省略Think Aloud ❌
### 4. 绝不跳过用户确认（重要决策） ❌

详见：[`.claude/skills/writing-principles/SKILL.md`](.claude/skills/writing-principles/SKILL.md)

---

## 📊 任务类型

收到写作请求后，Claude会自动判断：

- **A. 新写作任务（有完整brief）** → 完整流程
- **B. 新写作任务（无brief）** → 先创建brief
- **C. 修改已有文章** → 读取→修改→审校
- **D. 文章审校/降AI味** → 三遍审校流程
- **E. 快速咨询** → 直接回答

详见：[`.claude/skills/task-judgment/SKILL.md`](.claude/skills/task-judgment/SKILL.md)

---

## 📖 各平台规则文档

### 微信公众号

**Skill**: [`.claude/skills/mp-wechat-flow/SKILL.md`](.claude/skills/mp-wechat-flow/SKILL.md)

- **字数**: 1500-3000字
- **配图**: 推荐5-8张
- **风格**: 实践+落地，真实案例
- **流程**: 10步完整流程

### 其他平台（待创建）

- **X/Twitter**: 待创建
- **小红书**: 待创建
- **知乎**: 待创建

---

## 🛠️ 技巧与参考

技巧类内容（微幽默、强开头、概念把手等）暂未skill化，仍保留在原文档中。

详见：[`mp-wechat/CLAUDE.md`](mp-wechat/CLAUDE.md)

---

## 📞 联系与反馈

如果发现：
- Skills配置有误
- 流程可以优化
- 新增平台需求
- 其他建议

请直接告诉我。

---

## 版本历史

**v3.0 (2026-01-17)**
- 采用官方Claude Skills规范
- 目录迁移到 `.claude/skills/`
- 每个skill独立文件夹，包含SKILL.md
- 支持自动触发和渐进式披露

**v2.0 (2026-01-17)**
- 初次尝试Skills渐进式加载架构（非官方规范）

**v1.0 (2025-11-02)**
- 初始版本
- 建立多平台架构

---

**这是总控文档v3.0，采用官方Claude Skills系统。**

**原则：流程是指南，不是教条。核心原则不可妥协。**



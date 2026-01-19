# SKILL.md编写指南：写好技能描述是成功的一半

作者：[你的名字]

> 这是「Claude Code Skills 教程系列」的第 5 篇。
>
> 前几篇我们讲了什么是 Skills、渐进式披露机制、以及如何从零创建第一个技能。但有一个问题很多人遇到了：
>
> **为什么我写的技能总不被 Claude 触发？**
>
> 答案很简单：你的 SKILL.md 没写好。
>
> 尤其是那个看似不起眼的 `description` 字段，它决定了你的技能会不会被"召唤"出来。

---

## 一、痛点切入：技能写了但没人用？

上周有读者问我：

> "我按照教程创建了一个技能，放在 `.claude/skills/` 目录下，但是每次跟 Claude 对话，它都不主动用。我非得明确说'用 xxx 技能'它才会动。这是不是 bug？"

这不是 bug。这是你的 `description` 写得太模糊了。

让我给你看个真实例子。

**❌ 坏的描述**：
```yaml
---
name: my-helper
description: 这是一个帮助我的技能
---
```

Claude 看到这个描述时，内心是崩溃的——帮助什么？什么时候用？我该在什么场景下加载它？

**✅ 好的描述**：
```yaml
---
name: prd-generator
description: 当需要将会议记录、需求讨论整理成规范的产品需求文档时使用此技能
---
```

Claude 看到这个描述时，立即明白了三件事：
- **什么时候用**：需要整理会议记录、需求讨论时
- **用来做什么**：生成产品需求文档（PRD）
- **触发关键词**：会议记录、需求讨论、PRD、产品需求文档

你看，同样是写技能，一个写了之后吃灰，一个却能自动触发。区别就在 `description` 这短短几行字。

---

## 二、Frontmatter 元数据：技能的"身份证"

每个 SKILL.md 文件的开头，都有一个 YAML 格式的元数据区块：

```yaml
---
name: your-skill-name
description: 这个技能做什么以及何时使用
---

# 技能名称（可选）
...
```

这个区块有两个字段：`name` 和 `description`。

### 2.1 name 字段：命名有学问

**命名原则**：
- ✅ 用 kebab-case（小写字母+连字符）
- ✅ 简短但能说明用途
- ✅ 避免通用词

**❌ 坏例子**：
```yaml
name: helper           # 太通用，不知道帮什么
name: code             # 太宽泛
name: my-skill         # 没有任何信息量
name: 文章写作         # 不要用中文（可能有问题）
```

**✅ 好例子**：
```yaml
name: prd-generator              # PRD 生成器
name: typescript-coding-standards # TypeScript 代码规范
name: wechat-article-writer       # 微信公众号文章写作
name: pdf-processor               # PDF 处理器
```

**命名模式推荐**：
- `动作-对象`：`prd-generator`、`api-doc-generator`
- `对象-用途`：`typescript-coding-standards`、`mysql-query-helper`
- `平台-任务`：`wechat-article-writer`、`twitter-post-creator`

### 2.2 description 字段：触发成功的关键【重点】

把 description 写好，你的技能才能真正被 Claude 用起来。

**Claude 如何使用 description**：

1. **启动时扫描**：Claude 启动时会读取所有技能的 description（约 100 tokens）
2. **实时匹配**：每次收到用户请求，Claude 会扫描所有 description，判断哪个技能相关
3. **按需加载**：匹配成功后，才读取完整的 SKILL.md

**所以，description 的目标只有一个：让 Claude 准确判断"何时该用这个技能"。**

---

## 三、description 字段的写作原则

### 原则 1：明确"何时使用"

**❌ 坏的描述**：
```yaml
description: 这是一个关于 PRD 的技能
```

问题：PRD 什么事？创建 PRD？修改 PRD？评审 PRD？

**✅ 好的描述**：
```yaml
description: 当需要将会议记录、需求讨论整理成规范的产品需求文档时使用此技能
```

改进：
- 明确了**输入**：会议记录、需求讨论
- 明确了**输出**：产品需求文档
- 明确了**场景**：整理、规范化

### 原则 2：包含触发关键词

Claude 通过关键词匹配来判断是否需要加载技能。

**❌ 坏的描述**：
```yaml
description: 辅助完成开发任务
```

问题：太宽泛，什么开发任务？写代码？调试？部署？

**✅ 好的描述**：
```yaml
description: 当编写 TypeScript 代码时使用，确保符合团队的命名规范、函数长度要求和错误处理标准
```

改进：
- **关键词**：TypeScript、代码、命名规范、函数长度、错误处理
- **场景明确**：编写代码时
- **结果预期**：符合团队标准

### 原则 3：避免模糊词汇

**❌ 常见模糊词汇**（不要用）：
- "帮助"（帮什么？）
- "辅助"（辅助什么？）
- "优化"（优化什么？）
- "提升"（提升什么？）
- "相关"（什么相关？）

**✅ 替换为具体词汇**：
- "帮助" → "生成 XXX"、"检查 XXX"、"转换 XXX"
- "优化" → "重构代码"、"改进性能"、"简化逻辑"
- "提升" → "提高代码可读性"、"减少重复代码"

**示例对比**：

❌ **模糊版本**：
```yaml
description: 帮助优化代码
```

✅ **具体版本**：
```yaml
description: 当需要重构代码以提高可读性、减少重复逻辑、添加类型注解时使用
```

### 原则 4：控制在 1-2 句话内

**太短不好**：
```yaml
description: PRD 生成
```
→ Claude 不知道从什么材料生成

**太长也不好**：
```yaml
description: 当用户提供了会议记录、需求讨论、用户反馈、竞品分析等多种原始材料，需要将这些信息整合成一份结构化的、符合公司规范的产品需求文档时使用此技能，该文档应包含需求背景、目标用户、功能列表、优先级排序、验收标准等完整内容...
```
→ 信息过载，Claude 难以快速抓取重点

**✅ 刚刚好**：
```yaml
description: 当需要将会议记录、需求讨论、用户反馈整理成结构化的产品需求文档时使用
```

→ 一句话讲清楚：输入 + 输出 + 场景

---

## 四、description 写作模板

给你几个常用模板：

### 模板 1：转换型技能
**适用场景**：将一种格式转换为另一种格式

```yaml
description: 当需要将 [输入格式] 转换为 [输出格式] 时使用
```

**示例**：
```yaml
description: 当需要将会议记录转换为结构化的产品需求文档时使用
description: 当需要将代码注释提取生成 API 文档时使用
description: 当需要将 Markdown 文档转换为 PowerPoint 演示文稿时使用
```

### 模板 2：检查型技能
**适用场景**：检查、审核、验证

```yaml
description: 当需要检查 [对象] 的 [标准/要求] 时使用
```

**示例**：
```yaml
description: 当需要检查 TypeScript 代码是否符合团队编码规范时使用
description: 当需要审核产品需求文档的完整性和合理性时使用
description: 当需要验证 SQL 查询的性能和安全性时使用
```

### 模板 3：生成型技能
**适用场景**：从零创建内容

```yaml
description: 当需要生成 [内容类型] 用于 [目的] 时使用
```

**示例**：
```yaml
description: 当需要生成微信公众号文章用于分享技术知识时使用
description: 当需要生成单元测试代码用于验证功能正确性时使用
description: 当需要生成小红书种草文案用于推广产品时使用
```

### 模板 4：执行型技能
**适用场景**：执行特定任务或流程

```yaml
description: 当需要执行 [任务] 以实现 [目标] 时使用
```

**示例**：
```yaml
description: 当需要执行数据库迁移以升级数据结构时使用
description: 当需要部署应用到生产环境时使用
description: 当需要分析日志文件以定位性能瓶颈时使用
```

### 模板 5：综合型技能（组合多个要素）

```yaml
description: 当需要 [动作] [对象]，确保 [标准/要求] 时使用
```

**示例**：
```yaml
description: 当需要编写 TypeScript 代码，确保符合团队命名规范、函数长度限制和错误处理标准时使用
```

---

## 五、description 的常见错误与避坑

### 错误 1：description 太模糊

**❌ 坏例子**：
```yaml
description: 这是一个写作技能
description: 代码相关工具
description: 帮助我完成工作
```

**问题**：Claude 无法判断何时使用

**✅ 改进方案**：
```yaml
description: 当需要编写符合微信公众号风格的技术文章时使用
description: 当需要编写或重构 TypeScript 代码时使用
description: 当需要处理日常开发任务如代码检查、测试生成、文档编写时使用
```

### 错误 2：缺少关键场景信息

**❌ 坏例子**：
```yaml
description: PRD 生成器
```

**问题**：什么情况下生成 PRD？从什么材料生成？

**✅ 改进方案**：
```yaml
description: 当需要从会议记录、需求讨论、用户反馈中提取并整理成产品需求文档时使用
```

### 错误 3：使用过于专业的术语

**❌ 坏例子**：
```yaml
description: 实现基于 SOLID 原则的 DDD 架构重构
```

**问题**：术语堆砌，Claude 可能理解偏差

**✅ 改进方案**：
```yaml
description: 当需要重构代码以提高可维护性、降低耦合度、遵循单一职责原则时使用
```

### 错误 4：description 和内容不符

**❌ 坏例子**：
```yaml
---
name: prd-generator
description: 自动生成产品需求文档
---

# 代码审查技能

本文档说明如何进行代码审查...
```

**问题**：description 说生成 PRD，内容却是代码审查，会混淆 Claude

**✅ 改进方案**：
```yaml
---
name: code-reviewer
description: 当需要对代码进行安全性、性能、可维护性审查时使用
---

# 代码审查技能

本文档说明如何进行代码审查...
```

### 错误 5：一次塞入多个不相关的能力

**❌ 坏例子**：
```yaml
description: 当需要写代码、生成文档、创建测试、部署应用时使用
```

**问题**：一个技能做太多事，难以维护，触发也不精确

**✅ 改进方案**：
拆分成多个技能：
```yaml
# skill 1
name: typescript-writer
description: 当需要编写符合团队规范的 TypeScript 代码时使用

# skill 2
name: api-doc-generator
description: 当需要从代码注释生成 API 文档时使用

# skill 3
name: test-generator
description: 当需要为函数生成单元测试时使用
```

---

## 六、SKILL.md 主体结构：让 Claude 正确执行

写好 description 只是第一步。SKILL.md 的主体内容同样重要。

### 6.1 标准结构

```markdown
---
name: your-skill
description: 何时使用此技能
---

# 技能名称

## Getting Started
[快速开始的基本步骤]

## Core Workflows
[核心工作流程，分步骤说明]

## Extended Capabilities
- **高级功能 1**：详见 [references/advanced-1.md](references/advanced-1.md)
- **高级功能 2**：详见 [references/advanced-2.md](references/advanced-2.md)

## Examples
[具体的输入输出示例]
```

### 6.2 Getting Started 部分

**目的**：Claude 需要知道第一步做什么

**❌ 坏例子**：
```markdown
## Getting Started
欢迎使用本技能。
```

**✅ 好例子**：
```markdown
## Getting Started

当用户请求生成 PRD 时：

1. **确认输入材料**：检查用户是否提供了会议记录、需求讨论或其他原始材料
2. **询问缺失信息**：如果缺少关键信息（如目标用户、核心功能），主动询问
3. **加载 PRD 模板**：详见 [PRD_TEMPLATE.md](references/PRD_TEMPLATE.md)
4. **按照模板生成**：将输入材料填充到模板中，确保逻辑连贯
```

### 6.3 Core Workflows 部分

**目的**：把步骤说清楚，让 Claude 照着做

**写作技巧**：
- ✅ 用**编号列表**，Claude 会按顺序执行
- ✅ 每个步骤**具体明确**
- ✅ 包含**决策逻辑**（如果...则...）

**❌ 坏例子**：
```markdown
## Core Workflows
- 分析需求
- 生成文档
- 检查质量
```

**✅ 好例子**：
```markdown
## Core Workflows

### 步骤 1：分析输入材料

1. **识别材料类型**：
   - 如果是会议记录 → 提取决策项、待办事项、负责人
   - 如果是需求讨论 → 提取用户痛点、解决方案、功能清单
   - 如果是用户反馈 → 提取常见问题、改进建议、新功能需求

2. **检查完整性**：
   - 是否明确了目标用户？（如没有，询问用户）
   - 是否定义了核心功能？（如没有，基于材料推断或询问）
   - 是否有优先级排序？（如没有，按照影响范围和紧急程度排序）

### 步骤 2：生成 PRD

详见 [PRD 生成流程](references/prd-workflow.md)

### 步骤 3：质量检查

使用以下清单检查生成的 PRD：
- [ ] 需求背景清晰
- [ ] 目标用户明确
- [ ] 功能列表完整
- [ ] 优先级合理
- [ ] 验收标准可测试
```

### 6.4 Extended Capabilities 部分

**目的**：实现渐进式披露，高级内容独立成文件

**❌ 坏做法**：把所有内容都塞进 SKILL.md

```markdown
## Core Workflows

[2000 行详细说明...]

## 高级功能 1
[500 行...]

## 高级功能 2
[500 行...]
```

**问题**：文件太大，Claude 加载慢，上下文占用高

**✅ 好做法**：
```markdown
## Core Workflows

[核心流程，500 行内]

## Extended Capabilities

### 高级场景处理
对于复杂的 PRD 生成场景（如大型项目、跨部门协作），详见：
[高级 PRD 生成指南](references/advanced-prd.md)

### 多语言支持
如需生成英文 PRD，使用 [英文模板](references/templates/prd-template-en.md)

### 导出格式
默认输出 Markdown，可导出为：
- PDF：使用 [导出脚本](scripts/export-pdf.sh)
- Word：使用 [导出脚本](scripts/export-docx.sh)
```

### 6.5 Examples 部分【重要】

没有 Examples，Claude 只能猜你想要什么。有了 Examples，结果就明确了。

**❌ 坏例子**：
```markdown
## Examples
示例见官方文档。
```

**✅ 好例子**：
```markdown
## Examples

### 示例 1：从会议记录生成 PRD

**用户输入**：
```
会议记录：用户反馈登录流程复杂，建议简化为手机号+验证码。
产品经理同意，要求下月上线。
```

**预期输出**：
```markdown
# 产品需求文档：登录流程优化

## 需求背景
当前登录流程需要用户名+密码，新用户注册率低（数据：Q1 注册率 15%，低于行业平均 25%）。

## 目标用户
- 新用户（注册转化率低）
- 老用户（忘记密码频繁）

## 核心功能
- 功能 1：手机号+验证码登录
- 功能 2：微信/支付宝一键登录
- 功能 3：保留原有登录方式（过渡期）

## 优先级
- P0（下月上线）：手机号+验证码登录
- P1（Q3）：第三方登录
- P2（Q4）：下线原登录方式

## 验收标准
- 新用户注册率提升至 20%+
- 登录成功率 > 95%
- 平均登录时长 < 10 秒
```

### 示例 2：从需求讨论生成 PRD

**用户输入**：
```
需求讨论：
- 用户：想要批量导出数据
- 技术：可以用 CSV 或 Excel
- 用户：Excel 更好，因为要二次编辑
- 决策：先做 Excel 导出，后续考虑 CSV
```

**预期输出**：
[...]
```

**Examples 的写作要点**：
- ✅ **真实输入**：模拟用户真实的表达方式
- ✅ **完整输出**：展示 Claude 应该生成的完整内容
- ✅ **多个场景**：至少 2-3 个不同场景的例子
- ✅ **标注关键点**：在例子中用注释说明为什么这样输出

---

## 七、完整 SKILL.md 模板

完整模板在这里：

```yaml
---
name: your-skill-name
description: 当需要 [明确场景] 时使用，实现 [核心价值]
---

# 技能名称（可选，与 name 可不同）

## Getting Started

当 [触发条件] 时：

1. **第一步**：[具体做什么]
2. **第二步**：[具体做什么]
3. **第三步**：[具体做什么]

## Core Workflows

### 步骤 1：[步骤名称]

[详细说明]

**决策逻辑**：
- 如果 [条件 A] → [行动 A]
- 如果 [条件 B] → [行动 B]

**检查清单**：
- [ ] 检查项 1
- [ ] 检查项 2

### 步骤 2：[步骤名称]

[详细说明]

### 步骤 3：[步骤名称]

[详细说明]

## Extended Capabilities

### 高级功能 1
对于 [复杂场景]，详见：
[详细文档](references/advanced-feature-1.md)

### 高级功能 2
对于 [复杂场景]，详见：
[详细文档](references/advanced-feature-2.md)

## Examples

### 示例 1：[场景名称]

**用户输入**：
```
[真实用户输入]
```

**预期输出**：
```markdown
[完整输出示例]
```

**关键说明**：
- 为什么这样输出：[说明]
- 注意事项：[说明]

### 示例 2：[场景名称]

[同上结构]
```

---

## 八、写作 Checklist

创建或修改 SKILL.md 前，用这个清单检查一遍：

### Frontmatter 检查
- [ ] `name` 使用 kebab-case（小写+连字符）
- [ ] `name` 简短但能说明用途
- [ ] `description` 明确了"何时使用"
- [ ] `description` 包含了触发关键词
- [ ] `description` 避免了模糊词汇（帮助、辅助、优化）
- [ ] `description` 控制在 1-2 句话
- [ ] `description` 与实际内容相符

### 内容结构检查
- [ ] 包含 `Getting Started` 部分
- [ ] 包含 `Core Workflows` 部分
- [ ] 包含 `Examples` 部分（强烈推荐）
- [ ] 文件总长度不超过 500 行（考虑拆分）
- [ ] 高级内容放到 `references/` 目录

### Examples 检查
- [ ] 至少 2-3 个示例
- [ ] 每个示例包含真实用户输入
- [ ] 每个示例包含完整输出
- [ ] 覆盖了主要使用场景

### 触发测试
- [ ] 用 3-5 个不同场景的 prompt 测试
- [ ] Claude 能正确识别何时使用技能
- [ ] Claude 生成的输出符合预期

---

## 九、实战案例：从坏到好的改进

看个真实的改进案例。

### 原始版本（❌ 坏）

```yaml
---
name: blog-helper
description: 帮助写博客文章
---

# 博客写作助手

## Getting Started
欢迎使用博客写作助手。

## Core Workflows
- 分析主题
- 生成大纲
- 写文章

## Examples
暂无
```

**问题诊断**：
1. `description` 太模糊："帮助写博客文章"
2. `name` 不明确：`blog-helper` 没说明是什么类型的博客
3. `Getting Started` 没用
4. `Core Workflows` 太简略
5. 缺少 `Examples`

### 改进版本（✅ 好）

```yaml
---
name: wechat-tech-article-writer
description: 当需要编写微信公众号技术文章时使用，确保符合 1500-3000 字、实践导向、真实案例的风格要求
---

# 微信公众号技术文章写作助手

## Getting Started

当用户请求编写或修改公众号技术文章时：

1. **确认主题**：明确文章要讲解的技术或工具
2. **搜索知识库**：检查是否有相关的个人素材或历史文章
3. **生成选题方案**：提供 3-4 个选题角度供用户选择
4. **等待确认**：用户确认选题后才开始写作

## Core Workflows

### 步骤 1：信息调研

**触发条件**：涉及新技术、新工具（2024-2025 年）

**操作**：
1. 搜索官方文档
2. 查看科技媒体报道（TechCrunch、The Verge）
3. 查看社区讨论（Reddit、Hacker News）
4. 保存到知识库

**决策逻辑**：
- 如果是成熟技术 → 跳过调研
- 如果是新技术 → 必须调研

### 步骤 2：选题讨论

**重要性**：避免方向错误，必须先讨论选题！

**操作**：
1. 提供 3-4 个选题方案
2. 每个方案包含：核心角度、工作量评估、优劣势
3. 等待用户选择

**禁止**：直接开始写作

### 步骤 3：学习风格

**操作**：
1. 阅读 `_writing_reference/` 中的风格指南
2. 阅读 2-3 篇历史优质文章
3. 提取风格特征：
   - 开头方式（故事/数据/金句）
   - 结构偏好（小标题风格）
   - 语言特征（句式、节奏）

### 步骤 4：搜索个人素材库

**目的**：用真实经历降低 AI 味

**操作**：
1. 在 `_personal_materials/` 中搜索相关关键词
2. 提取真实经历、观点、案例
3. 标记可用的素材

**使用场景**：
- 文章开头：用真实经历引入
- 观点支撑：用真实评价增强可信度
- 案例展示：用真实项目案例

### 步骤 5：创作初稿

**写作原则**：
- 基于真实数据（调研 + 测试）
- 保持"实践+落地"调性
- 加入具体案例（真实，不编造）
- 自然融入个人经验
- 保持风格一致
- 注入微幽默（每 200 字至少 1 个）

**文件保存**：
- 保存到 `_drafts/` 文件夹
- 文件名：`YYYY-MM-DD-主题-draft-v1.md`

### 步骤 6：三遍审校

**第一遍：内容审校**
- 检查事实准确性
- 检查逻辑清晰性
- 检查段落迷你论点（每段都应有明确论点）

**第二遍：风格审校（降 AI 味）**
- 删除套话（"在当今时代"、"综上所述"）
- 拆解 AI 句式（"不是…而是…"）
- 替换书面词汇（"显著提升" → 具体数字）
- 改成口语化
- 加入真实细节
- 加入个人态度

**第三遍：细节打磨**
- 句子节奏变化（短句+中句+长句交替）
- 段落长度（手机屏幕 3-5 行）
- 标点自然（多用句号）
- 多巴胺密度（每段至少 1 个有意思的点）

### 步骤 7：标题拟定

**操作**：提供两轮标题方案

**第一轮：爆款标题（基于 7 要素）**
- 金钱、数字
- 异常、悬念
- 捷径、快速
- ...

**第二轮：自然风格（无套路版）**
- 故事感+洞察
- 身份转变
- 引用金句
- ...

## Extended Capabilities

### 高级场景
对于需要真实测试的文章，详见：
[协作文档模板](../_templates/协作文档模板.md)

### 配图生成
对于需要配图的文章，详见：
[配图指南](../_templates/配图指南.md)

## Examples

### 示例 1：编写工具介绍文章

**用户输入**：
```
帮我写一篇介绍 Claude Code Skills 的公众号文章
```

**Claude 响应**：
```
我来帮你创作这篇关于 Claude Code Skills 的公众号文章。

首先让我搜索一下知识库和个人素材库，看看是否有相关素材...
[搜索过程...]

找到相关素材 3 条：
1. Claude Code Skills 官方文档
2. 个人测试经历（2025-01-10）
3. 相关技术文章 2 篇

现在让我提供几个选题方案：

### 选题 1：Claude Code Skills 入门：什么是 Skills，为什么你需要它
核心角度：从痛点切入（重复输入指令），介绍 Skills 的价值
工作量：⭐⭐⭐
优势：受众广，适合新手
劣势：话题相对基础

### 选题 2：5 分钟上手 Claude Skills：从零到第一个技能
核心角度：手把手教程，快速体验
工作量：⭐⭐⭐⭐
优势：实践性强，有即时反馈
劣势：需要准备测试环境

### 选题 3：渐进式披露：Claude Skills 的核心秘密
核心角度：技术原理深度剖析
工作量：⭐⭐⭐⭐⭐
优势：技术深度，适合进阶读者
劣势：受众较窄

### 选题 4：实战案例：用 5 分钟完成半天的工作量
核心角度：真实案例展示效率提升
工作量：⭐⭐⭐
优势：说服力强，有数据支撑
劣势：需要真实案例支撑

请问你想选择哪个选题？或者需要我调整方向？
```

**关键说明**：
- 为什么这样响应：先调研，再选题，避免方向错误
- 注意事项：绝不直接写文章，必须先讨论选题

### 示例 2：修改已有文章

**用户输入**：
```
这篇文章 AI 味太重了，帮我改一下
[附上文章内容]
```

**Claude 响应**：
```
我来帮你降低这篇文章的 AI 味。让我先分析一下问题...

**AI 味诊断**：
1. 套话：出现"在当今时代"、"值得注意的是"、"综上所述"
2. AI 句式：连续使用"不是…而是…"句式
3. 书面词汇："显著提升"、"充分利用"、"进行操作"
4. 缺少真实细节：没有具体数字、案例
5. 缺少个人态度：过于中立客观

**三遍审校计划**：
1. 第一遍：检查逻辑和事实
2. 第二遍：降 AI 味（删除套话、改成口语化、加入真实细节）
3. 第三遍：打磨节奏（句子长度变化、段落长度、标点）

现在开始修改...
[详细修改过程...]

修改完成。主要改动：
- 删除了 12 处套话
- 改写了 8 个 AI 句式
- 加入了 5 个真实细节（具体数字、案例）
- 调整了句子节奏（增加了短句和长句对比）
- 版本号：v2

请查看修改后的文章，如果需要进一步调整，请告诉我具体需求。
```

**关键说明**：
- 为什么这样响应：先诊断问题，再系统化修改
- 注意事项：每次修改都创建新版本，便于追踪
```

**改进效果**：
- ✅ `description` 明确了触发条件（编写公众号技术文章）
- ✅ `name` 具体说明了技能用途
- ✅ `Core Workflows` 详细且可执行
- ✅ 包含了完整的 `Examples` 展示预期行为
- ✅ 实现了渐进式披露（高级内容放到 Extended Capabilities）

---

## 十、总结与核心要点

### 核心要点回顾

1. **description 是技能成功的关键**：
   - 决定了技能是否能被 Claude 自动触发
   - 应该明确"何时使用"、"用来做什么"
   - 包含触发关键词，避免模糊词汇

2. **好的 description 特征**：
   - ✅ 明确场景：当需要 XXX 时使用
   - ✅ 具体动作：生成、检查、转换、执行
   - ✅ 关键词：包含 Claude 能识别的触发词
   - ✅ 简洁：1-2 句话讲清楚
   - ✅ 准确：与实际内容相符

3. **SKILL.md 主体结构**：
   - `Getting Started`：快速开始的第一步
   - `Core Workflows`：详细的执行步骤（含决策逻辑）
   - `Extended Capabilities`：高级内容独立文件（渐进式披露）
   - `Examples`：展示预期输入输出（非常重要！）

4. **常见错误**：
   - ❌ description 太模糊
   - ❌ 缺少 Examples
   - ❌ 内容太长（超过 500 行）
   - ❌ 一个技能做太多事
   - ❌ description 与内容不符

5. **写作 Checklist**：
   - 用清单检查 Frontmatter
   - 用清单检查内容结构
   - 用清单检查 Examples
   - 用真实场景测试触发效果

### 下篇预告

下一篇（第 6 篇），我们将深入探讨：

**《高级模式：让技能更强大的组织方式》**

将讲解：
- 渐进式披露模式的最佳实践
- 工作流模式（Workflow Pattern）
- 输出模式（Output Pattern）
- 示例模式（Example Pattern）
- 如何组织复杂的技能系统

敬请期待！

---

## 参考文档

### 官方资源

- **Agent Skills 官方文档**（中文）：https://platform.claude.com/docs/zh-CN/agents-and-tools/agent-skills/overview
- **GitHub 官方仓库**：https://github.com/anthropics/skills
  - 官方技能集合和示例
  - 技能模板
  - 完整规范文档

### 优质教程

- **《Claude Skills 终极指南：从新手到精通（附实战案例分析）》** - 火山引擎
  - 为什么需要 Skills
  - Skills vs 斜杠命令 vs MCP
  - 渐进式披露机制
  - 实战案例：自动生成 PRD

- **《Agent Skills 最佳实践 - Claude 中文》**
  - 清晰的描述编写
  - 保持功能专一性
  - 版本管理与安全考虑

- **《Claude Skills 入门指南：概念、结构与最佳实践》**
  - SKILL.md 配置模板
  - Frontmatter 元数据详解
  - 最佳实践指南

### 深度解析

- **《Claude Skills 架构拆解：渐进披露、运行时与安全沙箱》** - Claudecn.com
  - 核心机制：渐进式披露（Progressive Disclosure）
  - 三级加载系统详解
  - 运行时与安全沙箱机制

- **《终于有人把 Claude Skills 官方教程讲清楚了（附完整实践）》** - 知乎专栏
  - 基本概念与设计原则
  - 技能文件结构详解
  - 六步创建流程
  - 高级模式与技巧

### 技能集合

- **《Awesome Claude Skills》** - Jimmy Song
  - 文档处理类
  - 开发辅助类
  - 数据分析类
  - 创意媒体类

- **《Claude 官方开源 16 个技能库，老金帮你挑出 5 个必装神器》** - 阿里云
  - 文档处理技能
  - 创意开发技能
  - 测试相关技能

### 系列文章

本系列其他文章：
1. [Claude Code Skills 入门：什么是 Skills，为什么你需要它](../_published/claude-code-skills-01-what-is-skills.md)
2. [5 分钟上手 Claude Skills：从零到第一个技能](../_published/claude-code-skills-02-first-skill.md)
3. [Skills vs 斜杠命令 vs MCP：你应该用哪个？](../_published/claude-code-skills-03-comparison.md)
4. [渐进式披露：Claude Skills 的核心秘密](../_published/claude-code-skills-04-progressive-disclosure.md)

---

> 本文是「Claude Code Skills 教程系列」的第 5 篇。
>
> **系列目录**：
> 1. [Claude Code Skills 入门：什么是 Skills，为什么你需要它](../_published/claude-code-skills-01-what-is-skills.md)
> 2. [5 分钟上手 Claude Skills：从零到第一个技能](../_published/claude-code-skills-02-first-skill.md)
> 3. [Skills vs 斜杠命令 vs MCP：你应该用哪个？](../_published/claude-code-skills-03-comparison.md)
> 4. [渐进式披露：Claude Skills 的核心秘密](../_published/claude-code-skills-04-progressive-disclosure.md)
> 5. **SKILL.md 编写指南：写好技能描述是成功的一半**（本文）
> 6. [高级模式：让技能更强大的组织方式](../_published/claude-code-skills-06-advanced-patterns.md)（待发布）
>
> **素材库**：[Claude-Code-Skills教程素材库.md](../_personal_materials/Claude-Code-Skills教程素材库.md)
>
> 有问题或建议？欢迎在评论区留言，或在公众号后台与我交流。

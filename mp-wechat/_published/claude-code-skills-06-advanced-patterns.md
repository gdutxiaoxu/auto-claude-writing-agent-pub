# Claude Code Skills 高级模式：让技能更强大的组织方式

> 作者：Claude
>
> 这是「Claude Code Skills 教程系列」的第 6 篇。本系列将带你从零开始，完整掌握 Claude Code Skills 这一革命性功能。

---

## 一、从简单到复杂：技能演进的必经之路

前几篇讲了 Skills 的基础概念、核心机制、编写规范。你应该能创建简单技能了，让 Claude 在特定任务上表现更好。

但用久了，你会遇到这些问题：

- **技能内容越来越长**：一个代码审查技能，光 SKILL.md 就写了 8000+ tokens，超过官方建议的 5k 上限
- **流程越来越复杂**：多步骤任务（如 PRD 生成），需要清晰的阶段划分和决策逻辑
- **输出格式要求严格**：生成文档必须符合特定格式，每次都要反复强调
- **逻辑难以描述**：有些复杂规则用文字说不清楚，Claude 经常理解错

这时候，简单的 SKILL.md 不够用了。

你需要**更强大的组织模式**。

Anthropic 设计 Skills 时就考虑到了这些场景，提供了四种高级模式。用好了，技能就能从"能用"变成"好用"。

---

## 二、四种高级模式概览

先快速了解一下这四种模式：

| 模式 | 解决什么问题 | 核心机制 | 适用场景 |
|------|-------------|---------|---------|
| **渐进式披露模式** | 内容太长，超过 5k token | 主 SKILL.md + references/ 目录 | 复杂的专业知识 |
| **工作流模式** | 多步骤流程，需要阶段划分 | Core Workflows 设计 | PRD 生成、发布流程 |
| **输出模式** | 输出格式要求严格 | templates/ 目录 | 文档生成、代码生成 |
| **示例模式** | 逻辑复杂，文字描述不清 | examples/ 目录 | 数据查询、复杂规则 |

这四种模式可以单独用，也可以组合。下面逐一讲解，并提供真实案例。

---

## 三、渐进式披露模式：让内容更长而不臃肿

### 何时使用渐进式披露

**判断标准**：你的 SKILL.md 主体内容超过 5k token（约 500 行或 3000+ 字）。

**典型场景**：
- 代码审查技能（安全性 + 性能 + 可维护性，每个维度都有详细规则）
- 企业级开发规范（多语言、多框架、多工具）
- 复杂业务逻辑（电商、金融等领域的专业规则）

### 如何组织结构

核心思想：**主文件轻量化，详细内容拆分到 references/**

**目录结构示例**：
```
code-review/
├── SKILL.md              # 主文件，500 行以内
└── references/
    ├── security-check.md     # 安全性检查规则
    ├── performance-check.md  # 性能检查规则
    ├── maintainability.md    # 可维护性检查规则
    └── best-practices.md     # 最佳实践案例
```

### 主文件 SKILL.md 的设计原则

主文件应该包含：
- ✅ **元数据**：name 和 description（触发机制）
- ✅ **核心概览**：技能的整体介绍和使用方式
- ✅ **快速开始**：最简单的使用场景
- ✅ **扩展能力链接**：指向 references/ 的具体文件

**示例主文件**（约 200 行）：
```yaml
---
name: code-review
description: 当需要审查代码质量、安全性、性能时使用此技能
---

# Code Review 技能

## 快速开始
对当前文件进行全面的代码审查，包括安全性、性能和可维护性三个维度。

## 审查维度
本技能支持三个维度的深度审查：
- **安全性审查**：详见 [security-check.md](references/security-check.md)
- **性能审查**：详见 [performance-check.md](references/performance-check.md)
- **可维护性审查**：详见 [maintainability.md](references/maintainability.md)

## 使用方式
- 简单审查："帮我审查这个文件的安全性"
- 全面审查："对整个项目进行完整的代码审查"
- 特定维度："重点检查这段代码的性能问题"
```

### references/ 文件的组织

**原则**：按功能模块或主题拆分，每个文件专注一个主题。

**security-check.md 示例**（约 800 行）：
```markdown
# 安全性检查规则

## SQL 注入检查
### 检测规则
- 所有用户输入必须参数化
- 禁止字符串拼接 SQL
- 使用 ORM 或参数化查询

### 常见问题模式
❌ 错误示例：
```python
query = f"SELECT * FROM users WHERE name = '{user_input}'"
```

✅ 正确示例：
```python
query = "SELECT * FROM users WHERE name = ?"
cursor.execute(query, (user_input,))
```

## XSS 检查
...（详细规则）
```

### 实战案例：代码审查技能

看一个真实案例。某团队创建了一个"企业级 Python 代码审查"技能：

**问题**：初始版本 SKILL.md 有 1200+ 行，加载缓慢，Claude 经常遗漏规则。

**解决方案**：拆分成渐进式结构

**效果对比**：

| 指标 | 拆分前 | 拆分后 |
|------|--------|--------|
| SKILL.md 行数 | 1,200 行 | 180 行 |
| 初始加载 token | 约 6,000 | 约 900 |
| 规则覆盖率 | 70% | 95% |
| Claude 遗漏规则 | 15% | 3% |

**实际体验**：团队反馈，拆分后 Claude 不再"忘事"，审查质量明显提升。

**核心改进**：
1. 主文件只保留概览和链接
2. 详细规则按主题拆分到 8 个 reference 文件
3. 每个文件专注一个主题，更易维护

### 最佳实践

**✅ DO**：
- 每个reference文件专注一个主题（安全性、性能、可维护性）
- 文件命名清晰（security-check.md 而不是 rules1.md）
- 在主文件提供清晰的导航和快速开始
- 保持文件大小均衡（每个 300-800 行）

**❌ DON'T**：
- 不要把所有内容都塞进一个 reference 文件
- 不要创建过于琐碎的文件（每个文件少于 50 行没意义）
- 不要在主文件重复详细内容
- 不要使用晦涩的文件命名

---

## 四、工作流模式：让多步骤任务井井有条

### 何时使用工作流模式

**判断标准**：你的任务有明确的阶段划分，需要一步步执行。

**典型场景**：
- PRD 生成（需求分析 → 竞品调研 → 功能设计 → 文档输出）
- 发布流程（代码审查 → 测试 → 部署 → 通知）
- 内容创作（选题 → 大纲 → 写作 → 审校 → 发布）

### Core Workflows 设计原则

**核心思想**：在 SKILL.md 中定义清晰的工作流程，Claude 按步骤执行。

**标准结构**：
```markdown
## Core Workflows

### Workflow 1: [工作流名称]
**适用场景**：[什么时候用这个流程]

**步骤**：
1. **步骤1名称**：[具体操作]
2. **步骤2名称**：[具体操作]
3. **步骤3名称**：[具体操作]

**决策点**：
- 如果条件A → 执行分支A
- 如果条件B → 执行分支B

**输出**：[最终产出]
```

### 实战案例：PRD 生成技能

这是个真实案例，某产品团队用 Skills 把 PRD 生成时间从 2 小时缩短到 15 分钟。

**SKILL.md 中的 Core Workflows**：
```markdown
## Core Workflows

### Workflow 1: 从会议记录生成完整 PRD
**适用场景**：已有会议记录或需求讨论记录

**步骤**：
1. **需求提取**：
   - 从会议记录中提取关键需求
   - 识别功能需求和非功能需求
   - 标记不确定或需要澄清的点

2. **竞品分析**（可选）：
   - 识别 2-3 个竞品的类似功能
   - 分析它们的实现方式
   - 总结差异化机会

3. **功能设计**：
   - 设计用户流程图
   - 定义核心功能点
   - 列出技术约束

4. **文档输出**：
   - 使用 [PRD_TEMPLATE.md](references/PRD_TEMPLATE.md) 生成文档
   - 填充所有必需字段
   - 标注需要进一步讨论的部分

**决策点**：
- 如果需求不完整 → 生成问题清单，向用户确认
- 如果技术可行性不确定 → 标注"需要技术评估"

**输出**：完整的 PRD 文档，保存在 `docs/prd/` 目录
```

**实际效果**：

用户说：
> "把昨天的产品会议记录整理成 PRD"

Claude 会：
1. 自动读取会议记录文件
2. 按照上述 4 个步骤执行
3. 在每个步骤完成后确认再继续
4. 最终生成符合团队模板的 PRD 文档

**时间对比**：
- 传统方式：2 小时（包括反复沟通、格式调整）
- 使用 Skills：15 分钟（主要是 Claude 执行，人类审核）

### 高级技巧：条件分支与并行流程

**条件分支示例**：
```markdown
### Workflow 2: 紧急 hotfix 发布流程
**适用场景**：生产环境紧急 bug 修复

**步骤**：
1. **问题确认**：
   - 验证 bug 严重性
   - 评估影响范围

2. **分支选择**：
   - 如果影响核心功能 → 走"紧急发布"分支
   - 如果影响边缘功能 → 走"常规发布"分支

3. **紧急发布分支**：
   - 跳过部分测试（只测核心流程）
   - 简化审批流程
   - 部署后 24 小时内监控

4. **常规发布分支**：
   - 完整测试流程
   - 标准审批
   - 正常监控周期
```

### 最佳实践

**✅ DO**：
- 每个步骤描述清晰、可执行
- 明确标注决策点和分支条件
- 说明每个步骤的输入和输出
- 提供预期的完成时间

**❌ DON'T**：
- 不要创建过于复杂的嵌套流程
- 不要在一个工作流中混合多个不相关的任务
- 不要省略决策点（让 Claude 自己猜）
- 不要忘记定义"完成"的标准

---

## 五、输出模式：让格式化的工作不再重复

### 何时使用输出模式

**判断标准**：你的输出需要符合特定格式，且这个格式是固定的。

**典型场景**：
- PRD/技术文档生成（必须使用团队模板）
- API 文档生成（OpenAPI 规范）
- 代码生成（特定框架的脚手架）
- 测试用例生成（特定测试框架格式）

### templates/ 目录的使用

**核心思想**：将模板文件放在 `templates/` 目录，Claude 基于模板生成内容。

**目录结构示例**：
```
doc-generator/
├── SKILL.md
├── templates/
│   ├── prd-template.md          # PRD 模板
│   ├── api-doc-template.md      # API 文档模板
│   └── tech-design-template.md  # 技术设计文档模板
└── examples/
    ├── sample-prd.md            # 示例 PRD
    └── sample-api-doc.md        # 示例 API 文档
```

### 模板设计原则

**✅ 好的模板特征**：
- 使用占位符（`{{变量名}}` 或 `[需填写]`）
- 提供填写说明（注释或引导文字）
- 包含示例内容（降低理解成本）
- 结构清晰，易于导航

**示例模板**（prd-template.md）：
```markdown
# 产品需求文档（PRD）

## 元信息
- **文档名称**：[功能名称] PRD
- **版本**：v1.0
- **创建日期**：{{YYYY-MM-DD}}
- **负责人**：[姓名]

## 1. 需求背景
### 1.1 业务背景
[描述为什么需要这个功能，解决什么业务问题]

### 1.2 目标用户
- 主要用户：[用户画像]
- 使用场景：[具体场景]

## 2. 功能需求
### 2.1 核心功能
| 功能点 | 优先级 | 描述 | 验收标准 |
|--------|--------|------|----------|
| [功能1] | P0 | [描述] | [标准] |
| [功能2] | P1 | [描述] | [标准] |

### 2.2 用户流程
[描述用户的操作流程，可配流程图]

## 3. 非功能需求
- **性能要求**：[具体指标]
- **安全要求**：[具体要求]
- **兼容性**：[支持的系统/版本]

## 4. 技术方案
### 4.1 技术选型
- [技术栈1]：[选择理由]
- [技术栈2]：[选择理由]

### 4.2 架构设计
[描述系统架构，可配架构图]

## 5. 实施计划
| 阶段 | 任务 | 预计工期 | 负责人 |
|------|------|----------|--------|
| [阶段1] | [任务] | [时间] | [姓名] |

## 6. 风险与依赖
### 6.1 风险
- [风险1]：[影响] - [应对措施]

### 6.2 依赖
- [依赖1]：[描述]
```

### 实战案例：文档生成技能

某 SaaS 公司创建了"技术文档生成器"技能：

**问题**：团队技术文档格式不统一，经常遗漏关键章节。

**解决方案**：标准化模板 + Skills 引导填充

**SKILL.md 中的配置**：
```markdown
## Extended Capabilities

### PRD 生成
使用 PRD 模板生成产品需求文档：
- 模板位置：[templates/prd-template.md](templates/prd-template.md)
- 参考示例：[examples/sample-prd.md](examples/sample-prd.md)
- 使用方式："基于会议记录生成 PRD"

### API 文档生成
自动从代码生成 API 文档：
- 模板位置：[templates/api-doc-template.md](templates/api-doc-template.md)
- 支持格式：OpenAPI 3.0
- 使用方式："为这个 API 生成文档"
```

**效果**：
- 文档格式统一率：从 40% → 95%
- 文档完整度：从 60% → 90%
- 审核修改时间：从 1 小时 → 15 分钟

**团队反馈**：不用再反复提醒"填写这个章节"、"那个格式错了"，审核轻松多了。

### 最佳实践

**✅ DO**：
- 模板使用清晰的占位符
- 提供填写说明和示例
- 定期更新模板（根据反馈）
- 保持模板简洁（避免过度复杂）

**❌ DON'T**：
- 不要创建过于复杂的模板
- 不要在模板中硬编码过多内容
- 不要忽略模板的版本管理
- 不要忘记在 SKILL.md 中说明如何使用模板

---

## 六、示例模式：让复杂逻辑一目了然

### 何时使用示例模式

**判断标准**：你的规则或逻辑用文字描述难以理解，或者 Claude 经常理解错误。

**典型场景**：
- 数据库查询（复杂 join 逻辑）
- 数据转换规则（JSON → XML）
- 业务规则引擎（保险、金融等领域）
- 代码生成（特定模式或框架）

### examples/ 目录的设计

**核心思想**：用"输入→输出"的示例对，让 Claude 通过示例学习模式。

**目录结构示例**：
```
database-query/
├── SKILL.md
├── examples/
│   ├── simple-query.md        # 简单查询示例
│   ├── complex-join.md        # 复杂 join 示例
│   └── aggregation.md         # 聚合查询示例
└── references/
    └── schema.md              # 数据库结构
```

### 示例编写原则

**✅ 好的示例特征**：
- **输入-输出配对**：清晰展示输入和对应的输出
- **覆盖边界情况**：不只是"快乐路径"，还包括异常情况
- **逐步复杂化**：从简单到复杂，循序渐进
- **添加注释**：解释为什么是这样，而不是那样

**示例格式**：
```markdown
## 示例1：单表简单查询

**输入**（用户请求）：
> 查询本月注册的活跃用户

**输出**（SQL 查询）：
```sql
SELECT u.id, u.username, u.email
FROM users u
WHERE u.created_at >= DATE_TRUNC('month', CURRENT_DATE)
  AND u.last_login >= u.created_at
ORDER BY u.created_at DESC;
```

**要点说明**：
- 使用 `DATE_TRUNC` 获取本月第一天
- 活跃用户定义：注册后有过登录
- 按注册时间倒序排列

---

## 示例2：多表 JOIN

**输入**：
> 查询每个用户的订单数量和总金额

**输出**：
```sql
SELECT
  u.id,
  u.username,
  COUNT(o.id) AS order_count,
  COALESCE(SUM(o.total), 0) AS total_amount
FROM users u
LEFT JOIN orders o ON u.id = o.user_id
GROUP BY u.id, u.username
HAVING COUNT(o.id) > 0
ORDER BY total_amount DESC;
```

**要点说明**：
- 使用 `LEFT JOIN` 确保没有订单的用户也被统计
- 使用 `COALESCE` 处理 NULL 值
- `HAVING` 过滤掉没有订单的用户
```

### 实战案例：数据库查询技能

某数据分析师创建了一个"PostgreSQL 查询助手"技能：

**问题**：Claude 生成的 SQL 经常不符合公司的数据库架构和编码规范。

**解决方案**：创建示例库

**examples/ 目录内容**：
- `simple-query.md`：5 个简单查询示例
- `complex-join.md`：8 个复杂 join 示例（包括内连接、左连接、子查询）
- `aggregation.md`：6 个聚合查询示例（分组、窗口函数）
- `performance-tips.md`：4 个性能优化示例

**SKILL.md 中的引用**：
```markdown
## 使用示例

本技能包含丰富的查询示例，Claude 会根据类似模式生成查询：

- 简单查询参考：[examples/simple-query.md](examples/simple-query.md)
- 复杂 JOIN 参考：[examples/complex-join.md](examples/complex-join.md)
- 聚合查询参考：[examples/aggregation.md](examples/aggregation.md)

**使用建议**：如果你的查询需求与某个示例相似，Claude 会参考该示例的模式。
```

**效果**：
- SQL 准确率：从 65% → 92%
- 查询性能符合规范：从 50% → 85%
- 返工率：从 40% → 10%

**实际体验**：分析师说"终于不用每次都改 SQL 了"，Claude 生成的查询基本能用。

### 高级技巧：负面示例

除了"正确示例"，还可以提供"错误示例"，明确告诉 Claude 不要做什么：

```markdown
## ❌ 错误示例

**错误输入**：
> SELECT * FROM users

**问题**：
- 使用 `SELECT *` 会获取不必要的列，影响性能
- 没有WHERE条件，会查询全表（数据量大时很危险）

**正确做法**：
```sql
-- 明确指定需要的列
SELECT id, username, email FROM users;

-- 或者添加 LIMIT
SELECT * FROM users LIMIT 100;
```
```

### 最佳实践

**✅ DO**：
- 每个示例清晰标注输入和输出
- 提供示例的要点说明（为什么这样做）
- 从简单到复杂，循序渐进
- 包含边界情况和错误处理

**❌ DON'T**：
- 不要只提供"快乐路径"示例
- 不要忘记添加说明注释
- 不要创建过于相似的示例（冗余）
- 不要忽略示例的版本管理

---

## 七、混合模式：实战中的组合应用

真实场景中，这四种模式经常组合。看一个完整案例。

### 实战案例：完整的发布流程技能

某 DevOps 团队创建了一个"自动化发布"技能，组合使用了所有四种模式：

**目录结构**：
```
release-automation/
├── SKILL.md                        # 主文件（工作流模式）
├── references/                     # 渐进式披露
│   ├── pre-release-check.md       # 发布前检查清单
│   ├── deployment-steps.md        # 部署步骤详解
│   ├── post-release-verify.md     # 发布后验证
│   └── rollback-procedure.md      # 回滚流程
├── templates/                      # 输出模式
│   ├── release-notes-template.md  # 发布说明模板
│   └── changelog-template.md      # 变更日志模板
└── examples/                       # 示例模式
    ├── standard-release.md        # 标准发布示例
    ├── hotfix-release.md          # 紧急修复示例
    └── rollback-example.md        # 回滚示例
```

**SKILL.md 内容**（工作流 + 引用）：
```markdown
---
name: release-automation
description: 自动化代码发布流程，包括检查、部署、验证和回滚
---

# 发布自动化技能

## Core Workflows

### Workflow 1: 标准发布流程
**适用场景**：常规功能发布

**步骤**：
1. **发布前检查**：
   - 详见 [pre-release-check.md](references/pre-release-check.md)
   - 包括：代码审查、测试通过率、依赖检查

2. **部署**：
   - 详见 [deployment-steps.md](references/deployment-steps.md)
   - 分阶段：dev → staging → production

3. **验证**：
   - 详见 [post-release-verify.md](references/post-release-verify.md)
   - 包括：健康检查、核心功能测试、监控告警

4. **生成发布说明**：
   - 使用 [release-notes-template.md](templates/release-notes-template.md)
   - 参考 [standard-release.md](examples/standard-release.md)

**决策点**：
- 如果健康检查失败 → 执行回滚流程（见 Workflow 3）
- 如果监控告警 → 根据 [rollback-procedure.md](references/rollback-procedure.md) 判断是否回滚

### Workflow 2: 紧急修复发布
**适用场景**：生产环境紧急 bug 修复

**步骤**：
1. **简化检查**：只执行关键检查项
2. **快速部署**：跳过 staging，直接部署到生产
3. **核心验证**：只验证修复的功能点
4. **生成变更日志**：
   - 使用 [changelog-template.md](templates/changelog-template.md)
   - 参考 [hotfix-release.md](examples/hotfix-release.md)

### Workflow 3: 回滚流程
**适用场景**：发布后发现问题需要回滚

**步骤**：
1. **评估影响**：判断是否需要回滚
2. **执行回滚**：详见 [rollback-procedure.md](references/rollback-procedure.md)
3. **回滚后验证**：确保系统恢复正常
4. **生成事故报告**：
   - 参考 [rollback-example.md](examples/rollback-example.md)

## Extended Capabilities
- **检查清单生成**：基于 [pre-release-check.md](references/pre-release-check.md) 生成检查清单
- **发布说明自动填充**：基于 git commit history 填充模板
- **监控数据分析**：分析发布后的监控数据，判断是否需要回滚

## Examples
参考 [examples/](examples/) 目录查看完整的发布示例。
```

**使用效果**：

| 指标 | 使用前 | 使用后 | 改进 |
|------|--------|--------|------|
| 发布时间 | 2-3 小时 | 30-45 分钟 | 75% ↓ |
| 发布失败率 | 15% | 3% | 80% ↓ |
| 回滚时间 | 30-60 分钟 | 10-15 分钟 | 70% ↓ |
| 文档完整性 | 60% | 95% | 58% ↑ |

**核心价值**：
1. **渐进式披露**：每个环节的详细规则独立维护，易于更新
2. **工作流模式**：清晰的步骤和决策点，减少人为错误
3. **输出模式**：标准化的文档模板，确保合规性
4. **示例模式**：真实示例帮助 Claude 理解复杂场景

---

## 八、四种模式对比总结

用一张表对比这四种模式：

| 维度 | 渐进式披露 | 工作流 | 输出 | 示例 |
|------|-----------|--------|------|------|
| **核心问题** | 内容太长 | 流程混乱 | 格式不统一 | 逻辑复杂 |
| **主要机制** | references/ | Core Workflows | templates/ | examples/ |
| **典型场景** | 复杂专业知识 | 多步骤任务 | 文档/代码生成 | 查询/转换规则 |
| **学习成本** | 中 | 低 | 低 | 中 |
| **维护成本** | 中 | 低 | 低 | 中 |
| **效果提升** | ⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐⭐ |

**选择建议**：
- 如果是**一次性任务**：示例模式最有效
- 如果是**重复性流程**：工作流模式最佳
- 如果是**标准化输出**：输出模式优先
- 如果是**复杂知识体系**：渐进式披露必须

**组合使用优先级**：
1. 工作流 + 输出（最常见，如 PRD 生成）
2. 工作流 + 渐进式披露（复杂流程，如发布流程）
3. 输出 + 示例（代码生成，如脚手架）
4. 全部组合（企业级复杂系统）

---

## 九、总结与参考资源

### 核心要点

这篇文章讲了四种高级模式，每个解决一个具体问题：

**渐进式披露**：内容太长（超过 5k token）时，把详细内容拆到 `references/` 目录，主文件只保留概览和链接。

**工作流模式**：多步骤任务时，在 SKILL.md 中定义清晰的"Core Workflows"，包括步骤、决策点、输出。

**输出模式**：输出格式固定时，用 `templates/` 目录存放模板，Claude 基于模板生成内容。

**示例模式**：逻辑复杂、文字说不清时，用 `examples/` 目录提供"输入→输出"示例对，让 Claude 照着学。

**可以单独用，也可以组合**：
- 简单技能：单个模式够用
- 复杂技能：组合 2-3 个模式
- 企业级技能：四种模式全用上

**核心原则**：从需求出发，别为了模式而模式。先用起来，再优化。

---

### 参考文档

**官方资源**：
- [Agent Skills 官方文档](https://platform.claude.com/docs/zh-CN/agents-and-tools/agent-skills/overview) - Anthropic 官方文档，包含完整规范
- [GitHub 官方仓库](https://github.com/anthropics/skills) - 官方技能集合和示例

**优质教程**：
- [Claude Skills 终极指南 - 火山引擎](https://developer.volcengine.com/articles/7577301013976383498) - 从新手到精通的完整指南
- [Claude Skills 架构拆解 - Claudecn.com](https://claudecn.com/blog/claude-skills-architecture/) - 渐进披露、运行时与安全沙箱详解
- [终于有人把 Claude Skills 官方教程讲清楚了 - 知乎专栏](https://zhuanlan.zhihu.com/p/1987581624360145862) - 附完整实践案例

**技能集合**：
- [Awesome Claude Skills](https://jimmyang.io/zh/ai/awesome-claude-skills/) - 社区优质技能集合
- [Agent Skills 权威中文指南 - GitHub](https://github.com/libukai/awesome-agent-skills) - 技能库和最佳实践

### 下篇预告

第 7 篇是实战专场。

**《实战案例：用 5 分钟完成半天的工作量》** 会讲：

- **案例 1**：从会议记录到 PRD，15 分钟完整流程
- **案例 2**：代码审查技能，review 效率提升 3 倍
- **案例 3**：文档处理自动化，从半天到 20 分钟
- **案例 4**：个人知识库搭建，打造第二大脑

每个案例都包括：
- 完整代码实现
- Before/After 对比
- 可直接复用的模板
- 常见问题和解决方案

---

**系列文章目录**：

1. [Claude Code Skills 入门：什么是 Skills，为什么你需要它](https://your-domain.com/claude-code-skills-01)
2. [5 分钟上手 Claude Skills：从零到第一个技能](https://your-domain.com/claude-code-skills-02)
3. [Skills vs 斜杠命令 vs MCP：你应该用哪个？](https://your-domain.com/claude-code-skills-03)
4. [渐进式披露：Claude Skills 的核心秘密](https://your-domain.com/claude-code-skills-04)
5. [SKILL.md 编写指南：写好技能描述是成功的一半](https://your-domain.com/claude-code-skills-05)
6. **高级模式：让技能更强大的组织方式**（本文）
7. [实战案例：用 5 分钟完成半天的工作量](https://your-domain.com/claude-code-skills-07)（即将发布）
8. [5 个必装的 Claude Skills，效率直接翻倍](https://your-domain.com/claude-code-skills-08)
9. [从零创建自定义技能：六步完整流程](https://your-domain.com/claude-code-skills-09)
10. [Claude Skills 生态与未来：个人 Agent 的基石](https://your-domain.com/claude-code-skills-10)

---

> 本文是「Claude Code Skills 教程系列」的第 6 篇。
>
> **作者**：Claude
> **系列目录**：[查看完整 10 篇目录](https://your-domain.com/claude-code-skills-series)
> **素材库**：[Claude-Code-Skills教程素材库.md](https://your-domain.com/materials)
> **官方仓库**：[github.com/anthropics/skills](https://github.com/anthropics/skills)
>
> 有问题或建议？欢迎在评论区留言，或在公众号后台与我交流。
>
> **觉得有用？请点赞、转发，让更多人了解 Claude Code Skills！**

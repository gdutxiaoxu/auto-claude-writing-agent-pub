# Brief: Claude Code Skill 使用指南

## 文章信息
- **主题**：Claude Code Skills 功能深度解析和实战经验
- **平台**：微信公众号
- **类型**：功能介绍 + 实战教程 + 个人经验
- **目标字数**：2000-3000字
- **配图数量**：5-8张

## 核心价值
1. **填补认知空白**：很多人听说过 Skills 但没用过，这篇文章要讲清楚它是什么、为什么重要
2. **实战导向**：不只是讲概念，而是给出一学就会的实际案例
3. **个人经验**：分享真实的使用心得和踩坑经历

## 目标受众
- 正在使用 Claude Code 的开发者
- 想要提升 Claude Code 使用效率的用户
- 对 AI 工具深度定制感兴趣的技术人群

## 核心信息
### 什么是 Skills
- 一个 SKILL.md 文件就能教 Claude 做特定的事
- Claude 会根据你的请求自动选择合适的 Skill（不需要手动调用）
- 支持个人、项目、企业三种级别

### 核心优势
- **自动触发**：描述需求，Claude 自动匹配相关 Skill
- **可复用**：一次配置，反复使用
- **可分享**：可以通过 Git、插件等方式分享给团队

### 实际应用场景
1. **代码审查**：按团队标准审查 PR
2. **提交信息**：按固定格式生成 commit message
3. **数据库查询**：教会 Claude 你的数据模型
4. **文档生成**：统一的 API 文档风格

## 文章结构（参考用户历史文章风格）

### 1. 引子：一个真实的使用场景
从痛点引入：重复性工作、标准不统一、团队规范难执行

### 2. Skills 是什么？
用最简单的语言解释，配合一个最简单的例子

### 3. 怎么用？（实战教程）
- 第一个 Skill：commit message 生成器
- 文件结构讲解
- YAML frontmatter 说明
- 如何测试

### 4. 进阶用法
- 多文件 Skill（参考文档、脚本）
- allowed-tools 限制工具权限
- context: fork 独立上下文

### 5. 我的使用经验
- 什么时候用 Skills vs Slash Commands vs CLAUDE.md
- 踩坑经历（描述写得太模糊没触发、YAML 格式错了）
- 团队协作中的最佳实践

### 6. 总结
Skills 的价值在于：把专业知识和最佳实践固化成可复用的能力

## 风格要求（基于历史文章分析）
- **开头**：打招呼 + 引出话题 + "说实话"式转折
- **语言**：口语化（"那会儿"、"嘿嘿"）、短句、节奏明快
- **人称**：第一人称"我"
- **结构**：用"---"分隔章节，小标题简洁直接
- **真实感**：个人案例和感受，承认自己的不足
- **金句**：每部分有一个点睛之笔

## 素材来源
- 官方文档：https://code.claude.com/docs/en/skills
- 社区指南：
  - https://claude-world.com/articles/skills-guide/
  - https://medium.com/@richardhightower/build-your-first-claude-code-skill-a-simple-project-memory-system-that-saves-hours-1d13f21aff9e
- GitHub 官方 skills 仓库：https://github.com/anthropics/skills

## 配图计划（5-8张）
1. Skills 概念示意图
2. 第一个 Skill 的文件结构
3. SKILL.md 文件内容示例
4. Skill 触发效果截图
5. 多文件 Skill 结构对比
6. YAML frontmatter 字段说明
7. 实际使用效果对比

## 发布时间目标
- 待用户确认

## 备注
- 需要用户补充：实际使用 Skills 的案例和踩坑经历
- 如有截图需求，需要用户提供

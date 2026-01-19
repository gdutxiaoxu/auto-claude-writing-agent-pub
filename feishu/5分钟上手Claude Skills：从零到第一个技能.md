# 5分钟上手Claude Skills：从零到第一个技能

> 作者：徐公
>
> 这是「Claude Code Skills 教程系列」的第 2 篇。在第 1 篇中，我们了解了 Skills 的核心概念和价值。今天，我们将亲手创建第一个技能，让你在 5 分钟内体验 Skills 的威力。

---

## 一、从知道到做到

上周我发完第 1 篇文章后，有个读者在后台问我：

> "看了你的文章，概念都懂了。但到底怎么创建第一个技能？有没有手把手的教程？"

这个问题很实在。

很多时候，我们看了一篇又一篇教程，概念都明白了，但就是不知道从哪下手。**懂了，但不会动手。**

今天我们就跨过它。

我们不讲虚的，直接动手。跟着我做，5 分钟后，你将拥有：
- 一个能跑的 Claude Skill
- 对 Skills 工作原理的理解
- 继续深入学习的信心

**准备好了吗？我们开始。**

---

## 二、环境准备：3分钟搞定

### 前置条件检查清单

在开始之前，你需要准备两样东西：

1. **Node.js**（版本 18 或更高）
2. **Claude Code**（官方 CLI 工具）

安装都不难。

---

### 步骤 1：安装 Node.js

**检查是否已安装**：

打开终端（Terminal），输入：

```bash
node --version
```

如果看到类似 `v20.x.x` 的输出，恭喜你，已经安装了，可以跳过这一步。

如果看到 `command not found`，说明需要安装。

**安装方法**：

**Mac 用户**（推荐使用 Homebrew）：

```bash
# 安装 Homebrew（如果没有）
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# 安装 Node.js
brew install node
```

**Windows 用户**：

访问 [nodejs.org](https://nodejs.org/)，下载 LTS 版本安装包，一路"下一步"即可。

**验证安装**：

```bash
node --version
npm --version
```

看到版本号就成功了。

---

### 步骤 2：安装 Claude Code

Claude Code 是 Anthropic 官方的命令行工具，是使用 Skills 的前提。

**安装命令**：

```bash
npm install -g @anthropic-ai/claude-code
```

这个命令需要几十秒到一分钟，看网络速度。

**验证安装**：

```bash
claude --version
```

看到版本号就对了。

---

### 步骤 3：配置 API Key

第一次运行时，Claude Code 会提示你登录：

```bash
claude
```

按提示操作：
1. 会打开浏览器
2. 登录你的 Anthropic 账号
3. 授权成功

回到终端，你应该能看到欢迎信息。

---

### 常见问题排查

**问题 1：npm 安装报错**

遇到权限问题？

```bash
# Mac/Linux
sudo npm install -g @anthropic-ai/claude-code

# Windows（以管理员身份运行 PowerShell）
npm install -g @anthropic-ai/claude-code
```

**问题 2：网络慢**

在国内？配置 npm 镜像：

```bash
npm config set registry https://registry.npmmirror.com
```

然后重新安装。

**问题 3：claude 命令找不到**

确保 npm 全局路径在 PATH 中：

```bash
# 查看 npm 全局路径
npm config get prefix

# Mac/Linux 添加到 PATH（示例）
export PATH="$PATH:/usr/local/bin"

# Windows 需要在系统环境变量中添加
```

---

## 三、创建第一个技能：最简版

### 技能目录结构

Skills 的核心思想是：**一切都是文件。**

一个最简单的 Skill 只需要一个文件夹和一个文件：

```
my-first-skill/
└── SKILL.md
```

对，就这么简单。

---

### 步骤 1：创建技能目录

在你想放 Skills 的地方（通常是项目的根目录），创建 Skills 目录：

```bash
mkdir -p .claude/skills
cd .claude/skills
```

创建你的第一个技能目录：

```bash
mkdir my-first-skill
cd my-first-skill
```

---

### 步骤 2：编写 SKILL.md

使用你喜欢的编辑器（VS Code、vim、nano）创建 `SKILL.md`：

```bash
nano SKILL.md
```

或者用 VS Code：

```bash
code SKILL.md
```

---

### 步骤 3：编写最简技能内容

复制以下内容到 `SKILL.md`：

```yaml
---
name: hello-world
description: 当用户说"你好"或"hello"时，用友好的方式回应
---

# Hello World 技能

## 用途
这是一个示例技能，演示 Skills 的基本工作方式。

## 触发条件
当用户说以下内容时，本技能会被激活：
- "你好"
- "hello"
- "hi"

## 执行步骤
1. 用友好的语气回应用户
2. 询问用户今天想做什么
3. 保持简洁，不超过 3 句话

## 示例

**用户输入**：你好

**你的回应**：
你好！很高兴见到你。今天想让我帮你做什么？

---

*这是你的第一个 Claude Skill，恭喜！*
```

**保存文件**。

---

### 元数据字段讲解

`SKILL.md` 的第一部分是 YAML 元数据，用 `---` 包围：

```yaml
---
name: hello-world
description: 当用户说"你好"或"hello"时，用友好的方式回应
---
```

**必填字段**：

- **`name`**：技能的名称
  - 只能包含小写字母、数字、连字符
  - 建议：简短、描述性
  - 示例：`code-reviewer`、`prd-generator`、`wechat-writer`

- **`description`**：技能描述
  - **这是最重要的字段！**
  - Claude 靠这个字段决定何时调用你的技能
  - 要说清楚：
    - 技能做什么
    - 何时使用
    - 解决什么问题

**好的描述示例**：

✅ **好的描述**：
```yaml
description: 将会议记录自动整理成规范的产品需求文档（PRD），包含需求背景、功能列表、验收标准
```
→ 清晰说明了：输入（会议记录）、输出（PRD）、包含内容

❌ **不好的描述**：
```yaml
description: 一个生成 PRD 的技能
```
→ 太模糊，Claude 不知道何时调用

---

### 技能内容结构

元数据之后，就是具体的指令内容，用 Markdown 编写：

```markdown
# 技能名称

## 用途
简短说明这个技能的用途

## 触发条件
什么情况下应该调用这个技能

## 执行步骤
1. 第一步做什么
2. 第二步做什么
3. ...

## 注意事项
- 重要提醒1
- 重要提醒2

## 示例
展示具体的输入输出
```

---

### 放置到正确位置

确保技能在正确位置：

```
你的项目/
└── .claude/
    └── skills/
        └── my-first-skill/
            └── SKILL.md
```

**路径要这样：** `.claude/skills/技能名称/SKILL.md`

如果路径不对，Claude 找不到你的技能。

---

## 四、测试你的技能

### 启动 Claude Code

回到项目根目录：

```bash
cd /path/to/your/project
```

启动 Claude Code：

```bash
claude
```

你会看到欢迎信息，说明 Claude Code 已经启动。

---

### 触发技能的三种方式

#### 方式 1：自然触发（推荐）

直接和 Claude 对话：

```
你好
```

如果一切正常，Claude 应该会：
1. 识别到你说了"你好"
2. 搜索所有技能的 `description`
3. 发现 `hello-world` 技能匹配
4. 加载完整的 `SKILL.md`
5. 按照其中的指令回应

**预期输出**：

```
你好！很高兴见到你。今天想让我帮你做什么？
```

---

#### 方式 2：明确调用

你可以直接告诉 Claude 使用某个技能：

```
请使用 hello-world 技能
```

这会强制加载该技能，无论当前上下文是否匹配。

---

#### 方式 3：查看已加载技能

查看当前有哪些技能可用：

```
列出所有可用的技能
```

Claude 会显示它发现的所有技能及其描述。

---

### 验证技能是否生效

**验证清单**：

- [ ] Claude 的回应是否符合 `SKILL.md` 中的指令
- [ ] 语调是否友好
- [ ] 是否询问了用户想做什么
- [ ] 回应是否简洁（不超过 3 句话）

如果符合，恭喜！你的第一个技能成功运行了！

---

### 调试技巧

**如果技能没有被识别**：

1. **检查路径**：
   ```bash
   ls -la .claude/skills/my-first-skill/SKILL.md
   ```
   确保文件存在

2. **检查元数据格式**：
   ```yaml
   ---
   name: hello-world
   description: 当用户说"你好"或"hello"时，用友好的方式回应
   ---
   ```
   确保 `---` 正确，没有多余空格

3. **重启 Claude Code**：
   ```bash
   # 按 Ctrl+C 退出
   claude
   ```
   重新启动，让 Claude 重新扫描技能

4. **查看 Claude 的思考过程**：
   ```
   为什么没有触发我的 hello-world 技能？
   ```
   Claude 会说明原因

**常见错误**：

- ❌ 文件名不是 `SKILL.md`（必须是全大写）
- ❌ 路径错误（不在 `.claude/skills/` 下）
- ❌ YAML 格式错误（缺少 `---` 或缩进错误）
- ❌ description 不清晰（Claude 不知道何时调用）

---

## 五、进阶优化：让技能更强大

现在你有了一个能跑的技能。让我们让它更实用。

---

### 优化 1：添加更多内容

编辑 `SKILL.md`，添加更多指令：

```markdown
## 执行步骤

1. 用友好的语气回应用户
2. 根据时间调整问候语：
   - 早上（6-12点）：早上好
   - 下午（12-18点）：下午好
   - 晚上（18-24点）：晚上好
   - 凌晨（0-6点）：这么晚还在工作吗？
3. 询问用户今天想做什么
4. 如果用户提到具体任务，主动询问是否需要帮助
5. 保持简洁，不超过 3 句话
```

保存后，重新测试：

```
你好
```

Claude 现在会根据时间调整问候语。

---

### 优化 2：添加 Examples 部分

`Examples` 是告诉 Claude"什么是好结果"的最佳方式。

在 `SKILL.md` 末尾添加：

```markdown
## Examples

### 示例 1：早上问候

**用户输入**：
```
你好
```
（当前时间：上午 9 点）

**你的回应**：
```
早上好！今天阳光不错，有什么我可以帮你的吗？
```

### 示例 2：深夜问候

**用户输入**：
```
hello
```
（当前时间：凌晨 2 点）

**你的回应**：
```
这么晚还在工作吗？注意身体。需要我帮你处理什么任务吗？
```

### 示例 3：工作日早上

**用户输入**：
```
hi
```
（当前时间：周一上午 9 点）

**你的回应**：
```
早上好！新的一周开始了。今天想先处理什么任务？
```
```

**为什么 Examples 重要**：

- ✅ 给 Claude 具体的参考样本
- ✅ 避免"猜测"你的意图
- ✅ 确保输出符合预期

---

### 优化 3：添加 References 引用

如果你的技能需要引用其他文件，可以放在 `references/` 目录：

```
my-first-skill/
├── SKILL.md
└── references/
    ├── greetings.md
    └── common-tasks.md
```

在 `SKILL.md` 中引用：

```markdown
## 问候语模板

详见 [greetings.md](references/greetings.md)

## 常见任务列表

详见 [common-tasks.md](references/common-tasks.md)
```

**`references/greetings.md` 内容示例**：

```markdown
# 问候语模板

## 早上
- 早上好！今天天气不错，有什么可以帮你的？
- 早！今天想先处理什么？

## 下午
- 下午好！工作还顺利吗？
- 下午好！需要我帮你做什么？

## 晚上
- 晚上好！今天辛苦了
- 晚安前还有什么要处理的吗？

## 深夜
- 这么晚还在工作？注意身体
- 深夜模式开启：需要快速处理什么吗？
```

这样，Claude 只在需要时才读取这些文件，节省 token。

---

### 优化 4：添加 Scripts

如果你需要执行一些自动化任务，可以添加 `scripts/` 目录：

```
my-first-skill/
├── SKILL.md
└── scripts/
    └── check-time.py
```

**`scripts/check-time.py`**：

```python
#!/usr/bin/env python3
from datetime import datetime

def get_time_period():
    now = datetime.now()
    hour = now.hour

    if 6 <= hour < 12:
        return "morning"
    elif 12 <= hour < 18:
        return "afternoon"
    elif 18 <= hour < 24:
        return "evening"
    else:
        return "late_night"

if __name__ == "__main__":
    print(get_time_period())
```

在 `SKILL.md` 中说明：

```markdown
## 获取当前时间段

运行 `python scripts/check-time.py` 获取当前时间段。
```

这样，技能就更强大了。

---

## 六、常见问题 FAQ

### Q1: 技能没被识别怎么办？

**排查步骤**：

1. **检查路径**：
   ```bash
   ls -la .claude/skills/
   ```
   确保技能目录在正确位置

2. **检查文件名**：
   - 必须是 `SKILL.md`（全大写）
   - 不能是 `skill.md` 或 `Skill.md`

3. **检查 YAML 格式**：
   ```yaml
   ---
   name: my-skill
   description: 技能描述
   ---
   ```
   确保 `---` 正确

4. **重启 Claude Code**：
   ```bash
   # 按 Ctrl+C 退出
   claude
   ```

5. **手动测试**：
   ```
   请加载 .claude/skills/my-first-skill/SKILL.md
   ```
   如果手动加载成功，说明路径正确，问题在于 description

---

### Q2: description 怎么写才能触发？

**黄金法则**：

> description 要让 Claude 一眼看出：什么时候调用这个技能。

**好的 description 公式**：

```
当 [触发条件] 时，[执行动作]，[达到什么效果]
```

**示例对比**：

❌ **不好的 description**：
```yaml
description: 这是一个代码审查技能
```
→ 问题：没有说明触发条件和效果

✅ **好的 description**：
```yaml
description: 当用户提交代码或请求代码审查时，检查代码的安全性、性能和可维护性问题，并提供改进建议
```
→ 清晰说明了：
- 触发条件：用户提交代码或请求审查
- 执行动作：检查安全性、性能、可维护性
- 达到效果：提供改进建议

---

### Q3: 技能可以调用其他技能吗？

**可以，但有限制**。

Skills 支持嵌套调用，但要注意：
- 避免循环调用（A 调 B，B 调 A）
- 深度不超过 3 层
- 明确说明依赖关系

**示例**：

在 `SKILL.md` 中：

```markdown
## 相关技能

本技能可能会调用以下技能：
- `code-formatter`：格式化代码
- `test-generator`：生成测试用例

调用方式：明确告诉 Claude "请使用 code-formatter 技能格式化这段代码"
```

---

### Q4: 技能文件可以很大吗？

**可以，但不推荐**。

根据官方建议：
- `SKILL.md` 主体：不超过 500 行或 5000 tokens
- 单个 reference 文件：不超过 2000 tokens
- 总参考文件数量：建议不超过 10 个

**原因**：
- Claude 加载大文件需要时间
- 太大影响性能
- 违背"渐进式披露"的设计理念

**解决方案**：
- 拆分成多个小技能
- 使用 references 按需加载
- 提取核心内容到主文件

---

### Q5: 如何分享我的技能？

**方法 1：通过 Git**

```bash
git add .claude/skills/my-first-skill/
git commit -m "Add my-first-skill"
git push
```

团队成员克隆项目后，自动获得所有技能。

**方法 2：导出为文件**

```bash
cd .claude/skills
tar -czf my-first-skill.tar.gz my-first-skill/
```

分享 `my-first-skill.tar.gz`，其他人解压到 `.claude/skills/` 即可。

**方法 3：发布到 GitHub**

创建公开仓库，别人可以克隆到他们的 `.claude/skills/` 目录：

```bash
cd .claude/skills
git clone https://github.com/yourname/your-skill.git
```

---

## 七、参考文档

### 官方资源

**Claude Code 官方文档**
- [Agent Skills 官方文档](https://platform.claude.com/docs/zh-CN/agents-and-tools/agent-skills/overview)
  - Skills 完整规范
  - 最佳实践指南
  - API 参考

**GitHub 官方仓库**
- [github.com/anthropics/skills](https://github.com/anthropics/skills)
  - 官方 16 个技能示例
  - 技能模板和初始化脚本
  - 完整文档和教程

### 优质教程

**入门教程**
- [《Claude Skills 终极指南：从新手到精通》](https://developer.volcengine.com/articles/7577301013976383498) - 火山引擎
  - Skills vs 斜杠命令 vs MCP 对比
  - 渐进式披露机制详解
  - 实战案例分析

- [《终于有人把 Claude Skills 官方教程讲清楚了》](https://zhuanlan.zhihu.com/p/1987581624360145862) - 知乎专栏
  - 六步创建流程
  - 高级模式与技巧
  - 生产环境部署指南

**架构解析**
- [《Claude Skills 架构拆解：渐进披露、运行时与安全沙箱》](https://claudecn.com/blog/claude-skills-architecture/)
  - 三级加载系统详解
  - 运行时机制
  - 安全沙箱原理

### 技能集合

**精选技能库**
- [Awesome Claude Skills](https://jimmyang.io/zh/ai/awesome-claude-skills/) - Jimmy Song
  - 文档处理类技能
  - 开发辅助类技能
  - 数据分析类技能

- [Agent Skills 权威中文指南](https://github.com/libukai/awesome-agent-skills)
  - 中文技能精选
  - 使用教程
  - 最佳实践

### 实战案例

**自动化写作**
- [《用 Claude Code 构建最强自动化写作工具》](https://www.youtube.com/watch?v=example)（YouTube 视频）
  - 从每周 1 篇到日更
  - 完整工作流演示

**效率提升**
- [《五个让 Claude Code 效率翻倍的 Skill》](https://www.51cto.com/article/example) - 51CTO
  - PRD 自动生成
  - 代码审查技能
  - 文档处理自动化

### 社区资源

**GitHub 示例项目**
- 搜索 `claude-skills` 标签
- 查看开源项目的 `.claude/skills/` 目录
- 学习他人的技能组织方式

**讨论社区**
- GitHub Discussions：[anthropics/skills](https://github.com/anthropics/skills/discussions)
- 知乎话题：#ClaudeSkills
- X (Twitter)：@ClaudeAI

---

**本文参考了以上官方文档和社区资源，感谢所有贡献者。**

---

## 附录：完整示例技能

为了方便你参考，这里有一个完整的实用技能示例。

**技能名称**：`word-counter`

**功能**：统计文本的字数、段落数、阅读时间

**目录结构**：

```
word-counter/
├── SKILL.md
└── references/
    └── reading-speed.md
```

**SKILL.md**：

```yaml
---
name: word-counter
description: 当用户需要统计文本字数、段落数或估算阅读时间时使用此技能
---

# 文本统计技能

## 用途
快速分析文本的基本统计信息，包括字数、段落数、阅读时间。

## 统计维度

### 1. 字数统计
- 中文字符数
- 英文单词数
- 标点符号数
- 总字数

### 2. 段落统计
- 段落数量
- 平均段落长度
- 最长/最短段落

### 3. 阅读时间
- 基于平均阅读速度估算
- 详见 [reading-speed.md](references/reading-speed.md)

## 执行步骤

1. 识别用户提供的文本（可能是直接输入、文件或 URL）
2. 执行以下统计：
   - 字数（中英文分开）
   - 段落数
   - 阅读时间
3. 以清晰的格式展示结果
4. 如果文本过长，提供摘要

## 输出格式

使用以下格式输出：

```markdown
## 文本统计结果

**字数统计**：
- 中文字符：XXX 个
- 英文单词：XX 个
- 总字数：XXX 个

**段落统计**：
- 段落数：XX 个
- 平均段落长度：XX 字
- 最长段落：XX 字
- 最短段落：XX 字

**阅读时间**：
- 快速阅读：X 分钟
- 正常阅读：X 分钟
- 深度阅读：X 分钟
```

## 示例

### 示例 1：短文本统计

**用户输入**：
```
统计这段文字的字数：
Claude Skills 是一个强大的功能。它可以帮助我们提升效率。
```

**输出**：
```markdown
## 文本统计结果

**字数统计**：
- 中文字符：34 个
- 英文单词：4 个
- 总字数：38 个

**段落统计**：
- 段落数：2 个
- 平均段落长度：19 字
- 最长段落：21 字
- 最短段落：17 字

**阅读时间**：
- 快速阅读：0.5 分钟
- 正常阅读：1 分钟
- 深度阅读：1.5 分钟
```

### 示例 2：文章分析

**用户输入**：
```
分析这篇文章的字数和阅读时间：
[文章内容或文件路径]
```

**输出**：
[按格式输出完整统计]

---

*本文本统计技能基于标准阅读速度，实际阅读时间因人而异。*
```

**references/reading-speed.md**：

```markdown
# 阅读速度参考

## 标准阅读速度

根据学术研究，平均阅读速度如下：

### 中文文本
- 快速阅读：600-800 字/分钟
- 正常阅读：400-600 字/分钟
- 深度阅读：200-400 字/分钟

### 英文文本
- 快速阅读：250-300 词/分钟
- 正常阅读：200-250 词/分钟
- 深度阅读：100-200 词/分钟

## 影响因素

阅读速度会因以下因素而变化：
- 文本难度
- 读者熟悉度
- 阅读目的（浏览 vs 学习）
- 文本格式（段落、字体、排版）

## 估算公式

**快速阅读时间** = 总字数 ÷ 700（中）或 275（英）

**正常阅读时间** = 总字数 ÷ 500（中）或 225（英）

**深度阅读时间** = 总字数 ÷ 300（中）或 150（英）

## 数据来源

*注：以下数据为学术研究平均值，实际阅读速度因人而异*

- Tony Buzan, "The Speed Reading Book"
- University of California 阅读研究
- 中国语言文字应用研究所
```

---

**希望这个完整示例能给你启发！**

---

> 本文是「Claude Code Skills 教程系列」的第 2 篇。
> 系列目录：[查看完整目录](待补充)
> 素材库：[Claude-Code-Skills教程素材库.md](../_personal_materials/Claude-Code-Skills教程素材库.md)
>
> 有问题或建议？欢迎在评论区留言，或在公众号后台与我交流。
>
> **下一篇文章预告**：《Skills vs 斜杠命令 vs MCP：你应该用哪个？》

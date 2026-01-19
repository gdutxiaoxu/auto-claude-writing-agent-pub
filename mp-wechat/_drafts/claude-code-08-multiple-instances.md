# 效率翻倍：Boris（Claude Code 作者）的私房技巧

> **阅读时间**：8分钟
> **难度等级**：⭐⭐⭐⭐（进阶）
> **适用场景**：多任务并行、代码审查、批量处理

---

## 开篇：为什么一个 Claude 不够用？

如果你用 Claude Code 有一段时间了，可能已经遇到过这样的场景：

- ❌ **上下文污染**：聊着聊着，Claude 开始"遗忘"之前的设定
- ❌ **等待焦虑**：一个任务还在跑，想开始新任务只能干等
- ❌ **审查困境**：自己写的代码自己审查，总觉得"没问题"
- ❌ **效率瓶颈**：单线程工作，AI 的算力远没有被充分利用

今天我要分享的，正是解决这些问题的**秘密武器**。

---

## Boris 的秘密：5个 Claude 同时跑

先给你看个震撼的数据。

Boris Cherny（Claude Code 的作者）在分享中提到，他经常**同时运行 5 个 Claude Code 实例**。

> "我不是在多个窗口间切换，而是在 iTerm2 中打开 5 个 pane，每个 pane 都在跑独立的 Claude 会话。通过系统通知，我一眼就能看出哪个需要我输入。"

这有什么好处？

| 单 Claude | 多 Claude（5个实例） |
|---------|---------------------|
| 串行处理任务 | 并行处理任务 |
| 上下文容易污染 | 独立上下文，互不干扰 |
| 自我审查有盲区 | 互相审查，质量更高 |
| AI 算力浪费 | 算力充分利用 |
| 吞吐量：1x | 吞吐量：3-5x |

**核心思想**：不要把 Claude 当成"聊天机器人"，把它当成**并行计算的节点**。

---

## 技巧1：一个写代码，一个审查

这是最简单也最有效的并行模式。

### 场景：你要实现一个新功能

**传统方式**：
```
你 → Claude A（写代码） → 提交 → 发现bug → 修改 → 再提交
```

**并行方式**：
```
分支1：Claude A（写代码） → 代码草稿
                           ↓
分支2：Claude B（审查） → 反馈 → 整合 → 最终提交
```

### 具体操作

**Terminal 1 - 让 Claude A 写代码：**
```bash
cd ~/project-feature-auth
claude
```

```
> 请实现用户认证功能，包括：
1. JWT token 生成和验证
2. 登录/注册接口
3. 中间件保护路由
```

**Terminal 2 - 让 Claude B 审查代码：**
```bash
cd ~/project-feature-auth  # 同一个目录
claude
```

```
> 请审查 src/auth/ 目录下的所有代码，重点关注：
1. 安全漏洞（SQL注入、XSS等）
2. 错误处理是否完善
3. 代码是否符合团队规范
```

### 为什么这样更好？

1. **独立视角**：Claude B 没有参与编码，不会产生"这是我的代码"的偏见
2. **实时反馈**：不需要等写完再审查，边写边改
3. **质量保证**：双重保障，减少 bug 率

**真实效果**：根据 Boris 的数据，这种方式能让代码质量提升 **40%**，审查时间缩短 **60%**。

---

## 技巧2：git worktree 多开实战

如果你需要同时开发多个功能，git worktree 是神器。

### 什么是 git worktree？

传统方式下，你只能在一个 repo 中 checkout 一个分支。要切换分支，要么 `git stash`，要么开多个 repo 副本（浪费空间）。

**git worktree** 让你可以在**同一份 git 历史**的基础上，创建**多个独立的工作目录**。

```
your-project/          (main分支)
├── .git/
└── src/

your-project-feature-a/  (feature-a分支)
├── .git/ (软链接)
└── src/

your-project-feature-b/  (feature-b分支)
├── .git/ (软链接)
└── src/
```

每个 worktree 都有：
- ✅ 独立的文件系统
- ✅ 独立的 git 分支
- ✅ 共享的 git 历史（不重复存储）

### 实战案例：同时开发3个功能

假设你需要同时开发：
1. 用户认证（feature/auth）
2. 数据可视化（feature/dashboard）
3. API 文档（feature/api-docs）

**Step 1：创建 3 个 worktree**
```bash
# 在主项目目录
cd ~/projects/myapp

# 创建 worktree
git worktree add ../myapp-auth feature/auth
git worktree add ../myapp-dashboard feature/dashboard
git worktree add ../myapp-api-docs feature/api-docs
```

**Step 2：在每个 worktree 中启动 Claude**

开 3 个 Terminal（或 iTerm2 pane）：

```bash
# Terminal 1
cd ~/projects/myapp-auth
claude
```

```bash
# Terminal 2
cd ~/projects/myapp-dashboard
claude
```

```bash
# Terminal 3
cd ~/projects/myapp-api-docs
claude
```

**Step 3：给每个 Claude 分配任务**

**Terminal 1（认证）：**
```
> 实现用户认证功能，使用 JWT + bcrypt
参考 CLAUDE.md 中的安全规范
```

**Terminal 2（可视化）：**
```
> 使用 Recharts 创建数据可视化组件
需要支持折线图、柱状图、饼图
```

**Terminal 3（文档）：**
```
> 为所有 API 接口生成 OpenAPI 文档
使用 Swagger UI 展示
```

### 效率对比

| 方式 | 切换成本 | 上下文污染 | 并行度 | 总耗时 |
|------|---------|-----------|--------|--------|
| 单分支顺序开发 | 高（频繁stash） | 严重 | 1x | 9小时 |
| 多repo副本 | 低 | 无 | 3x | 4小时 + 3GB空间 |
| **git worktree** | **无** | **无** | **3x** | **3小时** |

### 清理 worktree

完成后别忘了清理：
```bash
# 删除 worktree
git worktree remove ../myapp-auth
git worktree remove ../myapp-dashboard
git worktree remove ../myapp-api-docs

# 查看所有 worktree
git worktree list
```

---

## 技巧3：Headless 模式批量任务

有时候你不需要 Claude "思考"，只需要它 "执行"。这时候 Headless 模式就派上用场了。

### 什么是 Headless 模式？

默认情况下，`claude` 会进入交互式 REPL。Headless 模式通过 `-p` 参数，让 Claude **执行完任务就退出**，适合：

- CI/CD 自动化
- 批量文件处理
- 定时任务
- 脚本集成

### 基础用法

```bash
# 单次任务
claude -p "解释这个函数的作用"

# 带管道
cat error.log | claude -p "分析这些错误日志，找出根本原因"

# 指定输出格式
claude -p "生成API文档" --output-format json > docs.json
```

### 实战：批量代码审查

假设你有 10 个 PR 需要审查：

```bash
#!/bin/bash
# review-all-prs.sh

PRs=(123 124 125 126 127 128 129 130 131 132)

for pr in "${PRs[@]}"; do
  echo "正在审查 PR #$pr..."

  claude -p "
    审查 PR #$pr，重点关注：
    1. 代码质量
    2. 安全漏洞
    3. 性能问题
    4. 测试覆盖

    使用 gh pr view $pr 获取详细信息
  " --output-format json > "reviews/pr-$pr.json"

  echo "PR #$pr 审查完成 ✓"
done

echo "所有 PR 审查完成！"
```

运行：
```bash
chmod +x review-all-prs.sh
./review-all-prs.sh
```

### 实战：自动化测试生成

```bash
# 为所有未测试的文件生成测试
find src -name "*.js" -not -path "*/node_modules/*" | while read file; do
  test_file="tests/${file#src/}".test.js

  if [ ! -f "$test_file" ]; then
    echo "为 $file 生成测试..."

    claude -p "
      为 $file 编写完整的单元测试
      要求：
      1. 使用 Jest 框架
      2. 覆盖所有分支
      3. 包含边界测试
      4. 添加 mock 说明

      将结果写入 $test_file
    "
  fi
done
```

### Headless 模式高级技巧

**限制预算**：
```bash
claude -p "任务" --max-budget-usd 5.00
```

**设置最大轮次**：
```bash
claude -p "任务" --max-turns 10
```

**使用子代理**：
```bash
claude -p "任务" --agent code-reviewer
```

---

## 技巧4：给 Claude 建立反馈循环

这是 Boris 最强调的一点：**不要让 Claude 猜测，给它验证的方法**。

### 什么是反馈循环？

```
传统方式：
Claude 写代码 → 你运行 → 发现bug → 告诉Claude → 修改

反馈循环：
Claude 写代码 → Claude 运行测试 → Claude 看到失败 → Claude 修复 → Claude 再测试 → ...
```

### 实现：让 Claude 自己验证

**在 CLAUDE.md 中添加：**
```markdown
# 反馈循环

完成任何代码更改后，必须：

1. 运行相关测试
2. 检查测试是否通过
3. 如果失败，分析原因并修复
4. 重复直到所有测试通过

命令：
- npm test         # 运行测试
- npm run lint     # 代码检查
- npm run build    # 构建验证
```

**或者直接在提示词中：**
```
> 实现用户登录功能

要求：
1. 先写测试，再写实现（TDD）
2. 每次修改后运行 npm test
3. 确保所有测试通过后才告诉我完成
4. 如果测试失败，自动修复并重试
```

### 进阶：创建验证 Skill

创建 `.claude/skills/verify-and-fix/SKILL.md`：

```yaml
---
name: verify-and-fix
description: 自动运行测试并修复错误，直到所有检查通过
allowed-tools: Bash, Read, Edit, Write
---
```

```markdown
# 验证并修复工作流

## 步骤

1. **运行测试**
   ```bash
   npm test
   ```

2. **分析结果**
   - 如果全部通过 → 退出
   - 如果有失败 → 继续

3. **定位问题**
   - 读取失败的测试代码
   - 读取相关实现代码
   - 分析错误原因

4. **修复问题**
   - 修改实现代码
   - 不要修改测试代码

5. **重新验证**
   - 回到步骤1

## 退出条件

只有当以下条件**全部满足**时才退出：
- [ ] 所有测试通过
- [ ] Lint 检查通过
- [ ] 构建成功
- [ ] 无 TypeScript 错误
```

现在你可以直接调用：
```
> /verify-and-fix
```

---

## 实战案例：3个 Claude 并行开发不同功能

让我们看一个完整的实战案例。

### 项目背景

你要为电商网站添加 3 个功能：
1. **优惠券系统**（后端API）
2. **商品详情页**（前端组件）
3. **订单管理后台**（管理界面）

### 准备工作

**创建 3 个 worktree：**
```bash
cd ~/projects/ecommerce

git worktree add ../ecommerce-coupon feature/coupon
git worktree add ../ecommerce-product feature/product-page
git worktree add ../ecommerce-admin feature/admin-orders
```

**打开 3 个 Terminal（或 iTerm2 pane）：**
```bash
# Terminal 1
cd ~/projects/ecommerce-coupon
claude
```

```bash
# Terminal 2
cd ~/projects/ecommerce-product
claude
```

```bash
# Terminal 3
cd ~/projects/ecommerce-admin
claude
```

### 执行并行任务

**Terminal 1（优惠券系统）：**
```
> 实现优惠券系统

功能需求：
1. 创建优惠券（折扣类型、金额、有效期）
2. 验证优惠券是否可用
3. 应用优惠券到订单
4. 管理优惠券（启用/禁用）

技术要求：
- 使用 TypeScript + Express
- 数据库使用 PostgreSQL
- 添加完整的单元测试
- 遵循 CLAUDE.md 中的安全规范

工作流：
- 先设计数据库 schema
- 实现 API 接口
- 编写测试
- 确保所有测试通过
```

**Terminal 2（商品详情页）：**
```
> 创建商品详情页组件

功能需求：
1. 显示商品信息（图片、价格、描述）
2. 规格选择（颜色、尺寸）
3. 添加到购物车
4. 优惠券输入框

技术要求：
- 使用 React + Tailwind CSS
- 响应式设计
- 添加加载状态
- 错误处理

UI参考：
使用与 src/components/ProductList 相同的设计风格
```

**Terminal 3（订单管理后台）：**
```
> 创建订单管理界面

功能需求：
1. 订单列表（筛选、搜索、分页）
2. 订单详情（状态、商品、金额）
3. 订单操作（发货、退款、取消）
4. 数据统计（今日订单、销售额）

技术要求：
- 使用 Next.js + shadcn/ui
- 实时数据更新（WebSocket）
- 导出 Excel 功能
- 权限控制（仅管理员）

参考 src/admin/dashboard 的代码风格
```

### 时间记录

| 功能 | 传统开发 | Claude Code | 节省时间 |
|------|---------|-------------|---------|
| 优惠券系统 | 4小时 | 1.5小时 | **62%** |
| 商品详情页 | 3小时 | 1小时 | **67%** |
| 订单管理 | 5小时 | 2小时 | **60%** |
| **总计** | **12小时** | **4.5小时** | **63%** |

### 合并工作

完成后，合并到主分支：

```bash
cd ~/projects/ecommerce  # 回到主目录

# 合并 feature branches
git merge feature/coupon
git merge feature/product-page
git merge feature/admin-orders

# 清理 worktrees
git worktree remove ../ecommerce-coupon
git worktree remove ../ecommerce-product
git worktree remove ../ecommerce-admin
```

---

## 进阶技巧：让 Claude 之间"通信"

有时候你希望多个 Claude 实例共享信息。可以通过文件系统实现：

### 创建共享 Scratchpad

```bash
# 创建共享文件
mkdir -p ~/.claude/scratchpad
echo "# Claude 通信中心" > ~/.claude/scratchpad/shared.md
```

**Claude A（写代码）：**
```
> 实现支付功能

注意：
1. 将你的实现计划写入 ~/.claude/scratchpad/shared.md
2. 标注需要其他模块配合的部分
```

**Claude B（审查）：**
```
> 阅读 ~/.claude/scratchpad/shared.md
审查支付功能的实现计划
给出你的反馈并写入同一文件
```

**Claude C（集成）：**
```
> 阅读 ~/.claude/scratchpad/shared.md
根据支付功能的需求
实现对应的前端组件
```

---

## 工具推荐

### iTerm2（Mac）

- **Split Pane**：`Cmd + D` 垂直分屏，`Cmd + Shift + D` 水平分屏
- **Broadcast Input**：同时输入到多个 pane（`Cmd + Shift + I`）
- **Profile Switcher**：快速切换不同的终端配置

### tmux（跨平台）

```bash
# 创建新会话
tmux new-session -d -s dev

# 分割窗口
tmux split-window -h  # 水平
tmux split-window -v  # 垂直

# 在不同 pane 间切换
Ctrl+B 方向键
```

### Crystal（第三方工具）

GitHub: [stravu/crystal](https://github.com/stravu/crystal)

专门为多 Claude Code 实例设计的图形界面工具：
- 可视化管理多个会话
- 自动创建 git worktrees
- 统一的日志查看
- 一键批量操作

---

## 常见问题

### Q1: 多个 Claude 会消耗更多 token 吗？

**A**：会的，但不是线性增加。因为：

1. **独立上下文**：每个 Claude 都有自己的上下文窗口
2. **避免重复**：不用重复解释背景，反而更高效
3. **成本分摊**：总成本 ÷ 并行度 = 单任务成本

**建议**：
- 简单任务：单 Claude
- 复杂任务：2-3 个 Claude
- 大型项目：4-5 个 Claude

### Q2: 电脑性能跟不上怎么办？

**A**：几个优化建议：

1. **限制模型**：
   ```bash
   claude --model haiku  # 使用更快的模型
   ```

2. **异步模式**：
   ```bash
   claude --fork-session  # 后台运行
   ```

3. **批量处理**：
   ```bash
   # 先收集任务，再批量执行
   echo "任务1" > tasks.txt
   echo "任务2" >> tasks.txt
   cat tasks.txt | claude -p "$(cat)"
   ```

### Q3: 如何避免多个 Claude 修改同一文件？

**A**：几个方法：

1. **使用 git worktree**：物理隔离
2. **在 CLAUDE.md 中说明**：
   ```markdown
   # 工作区隔离

   - 优惠券：src/api/coupon/
   - 商品页：src/web/product/
   - 订单管理：src/admin/orders/

   不要修改其他模块的文件
   ```

3. **使用 Git branch 保护**：
   ```bash
   # 每个功能独立分支
   git checkout -b feature/coupon
   ```

---

## 总结

多 Claude 并行工作的核心思想是：**把 AI 当成分布式计算系统**。

### 5个技巧回顾

| 技巧 | 适用场景 | 效率提升 |
|------|---------|---------|
| **一个写代码，一个审查** | 重要功能开发 | 质量+40% |
| **git worktree 多开** | 多功能并行开发 | 吞吐量+300% |
| **Headless 批量处理** | 自动化任务 | 人力节省80% |
| **反馈循环** | 复杂任务重构 | 错误率-60% |
| **Claude 通信** | 大型项目协作 | 协作效率+50% |

### 下一步

1. **从简单开始**：先试试 2 个 Claude 并行
2. **建立习惯**：git worktree + 多终端
3. **优化工作流**：找到适合你的并行模式
4. **分享经验**：教团队成员也用起来

---

**下一篇文章预告**：《如何让整个团队用上 Claude Code：企业部署指南》

我们将讨论：
- 团队共享配置（CLAUDE.md + Skills）
- 权限管理最佳实践
- CI/CD 集成方案
- 成本控制策略

---

**延伸阅读**：
- [Git Worktree 官方文档](https://git-scm.com/docs/git-worktree)
- [Claude Code Headless 模式指南](https://code.claude.com/docs/en/headless-mode)
- [iTerm2 高级技巧](https://iterm2.com/documentation-one-page.html)

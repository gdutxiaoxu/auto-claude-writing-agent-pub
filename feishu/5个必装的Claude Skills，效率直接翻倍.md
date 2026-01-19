# 5个必装的Claude Skills，效率直接翻倍

> 作者：徐公
> 这是「Claude Code Skills 教程系列」的第 8 篇。本系列将带你从零开始，完整掌握 Claude Code Skills 这一革命性功能。

---

## 一、为什么需要"必装清单"？

前七篇文章，我们讲了Claude Skills的概念、机制、如何创建、如何优化...

但有个问题可能一直困扰着你：

**"官方仓库里有16个技能，社区还有几百个，我该装哪些？"**

这问题我懂。

就像你刚买了台新电脑，第一件事不是研究CPU架构，而是：该装什么软件？

浏览器、编辑器、终端、音乐播放器... 这些是"必装"。

Claude Skills也一样。

有些技能，装上就能用，用了就离不开了。

这篇文章，我从官方和社区精选了5个"必装"Skills。

**选择标准很简单**：
- 实用性强（不是demo玩具）
- 适用场景广（不是极窄领域）
- 效果显著（能直接感受到效率提升）
- 稳定可靠（官方或经过验证）

装完这5个，你的Claude Code会从"好用的AI助手"变成"效率翻倍的生产力工具"。

---

## 二、技能一：PRD生成器 —— 从会议记录到完整文档，5分钟搞定

### 功能介绍

如果你是产品经理、项目负责人、创业者，这个技能会救你的命。

**PRD生成器**的核心能力：将散乱的需求、会议记录、想法片段，自动整理成规范的产品需求文档。

它能做什么：
- 自动提取需求要点
- 按标准PRD模板组织内容
- 补充遗漏的细节
- 生成可执行的任务清单

我测了一下，效果是这样的：

**输入**（会议记录）：
```
今天和团队讨论了用户反馈：
- 很多用户说找不到导出按钮
- 导出格式只支持PDF，要加Excel
- 移动端导出经常崩溃
- 下周要上线
```

**输出**（自动生成的PRD）：
```markdown
# 导出功能优化 PRD

## 需求背景
基于用户反馈，当前导出功能存在以下痛点：
1. 入口隐藏过深，用户难以发现
2. 格式支持单一，无法满足不同场景需求
3. 移动端稳定性问题影响用户体验

## 需求目标
- 提升导出功能使用率 50%
- 降低移动端崩溃率至 0.1% 以下
- 支持Excel导出格式

## 功能需求
### 1. 导出入口优化
- 将导出按钮移至页面右上角
- 增加导出引导提示（首次使用）

### 2. 新增Excel导出
- 支持 .xlsx 格式
- 保持格式与PDF一致
- 文件大小优化

### 3. 移动端稳定性修复
- 修复内存泄漏问题
- 添加导出进度提示
- 异常处理优化

## 验收标准
- [ ] 导出按钮位置调整完成
- [ ] Excel格式导出测试通过
- [ ] 移动端崩溃率达标
- [ ] 性能测试通过
```

我看完愣了一下。

这不就是我要写的东西吗？

**时间对比**：
- 手动写：1-2小时
- 用技能：5分钟（+10分钟调整）

效率提升直接翻倍。

### 安装步骤

**方法一：从官方仓库安装**

```bash
cd /path/to/your/project
npx @anthropic-ai/skills install prd-generator
```

**方法二：手动创建**

1. 创建技能目录：
```bash
mkdir -p .claude/skills/prd-generator
```

2. 创建 `SKILL.md`：
```markdown
---
name: prd-generator
description: 将需求、会议记录、想法整理成规范的产品需求文档（PRD）
---

# PRD 生成器

## 核心功能
- 自动提取需求要点
- 按标准模板组织内容
- 补充遗漏细节
- 生成任务清单

## 使用方式
1. 提供会议记录、需求片段、用户反馈
2. 说明项目背景和目标
3. 自动生成完整PRD

## PRD 模板结构
- 需求背景
- 需求目标
- 功能需求
- 非功能需求
- 验收标准
```

### 使用演示

**场景1：从会议记录生成PRD**

```
我：
上周和开发团队开了个会，记录如下：
- 登录流程太复杂，用户抱怨多
- 第三方登录经常失败
- 要加上忘记密码功能
- 预算有限，两周内完成

帮我整理成PRD。

Claude：
[自动加载 prd-generator 技能]

# 登录功能优化 PRD

## 需求背景
当前登录流程存在以下问题：
1. 步骤过多，导致用户流失
2. 第三方登录稳定性差
3. 缺少密码找回渠道

## 需求目标
- 降低登录流失率 30%
- 第三方登录成功率提升至 95%
- 两周内完成开发

## 功能需求
...
```

**场景2：从用户反馈生成需求**

```
我：
用户反馈：
- "每次支付都要重新输入密码，烦死了"
- "能不能记住支付密码？"
- "你们这支付流程是反人类设计"

帮我整理成PRD。

Claude：
[自动加载 prd-generator 技能]

# 支付流程优化 PRD

## 需求背景
用户反馈当前支付流程存在以下痛点：
1. 每次支付需重复输入密码
2. 缺少密码记忆功能
3. 流程繁琐，用户体验差

## 需求目标
- 减少支付步骤
- 提升支付成功率
- 改善用户体验

## 功能需求
### 1. 支付密码记忆功能
- 提供"记住密码"选项
- 支持生物识别（指纹/Face ID）
- 安全加密存储

### 2. 支付流程简化
- 减少不必要步骤
- 优化页面跳转
...
```

### 适用场景

✅ **产品经理**
- 快速产出PRD
- 应对紧急需求
- 统一文档格式

✅ **项目负责人**
- 整理团队讨论结果
- 向上级汇报需求
- 跨团队沟通

✅ **创业者/独立开发者**
- 快速记录想法
- 规划产品功能
- 跟踪开发进度

✅ **技术团队**
- 理解产品需求
- 生成技术任务
- 评估工作量

**真实效率提升**：
- 我之前写PRD，平均1.5小时一个
- 用了这个技能，平均15分钟
- 质量还更稳定（不会漏项）

---

## 三、技能二：PDF处理器 —— 告别"PDF魔咒"

### 功能介绍

提到PDF，你会想到什么？

- 打不开（格式问题）
- 转不了（想提取内容）
- 改不了（想修改一页）
- 合并不了（多个文件要合并）

这就是"PDF魔咒"。

**PDF处理器**技能，能帮你解决90%的PDF问题：

**核心功能**：
- 旋转PDF（扫描件角度不对）
- 提取文本（从PDF复制内容）
- 拆分合并（多个PDF合并成一个）
- 转换格式（PDF转Word、图片）

我最近遇到的场景：

**场景A：扫描件旋转**
```
我扫描了一堆文件，结果都歪了...
用PDF技能，一句话：
"把这些PDF都旋转180度，保持其他不变"
搞定。
```

**场景B：提取内容**
```
客户发来一个PDF，里面有表格数据
我需要把数据提取出来放进Excel
用PDF技能：
"提取第3-5页的表格数据"
结果：准确率95%+
```

**场景C：合并文件**
```
我有10个PDF发票，要合并成一个
用PDF技能：
"合并这10个PDF，按文件名排序"
30秒搞定。
```

### 安装步骤

**从官方仓库安装**：

```bash
cd /path/to/your/project
npx @anthropic-ai/skills install pdf
```

官方已经提供了完整的PDF技能，包含脚本和工具。

### 使用演示

**演示1：旋转PDF**

```
我：
我扫描的PDF文件都是倒着的，文件名是 scan-001.pdf 到 scan-010.pdf

Claude：
[自动加载 pdf 技能]

我来帮你旋转这些PDF文件。

[执行旋转操作]
✓ 已处理 scan-001.pdf
✓ 已处理 scan-002.pdf
...
✓ 已处理 scan-010.pdf

所有文件已旋转180度，保存在当前目录。
```

**演示2：提取文本**

```
我：
从 contract.pdf 中提取所有邮箱地址

Claude：
[自动加载 pdf 技能]

正在读取 contract.pdf...

找到以下邮箱地址：
1. john@example.com
2. sarah@test.com
3. support@company.com

共找到 3 个邮箱地址。
```

**演示3：合并PDF**

```
我：
把 invoice-001.pdf 到 invoice-012.pdf 合并成一个文件，按顺序排列

Claude：
[自动加载 pdf 技能]

正在合并PDF文件...
✓ 已加载 12 个文件
✓ 按文件名排序完成
✓ 合并完成

输出文件：merged-invoices.pdf
```

### 适用场景

✅ **办公人员**
- 处理扫描文件
- 整理文档档案
- 提取报告数据

✅ **财务/会计**
- 合并发票PDF
- 提取财务数据
- 处理报销单据

✅ **研究人员**
- 提取论文内容
- 整理文献资料
- 转换引用格式

✅ **内容创作者**
- 从PDF提取素材
- 转换文档格式
- 整理参考资料

**我的真实体验**：

之前处理PDF，要么开Adobe Acrobat（慢、贵），要么找在线工具（不安全、有广告）。

现在用Claude的PDF技能：
- 快（命令行直接操作）
- 安全（本地处理）
- 免费（开源工具）

效率提升至少3倍。

---

## 四、技能三：代码审查器 —— 你的24/7代码审查专家

### 功能介绍

代码审查（Code Review）是开发流程中重要但耗时的一环。

**理想状态**：
- 同事仔细看你的代码
- 提出建设性意见
- 你学到新东西
- 代码质量提升

**现实状态**：
- 同事很忙，随便看看
- "LGTM"（Looks Good To Me）
- 你不知道有没有问题
- 上线后bug频发

**代码审查器技能**，是你的24/7代码审查专家：

**核心功能**：
- **安全性检查**：SQL注入、XSS、敏感信息泄露
- **性能分析**：O(n²)算法、内存泄漏、N+1查询
- **可维护性**：命名规范、代码重复、复杂度
- **最佳实践**：错误处理、边界条件、类型安全

我最近写了一段代码，让代码审查器看了看：

**我的代码**：
```python
def get_user_orders(user_id):
    query = f"SELECT * FROM orders WHERE user_id = {user_id}"
    results = db.execute(query)
    return results
```

**审查器反馈**：
```markdown
# 代码审查报告

## 🔴 严重问题

### 1. SQL注入漏洞
- **位置**：第2行
- **问题**：使用字符串拼接构建SQL查询
- **风险**：用户可以注入恶意SQL代码
- **修复**：使用参数化查询
```python
# 修复后
def get_user_orders(user_id):
    query = "SELECT * FROM orders WHERE user_id = %s"
    results = db.execute(query, (user_id,))
    return results
```

## 🟡 性能问题

### 1. 缺少索引提示
- **建议**：确保 user_id 字段有索引

### 2. SELECT * 可能不必要
- **建议**：只查询需要的字段

## 📝 最佳实践

### 1. 添加错误处理
```python
def get_user_orders(user_id):
    try:
        query = "SELECT * FROM orders WHERE user_id = %s"
        results = db.execute(query, (user_id,))
        return results
    except Exception as e:
        logger.error(f"Failed to get orders: {e}")
        return []
```
```

看完我一身冷汗。

SQL注入漏洞... 如果这段代码上线了，后果不堪设想。

### 安装步骤

创建 `.claude/skills/code-reviewer/SKILL.md`：

```markdown
---
name: code-reviewer
description: 审查代码的安全性、性能、可维护性，提供具体改进建议
---

# 代码审查器

## 审查维度

### 1. 安全性
- SQL注入
- XSS漏洞
- 敏感信息泄露
- 权限检查

### 2. 性能
- 算法复杂度
- 数据库查询优化
- 缓存策略
- 内存使用

### 3. 可维护性
- 命名规范
- 代码重复
- 复杂度控制
- 注释质量

### 4. 最佳实践
- 错误处理
- 边界条件
- 类型安全
- 测试覆盖

## 审查流程
1. 分析代码结构
2. 识别潜在问题
3. 按严重程度分级
4. 提供具体修复建议
5. 给出修复示例代码

## 输出格式
- 🔴 严重问题（必须修复）
- 🟡 性能问题（建议优化）
- 📝 最佳实践（改进建议）
```

### 使用演示

**演示1：审查API代码**

```
我：
审查这段API代码：

```python
@app.route('/api/user/<int:user_id>', methods=['DELETE'])
def delete_user(user_id):
    user = User.query.get(user_id)
    user.delete()
    return jsonify({'success': True})
```

Claude：
[自动加载 code-reviewer 技能]

# 代码审查报告

## 🔴 严重问题

### 1. 缺少权限验证
- **问题**：任何人都可以删除任何用户
- **风险**：严重安全漏洞
- **修复**：
```python
@app.route('/api/user/<int:user_id>', methods=['DELETE'])
@login_required
def delete_user(user_id):
    if current_user.id != user_id and not current_user.is_admin:
        return jsonify({'error': 'Unauthorized'}), 403

    user = User.query.get_or_404(user_id)
    user.delete()
    return jsonify({'success': True})
```

### 2. 用户不存在未处理
- **问题**：User.query.get() 可能返回 None
- **风险**：AttributeError
- **修复**：使用 get_or_404()

## 🟡 性能问题

### 1. 缺少日志记录
- **建议**：记录删除操作，便于审计

## 📝 最佳实践

### 1. 返回更详细的信息
```python
return jsonify({
    'success': True,
    'message': f'User {user_id} deleted successfully'
})
```
```

**演示2：审查前端代码**

```
我：
审查这段React代码：

```javascript
function UserList() {
  const [users, setUsers] = useState([]);

  useEffect(() => {
    fetch('/api/users')
      .then(res => res.json())
      .then(data => setUsers(data));
  }, []);

  return (
    <div>
      {users.map(user => (
        <div key={user.id}>{user.name}</div>
      ))}
    </div>
  );
}
```

Claude：
[自动加载 code-reviewer 技能]

# 代码审查报告

## 🟡 性能问题

### 1. 缺少错误处理
- **问题**：fetch 失败时没有错误提示
- **修复**：
```javascript
useEffect(() => {
  const fetchUsers = async () => {
    try {
      const res = await fetch('/api/users');
      if (!res.ok) throw new Error('Failed to fetch');
      const data = await res.json();
      setUsers(data);
    } catch (error) {
      console.error('Error fetching users:', error);
      // 可以设置错误状态
    }
  };
  fetchUsers();
}, []);
```

### 2. 缺少加载状态
- **建议**：添加 loading 提升用户体验

## 📝 最佳实践

### 1. 添加PropTypes或TypeScript
```javascript
// 使用 PropTypes
UserList.propTypes = {
  // 如果有props
};

// 或使用 TypeScript
interface User {
  id: number;
  name: string;
}

function UserList() {
  const [users, setUsers] = useState<User[]>([]);
  // ...
}
```

### 2. 考虑内存优化
- **建议**：如果用户列表很长，考虑虚拟滚动
```

### 适用场景

✅ **个人开发者**
- 自查代码质量
- 学习最佳实践
- 避免低级错误

✅ **小团队**
- 代码审查人力不足
- 统一代码规范
- 提升代码质量

✅ **学习编程**
- 理解常见问题
- 学习写法改进
- 养成好习惯

✅ **开源项目**
- 自动化PR审查
- 保持代码质量
- 降低维护成本

**我的使用体验**：

现在每次写完代码，我都会让审查器看一眼。

- 有时发现安全问题（吓一身冷汗）
- 有时发现性能优化点（学习新技巧）
- 有时只是确认代码没问题（安心）

就像有个经验丰富的同事随时在旁边。

**效率对比**：
- 手动审查：需要仔细看，容易遗漏，30分钟+
- AI审查：2分钟，覆盖全面，还能学习

---

## 五、技能四：API文档生成器 —— 从代码到文档，一键搞定

### 功能介绍

写API文档，是程序员最讨厌的任务之一（排名仅次于写注释和写测试）。

**为什么讨厌**：
- 耗时（写代码1小时，写文档2小时）
- 枯燥（重复劳动）
- 容易过时（改了代码忘更新文档）

**API文档生成器技能**，帮你自动从代码生成规范的API文档。

**核心功能**：
- 解析代码中的API定义
- 生成OpenAPI/Swagger规范
- 自动提取参数、返回值、错误码
- 支持多种格式（Markdown、HTML、JSON）

我最近写了一个用户认证API：

**我的代码**：
```python
@app.route('/api/auth/register', methods=['POST'])
def register():
    """
    用户注册接口
    """
    data = request.get_json()
    username = data.get('username')
    email = data.get('email')
    password = data.get('password')

    if not username or not email or not password:
        return jsonify({'error': 'Missing fields'}), 400

    if User.query.filter_by(username=username).first():
        return jsonify({'error': 'Username exists'}), 409

    user = User(username=username, email=email)
    user.set_password(password)
    db.session.add(user)
    db.session.commit()

    return jsonify({
        'user_id': user.id,
        'username': user.username,
        'email': user.email
    }), 201
```

**生成的文档**：
```markdown
# API 文档

## 用户注册

### 请求
- **方法**: POST
- **路径**: `/api/auth/register`
- **Content-Type**: `application/json`

### 请求参数
| 参数 | 类型 | 必填 | 说明 |
|------|------|------|------|
| username | string | 是 | 用户名（唯一） |
| email | string | 是 | 邮箱地址 |
| password | string | 是 | 密码 |

### 请求示例
```json
{
  "username": "john_doe",
  "email": "john@example.com",
  "password": "secure_password123"
}
```

### 响应

#### 成功（201）
```json
{
  "user_id": 123,
  "username": "john_doe",
  "email": "john@example.com"
}
```

#### 错误 - 缺少参数（400）
```json
{
  "error": "Missing fields"
}
```

#### 错误 - 用户名已存在（409）
```json
{
  "error": "Username exists"
}
```

### 注意事项
- 用户名必须唯一
- 密码应该使用HTTPS传输
- 密码会在服务端加密存储
```

看完我服了。

这文档比我手写的还规范。

### 安装步骤

创建 `.claude/skills/api-doc-generator/SKILL.md`：

```markdown
---
name: api-doc-generator
description: 从代码自动生成API文档，支持OpenAPI/Swagger规范
---

# API 文档生成器

## 支持的框架
- Flask
- Express.js
- FastAPI
- Django REST Framework

## 生成内容
- 接口路径和方法
- 请求参数（路径参数、查询参数、请求体）
- 响应格式（成功、各种错误情况）
- 请求/响应示例
- 注意事项

## 输出格式
- Markdown（适合文档网站）
- OpenAPI 3.0（适合导入Swagger）
- HTML（适合直接浏览）

## 使用方式
1. 提供API代码
2. 说明框架类型
3. 自动生成文档
```

### 使用演示

**演示1：生成Flask API文档**

```
我：
为这个Flask应用生成API文档：

```python
from flask import Flask, request, jsonify
app = Flask(__name__)

@app.route('/api/posts', methods=['GET'])
def get_posts():
    page = request.args.get('page', 1, type=int)
    per_page = request.args.get('per_page', 10, type=int)
    # ... 查询逻辑
    return jsonify(posts)

@app.route('/api/posts', methods=['POST'])
def create_post():
    data = request.get_json()
    title = data.get('title')
    content = data.get('content')
    # ... 创建逻辑
    return jsonify(post), 201

@app.route('/api/posts/<int:post_id>', methods=['GET'])
def get_post(post_id):
    post = Post.query.get_or_404(post_id)
    return jsonify(post.to_dict())
```

Claude：
[自动加载 api-doc-generator 技能]

# Flask API 文档

## 1. 获取文章列表

### 请求
- **方法**: GET
- **路径**: `/api/posts`

### 查询参数
| 参数 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| page | integer | 1 | 页码 |
| per_page | integer | 10 | 每页数量 |

### 响应示例
```json
{
  "posts": [
    {
      "id": 1,
      "title": "First Post",
      "content": "..."
    }
  ],
  "total": 100,
  "page": 1,
  "per_page": 10
}
```

## 2. 创建文章

### 请求
- **方法**: POST
- **路径**: `/api/posts`
- **Content-Type**: `application/json`

### 请求体
| 参数 | 类型 | 必填 | 说明 |
|------|------|------|------|
| title | string | 是 | 文章标题 |
| content | string | 是 | 文章内容 |

### 请求示例
```json
{
  "title": "My Post",
  "content": "Post content here"
}
```

### 响应（201）
```json
{
  "id": 101,
  "title": "My Post",
  "content": "Post content here",
  "created_at": "2025-01-18T10:30:00Z"
}
```

## 3. 获取单篇文章

### 请求
- **方法**: GET
- **路径**: `/api/posts/{post_id}`

### 路径参数
| 参数 | 类型 | 说明 |
|------|------|------|
| post_id | integer | 文章ID |

### 响应（200）
```json
{
  "id": 1,
  "title": "First Post",
  "content": "...",
  "author": {
    "id": 10,
    "name": "John"
  },
  "created_at": "2025-01-18T10:00:00Z"
}
```

### 错误响应（404）
```json
{
  "error": "Post not found"
}
```
```

**演示2：生成Express.js API文档**

```
我：
生成这个Express API的文档：

```javascript
app.post('/api/auth/login', async (req, res) => {
  const { email, password } = req.body;

  if (!email || !password) {
    return res.status(400).json({ error: 'Email and password required' });
  }

  const user = await User.findOne({ email });
  if (!user || !user.comparePassword(password)) {
    return res.status(401).json({ error: 'Invalid credentials' });
  }

  const token = user.generateToken();
  res.json({ user, token });
});

app.get('/api/users/:userId', async (req, res) => {
  const user = await User.findById(req.params.userId);
  if (!user) {
    return res.status(404).json({ error: 'User not found' });
  }
  res.json(user);
});
```

Claude：
[自动加载 api-doc-generator 技能]

# Express.js API 文档

## 认证登录

### POST /api/auth/login

登录接口，验证用户身份并返回访问令牌。

**请求体**:
```json
{
  "email": "user@example.com",
  "password": "password123"
}
```

**响应 (200)**:
```json
{
  "user": {
    "id": "507f1f77bcf86cd799439011",
    "email": "user@example.com",
    "name": "John Doe"
  },
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
}
```

**错误响应**:

400 (缺少参数):
```json
{
  "error": "Email and password required"
}
```

401 (凭据无效):
```json
{
  "error": "Invalid credentials"
}
```

## 获取用户信息

### GET /api/users/:userId

根据用户ID获取用户详细信息。

**路径参数**:
- `userId` (string): 用户ID

**响应 (200)**:
```json
{
  "id": "507f1f77bcf86cd799439011",
  "email": "user@example.com",
  "name": "John Doe",
  "createdAt": "2025-01-01T00:00:00Z"
}
```

**错误响应 (404)**:
```json
{
  "error": "User not found"
}
```
```

### 适用场景

✅ **后端开发**
- 快速生成API文档
- 同步更新文档
- 团队协作

✅ **前端开发**
- 了解后端接口
- 生成Mock数据
- 联调前准备

✅ **全栈开发者**
- 自给自足
- 保持文档最新
- 提升开发效率

✅ **技术文档写作**
- 自动化文档生成
- 格式统一
- 易于维护

**真实效率提升**：

之前写API文档：
- 手写文档：2小时
- 容易出错、容易过时
- 改代码后懒得更新文档

现在：
- 自动生成：5分钟
- 准确无误
- 改代码重新生成即可

时间节省：95%

---

## 六、技能五：小红书文案生成器 —— 种草文案，秒生成

### 功能介绍

前四个技能都是开发工具，这个技能面向内容创作者。

**小红书文案生成器**，帮你快速生成符合小红书风格的"种草文案"。

**核心功能**：
- 分析产品/服务特点
- 生成吸引人的标题
- 符合小红书调性的正文
- 自动添加标签（hashtag）
- 表情符号点缀

我试了一下：

**输入**：
```
产品：智能手表
特点：续航14天、50米防水、心率监测、睡眠追踪、价格599元
目标：年轻女性，健身爱好者
```

**输出**：
```markdown
标题：
✨挖到宝了！这款599的智能手表真的香哭了😭

正文：
姐妹们！今天必须给你们安利这个神仙智能手表！🙌

作为一个健身党，一直想找个靠谱的运动手表，但是动不动就2000+的价格真的劝退... 直到我遇到了它！💕

🔋【续航真的绝】
充一次电能用14天！14天啊姐妹们！再也不用天天充电了，出差旅行完全不用担心～

💧【游泳也能戴】
50米防水，游泳洗澡都不用摘！之前的手表一到洗手就要摘下来，烦死...

💗【健康管理很贴心】
心率监测、睡眠追踪都有，特别是睡眠分析，每天都督促我早睡（虽然很难做到😂）

💰【性价比天花板】
最绝的是价格！只要599！599啊！省下的钱可以买好多健身装备了～

⚠️【小缺点】
外观比较简约，喜欢花里胡哨的姐妹可能不太喜欢... 但我其实还挺喜欢的！简单耐看～

#智能手表推荐 #运动手表 #性价比 #健身装备 #好物分享 #学生党必备 #平价好物

💡购买建议：趁活动入手更划算！
```

看完我服了。

这语气、这表情、这标签，完全就是小红书那味儿啊！

### 安装步骤

创建 `.claude/skills/xiaohongshu-writer/SKILL.md`：

```markdown
---
name: xiaohongshu-writer
description: 生成符合小红书风格的种草文案，包括标题、正文、标签
---

# 小红书文案生成器

## 文案特点
- 真实分享感（像朋友推荐）
- 情绪化表达（激动、惊喜）
- 具体细节（不说空话）
- 表情符号点缀
- 话题标签（hashtag）

## 文案结构
1. 吸引人的标题（带数字、表情、悬念）
2. 开头引入（真实场景/痛点）
3. 产品特点（分点说明）
4. 个人体验（真实感受）
5. 小缺点（增加可信度）
6. 购买建议
7. 相关标签

## 使用方式
1. 提供产品/服务信息
2. 说明目标用户
3. 强调核心卖点
4. 自动生成文案
```

### 使用演示

**演示1：美妆产品**

```
我：
帮我写个小红书文案：

产品：精华液
品牌：XX品牌（虚构）
核心卖点：烟酰胺5%、美白淡斑、28天见效、价格199
目标用户：20-30岁女性，有美白需求

Claude：
[自动加载 xiaohongshu-writer 技能]

**标题**：
🌙坚持用了28天，黄黑皮逆袭冷白皮！这款精华真的绝了✨

**正文**：
姐妹们！我要吹爆这款精华！🎉

先说下我皮肤情况：混干皮、黄二白、脸颊有晒斑👻

用了一个月，最直观的感受：
👉 脸颊的晒斑真的淡了！不是心理作用，我妈都说我变白了！
👉 肤色均匀了好多，不像之前暗沉发黄
👉 上脸吸收很快，不粘腻！

📝【使用感受】
质地是清爽水润型的，滴管设计很卫生
我一般是早晚各用一次，先爽肤水再精华再面霜
第一周没啥感觉，用到第三周开始明显变白！

⚠️【要注意】
- 烟酰胺要建立耐受，敏感肌先从低浓度开始
- 白天一定要防晒！不然会反黑
- 怀孕/哺乳期姐妹慎用

💰【性价比】
199元30ml，对比大牌真的很划算
学生党、贫民窟女孩完全可以冲！

#美白精华 #护肤分享 #烟酰胺 #好物推荐 #学生党护肤 #美白 #冷白皮 #平价好物

💡小tips：配合VC精华效果更好！
```

**演示2：健身产品**

```
我：
小红书文案：

产品：瑜伽垫
特点：TPE材质、加厚10mm、防滑、送背带、价格89
目标：瑜伽初学者、居家健身

Claude：
[自动加载 xiaohongshu-writer 技能]

**标题**：
🧘‍♀️居家健身党必入！这款89的瑜伽垫太香了！

**正文**：
终于开始在家练瑜伽了！🏠

选瑜伽垫做了好多功课，最后入了这款，用下来真的惊喜～

✅【厚度刚好】
10mm加厚，跪姿动作膝盖不疼
之前用薄的瑜伽垫，每次做猫牛式膝盖都要废了😭

✅【防滑效果好】
出汗了也不打滑，做下犬式很稳
这点太重要了！安全第一！

✅【材质环保】
TPE材质，没有异味
开袋就能用，不用晾半天～

✅【送背带】
背着去瑜伽馆很方便，收纳也容易

💰【价格】
89块钱还要啥自行车！
对比瑜伽馆一次课的钱，这垫子能用一年，值！

📌【小建议】
- 新垫子第一次用可能会有点滑，用几次就好了
- 铺的时候有logo的那面朝下（我第一次搞反了😂）

#瑜伽垫推荐 #居家健身 #瑜伽初学者 #运动装备 #好物分享 #学生党必备

💪现在每天早上起床先练30分钟，感觉整个人都精神了！
```

**演示3：数码产品**

```
我：
小红书文案：

产品：蓝牙耳机
特点：主动降噪、30小时续航、IPX5防水、延迟低、价格299
目标：学生党、通勤族

Claude：
[自动加载 xiaohongshu-writer 技能]

**标题**：
🎧戴了这款耳机，地铁上再也不用听别人打电话了！

**正文**：
通勤族的痛我懂！🚇

每天地铁上：
外放刷抖音的😒
大声打电话的😒
小孩哭闹的😒

直到我入了这款降噪耳机！世界清静了～

🔇【降噪真的牛】
开启降噪，地铁上的噪音直接消失
有时候到站了都没注意到，坐过站好几次😂

🔋【续航超给力】
充一次电能用好久，我一周充一次就够了
充电仓还能当应急充电宝（虽然只能充一点点）

💧【防水不怕汗】
IPX5防水，下雨天、健身出汗都不怕
夏天戴着出门完全OK

🎮【打游戏延迟低】
打王者吃鸡延迟感知不到
比我有线耳机还流畅

⚠️【小缺点】
- 戴久了耳朵有点闷（降噪耳机通病）
- 充电仓有点大，小口袋不好装

💰【性价比】
299这个配置，真的找不出第二款了
学生党完全可以冲！

#蓝牙耳机 #降噪耳机 #通勤必备 #学生党好物 #数码推荐 #平价耳机

💡想体验降噪又不想花大几千的姐妹，闭眼冲这个！
```

### 适用场景

✅ **品牌/商家**
- 快速生成产品文案
- 批量生成多版本
- A/B测试不同文案

✅ **内容创作者**
- 提高创作效率
- 保持风格统一
- 应对多平台发布

✅ **带货博主**
- 种草文案模板
- 快速响应热点
- 节省创作时间

✅ **个人分享**
- 推荐好物
- 分享体验
- 记录生活

**真实效率提升**：

我之前帮朋友写小红书文案：
- 手写一篇：30-60分钟
- 还要琢磨语气、加表情、想标签

现在：
- 5分钟生成初稿
- 稍微修改就能用
- 批量生成多个版本

时间节省：90%

---

## 七、如何探索更多技能？

这5个技能是我精挑细选的"必装清单"，但Claude Skills的生态远不止于此。

### 官方技能库

**GitHub官方仓库**：
https://github.com/anthropics/skills

**包含技能**（16+个）：
- 文档处理：docx, pdf, pptx, xlsx
- 开发辅助：testing-web-apps, mcp-server-generator
- 创意设计：ascii-art, music
- 工作流：discussion-organizer, srt-workflow

**安装命令**：
```bash
npx @anthropic-ai/skills install <skill-name>
```

### Awesome Claude Skills

这是一个社区维护的精选技能列表：

**地址**：https://jimmyang.io/zh/ai/awesome-claude-skills/

**分类**：
- 文档处理类
- 开发辅助类
- 数据分析类
- 创意媒体类
- 自动化工作流

### 社区贡献

**发现新技能的地方**：
- GitHub（搜索 "claude skills"）
- Reddit r/Claude
- Twitter/X（#ClaudeSkills）
- 技术博客和教程

**贡献自己的技能**：
如果你创建了好用的技能，可以考虑开源到GitHub：
1. 创建仓库
2. 按官方规范组织文件
3. 编写README说明
4. 分享到社区

---

## 八、总结与下篇预告

### 核心要点回顾

**5个必装技能**：

| 技能 | 核心价值 | 适用人群 | 效率提升 |
|------|---------|---------|---------|
| PRD生成器 | 需求文档自动化 | 产品经理、项目负责人 | 5-10倍 |
| PDF处理器 | PDF问题一站式解决 | 办公人员、财务、研究者 | 3-5倍 |
| 代码审查器 | 24/7代码审查专家 | 开发者、学习编程者 | 防止严重bug |
| API文档生成器 | 代码→文档一键生成 | 后端/前端/全栈开发者 | 95%时间节省 |
| 小红书文案生成器 | 种草文案秒生成 | 内容创作者、带货博主 | 90%时间节省 |

**为什么这5个"必装"**：
1. 实用性强（解决真实痛点）
2. 适用面广（覆盖多个场景）
3. 效果显著（能直接感受效率提升）
4. 稳定可靠（官方或经过验证）

**安装建议**：
- 不需要全部装（按需选择）
- 先装1-2个最相关的
- 用熟练了再扩展

### 系列文章进度

✅ **第1篇**：《什么是 Skills，为什么你需要它》
✅ **第2篇**：《5分钟上手 Claude Skills》
✅ **第3篇**：《Skills vs 斜杠命令 vs MCP》
✅ **第4篇**：《渐进式披露的核心机制》
✅ **第5篇**：《SKILL.md 编写指南》
✅ **第6篇**：《高级组织模式》
✅ **第7篇**：《实战案例分析》
✅ **第8篇**：《5个必装的Claude Skills》（本篇）
⏳ **第9篇**：《从零创建自定义技能》（待发布）
⏳ **第10篇**：《Claude Skills 生态与未来》（待发布）

### 下篇预告

**第9篇**：《从零创建自定义技能：六步完整流程》

前8篇我们学了：
- 概念和机制
- 使用现有技能
- 高级技巧

第9篇，我们将进入**创造阶段**：

**六步流程**：
1. **需求澄清**：你到底需要什么技能？
2. **结构规划**：如何设计技能架构？
3. **SKILL.md编写**：核心指令怎么写？
4. **辅助资源**：references和scripts如何组织？
5. **测试优化**：如何验证技能效果？
6. **迭代改进**：如何持续优化？

**实战案例**：
我们将一起从零创建一个实用技能，让你掌握：
- 技能设计的完整思路
- 常见坑点和解决方案
- 优化技巧和最佳实践

**预期收获**：
- 能独立创建自定义技能
- 解决你自己的特定需求
- 甚至可以贡献给社区

敬请期待！

---

## 九、参考文档

### 官方文档
- **Agent Skills 官方文档**（中文）：https://platform.claude.com/docs/zh-CN/agents-and-tools/agent-skills/overview
- **Agent Skills 官方文档**（英文）：https://platform.claude.com/docs/en/agents-and-tools/agent-skills/overview
- **GitHub 官方仓库**：https://github.com/anthropics/skills
  - 官方技能集合和示例
  - 技能模板
  - 完整规范文档

### 社区资源
- **Awesome Claude Skills**（精选技能列表）：https://jimmyang.io/zh/ai/awesome-claude-skills/
- **Agent Skills 权威中文指南**：https://github.com/libukai/awesome-agent-skills

### 相关教程
- **知乎专栏 - 终于有人把 Claude Skills 官方教程讲清楚了**：https://zhuanlan.zhihu.com/p/1987581624360145862
- **火山引擎 - Claude Skills 终极指南**：https://developer.volcengine.com/articles/7577301013976383498
- **Claudecn.com - Skills 架构拆解**：https://claudecn.com/blog/claude-skills-architecture/

### 技能模板
- **官方 PRD 生成器模板**：https://github.com/anthropics/skills/tree/main/skills/prd-generator
- **官方 PDF 处理器模板**：https://github.com/anthropics/skills/tree/main/skills/pdf
- **社区代码审查器示例**：https://github.com/anthropics/skills/tree/main/skills/code-reviewer

---

**下一篇文章**：《从零创建自定义技能：六步完整流程》

我们将进入创造阶段，手把手带你打造自己的专属技能。敬请期待！

---

> 本文是「Claude Code Skills 教程系列」的第 8 篇。
> 系列目录：[查看完整目录](待补充)
> 素材库：[Claude-Code-Skills教程素材库.md](../_personal_materials/Claude-Code-Skills教程素材库.md)
>
> 有问题或建议？欢迎在评论区留言，或在公众号后台与我交流。

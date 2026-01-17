---
name: mp-wechat-flow
description: 微信公众号写作完整流程（10步）。用于公众号文章写作任务，包含brief创建、调研、选题讨论、素材库使用、创意排水、写作、审校、标题拟定、配图等全流程。
---

# 微信公众号写作流程

> **版本**: v1.3 | **平台**: 微信公众号
> **字数**: 1500-3000字 | **配图**: 推荐5-8张

---

## 🚨 首要原则（最高优先级）

**必须严格按照规则执行完整流程，不得跳过任何标记为⭐的关键步骤。**

### 关键步骤检查清单

1. ✅ **Step 2: 知识库** - 搜索后必须保存到 `_knowledge_base/`
2. ✅ **Step 3: 选题讨论** ⭐⭐⭐ - **绝不直接写文章**，必须先提供3-4个选题方案
3. ✅ **Step 4: 协作文档** - 需要测试时必须创建
4. ✅ **Step 5.5: 个人素材库** ⭐⭐⭐ - 必须搜索 `_personal_materials/`
5. ✅ **Step 6.5: 创意排水** ⭐ - 推荐执行，重要文章必做
6. ✅ **Step 7: 版本管理** - draft-v1 → v2 → v3 → final
7. ✅ **Step 8: 三遍审校** ⭐⭐⭐ - 内容→风格→细节，每遍创建新版本
8. ✅ **Step 9: 标题拟定** ⭐⭐⭐ - 提供3-5个方案，等待用户选择
9. ✅ **Step 10: 配图** ⭐ - 提供5-8张配图的Prompt（3个版本）

---

## 完整流程（10步）

### Step 1: 理解需求 & 保存Brief ⭐

创建brief文档到 `_briefs/` 文件夹

详细操作：见 [step1-brief.md](steps/step1-brief.md)

### Step 2: 信息搜索与知识管理 ⭐

搜索最新资料，保存到 `_knowledge_base/`

详细操作：见 [step2-research.md](steps/step2-research.md)

### Step 3: 选题讨论 ⭐⭐⭐ （必做）

**绝不要直接写文章！必须先讨论选题！**

提供3-4个选题方向，等待用户选择

详细操作：见 [step3-topic.md](steps/step3-topic.md)

### Step 4: 创建协作文档（如需测试）

需要真实测试时创建协作文档

详细操作：见 [step4-cooperation.md](steps/step4-cooperation.md)

### Step 5: 学习我的风格

阅读 `_writing_reference/` 提取风格特征

详细操作：见 [step5-writing-style.md](steps/step5-writing-style.md)

### Step 5.5: 使用个人素材库 ⭐⭐⭐ （必做）

从用户真实经历、观点、案例中提取素材

详细操作：见 [step55-materials.md](steps/step55-materials.md)

### Step 6: 等待测试数据（如需）

如需测试，等待用户提供数据

### Step 6.5: 创意排水 ⭐ （推荐）

先排空"废水"（套路想法），再写"清水"（独特创意）

详细操作：见 [step65-creative-drain.md](steps/step65-creative-drain.md)

### Step 7: 创作初稿

基于真实数据和"清水"创意写作

详细操作：见 [step7-writing.md](steps/step7-writing.md)

### Step 8: 三遍审校 ⭐⭐⭐ （最关键）

- 第一遍：内容审校（逻辑、事实、结构）
- 第二遍：风格审校（降AI味）
- 第三遍：细节打磨（标点、排版、节奏）

详细操作：见 [step8-review.md](steps/step8-review.md)

### Step 9: 标题拟定 ⭐⭐⭐

提供3-5个标题方案，等待用户选择

详细操作：见 [step9-titles.md](steps/step9-titles.md)

### Step 10: 文章配图 ⭐

提供5-8张配图的Prompt（3个版本）

详细操作：见 [step10-images.md](steps/step10-images.md)

---

## 简化流程（特殊情况）

### 修改已有文章

```
读取原文 → 理解需求 → 修改 → 审校（至少第二遍）
```

### 仅审校/降AI味

```
直接进入 Step 8 三遍审校流程
```

---

## 文件结构规范

```
mp-wechat/
├── _briefs/                    # 需求文档
│   └── YYYY-MM-DD-主题-brief.md
├── _knowledge_base/            # 调研资料
│   └── YYYY-MM-DD-主题.md
├── _cooperation/               # 协作文档
│   └── YYYY-MM-DD-主题-协作文档.md
├── _drafts/                    # 草稿
│   ├── YYYY-MM-DD-主题-draft-v1.md
│   ├── YYYY-MM-DD-主题-draft-v2.md
│   ├── YYYY-MM-DD-主题-draft-v3.md
│   └── YYYY-MM-DD-主题-final.md
├── _published/                 # 已发布
│   └── YYYY-MM-DD-主题.md
├── _writing_reference/         # 风格参考
│   ├── 风格指南.md
│   └── 历史优质文章/
├── _personal_materials/        # 个人素材库
│   ├── X平台内容/
│   ├── 小红书内容/
│   └── 公众号历史文章/
└── images/                     # 配图
    └── 主题关键词/
        ├── image-1.png
        └── prompts.md
```

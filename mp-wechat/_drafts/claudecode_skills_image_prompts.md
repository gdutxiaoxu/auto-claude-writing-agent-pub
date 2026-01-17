# 配图 Prompt 方案

## 配图计划（7张）

### 1. Skills 概念示意图
**用途**：文章开篇，解释 Skills 的概念
**位置**：在"Skills 是什么？"章节后

**版本 A（Midjourney v6）：**
```
minimalist illustration of a robot brain being upgraded with modular plugin cards, each card represents a skill or capability, clean white background, tech aesthetic, soft blue and purple gradients, --style raw --v 6
```

**版本 B（DALL-E 3）：**
```
A simple, clean illustration showing an AI assistant receiving "skill cards" that teach it new capabilities. The concept of installing plugins into a robot brain, represented visually as modular cards being inserted. Minimalist tech style, soft colors, white background.
```

**版本 C（Stable Diffusion XL）：**
```
minimalist tech illustration, robot brain with modular plugin cards, concept of AI learning through addons, clean aesthetic, soft blue purple colors, white background, high quality
```

---

### 2. 第一个 Skill 的文件结构
**用途**：展示最简单的 Skill 文件结构
**位置**：在"第一个 Skill：commit message 生成器"章节

**版本 A（Midjourney v6）：**
```
clean code editor screenshot showing a simple file structure, a single markdown file named SKILL.md in a folder, minimal interface, syntax highlighting, --style raw --v 6
```

**版本 B（DALL-E 3）：**
```
A clean, minimalist code editor window showing a simple file directory structure. A folder named "commit-helper" containing a single file "SKILL.md". The file is open in the editor showing clean markdown code. Professional IDE aesthetic.
```

**版本 C（Stable Diffusion XL）：**
```
clean code editor interface, file tree on left showing simple folder structure, SKILL.md file open, minimal design, professional IDE look
```

---

### 3. SKILL.md 文件内容示例
**用途**：展示实际的 Skill 文件内容
**位置**：在"SKILL.md 内容"章节后

**版本 A（Midjourney v6）：**
```
close-up of a code editor showing YAML frontmatter and markdown content, clean syntax highlighting, the text shows "name: commit-helper" and "description: generate commit messages", professional code aesthetic, --style raw --v 6
```

**版本 B（DALL-E 3）：**
```
A close-up view of a code editor showing a SKILL.md file. Visible content includes YAML frontmatter with "name:" and "description:" fields, followed by markdown content about commit message standards. Clean syntax highlighting in a modern code editor.
```

**版本 C（Stable Diffusion XL）：**
```
code editor close-up, YAML syntax highlighting, markdown file content showing skill configuration, clean professional look
```

---

### 4. Skill 触发效果对比
**用途**：展示有无 Skill 的效果差异
**位置**：在"效果对比"章节后

**版本 A（Midjourney v6）：**
```
split screen comparison, left side shows generic AI response, right side shows customized AI response following specific standards, visual representation of consistency vs inconsistency, minimalist style, --style raw --v 6
```

**版本 B（DALL-E 3）：**
```
A split-screen comparison illustration. Left side: "Without Skill" showing varied, inconsistent commit messages. Right side: "With Skill" showing uniform, properly formatted commit messages. Clean before/after comparison style with clear visual distinction.
```

**版本 C（Stable Diffusion XL）：**
```
split comparison illustration, inconsistent vs consistent results, visual before and after, clean minimalist style, clear contrast
```

---

### 5. description 字段的重要性
**用途**：说明 description 字段的作用
**位置**：在"核心机制：description 是关键"章节

**版本 A（Midjourney v6）：**
```
abstract illustration showing a search query matching with specific keywords, visual representation of pattern matching, clean infographic style, soft colors, --style raw --v 6
```

**版本 B（DALL-E 3）：**
```
An infographic-style illustration showing the concept of keyword matching. A user's request flowing through and matching with specific trigger words in a skill description. Visual representation of how Claude decides which skill to use. Clean, educational diagram style.
```

**版本 C（Stable Diffusion XL）：**
```
infographic showing pattern matching concept, user request connecting to skill description through keywords, clean educational illustration, soft colors
```

---

### 6. 多文件 Skill 结构
**用途**：展示复杂 Skill 的文件组织
**位置**：在"进阶用法：多文件 Skill"章节

**版本 A（Midjourney v6）：**
```
clean file tree diagram showing a skill folder with multiple files, SKILL.md as the main file, connected to examples.md, reference.md, and scripts folder, showing the progressive disclosure concept, minimal infographic style, --style raw --v 6
```

**版本 B（DALL-E 3）：**
```
A clean file structure diagram showing a multi-file skill organization. Central "SKILL.md" file with visual connections to "examples.md", "reference.md", and a "scripts/" folder. Illustrates the concept of progressive disclosure where additional files are loaded only when needed. Infographic style.
```

**版本 C（Stable Diffusion XL）：**
```
file structure diagram, multi-file skill organization, central SKILL.md with connections to supporting files, infographic style, clean minimal design
```

---

### 7. 团队协作分享
**用途**：展示 Skills 如何在团队中共享
**位置**：在"团队协作"章节

**版本 A（Midjourney v6）：**
```
illustration of multiple developers working together, sharing skill files through a Git repository, concept of team collaboration and knowledge sharing, modern tech workplace aesthetic, diverse team, --style raw --v 6
```

**版本 B（DALL-E 3）：**
```
A modern illustration showing team collaboration. Multiple developers at their computers, with visual representations of skill files being shared through a Git repository. The concept of team standards and knowledge sharing. Clean, professional tech workplace aesthetic with a diverse team.
```

**版本 C（Stable Diffusion XL）：**
```
team collaboration illustration, developers sharing code through Git repository, modern tech workplace, diverse team, professional aesthetic
```

---

## 使用建议

1. **推荐工具**：Midjourney v6（整体效果最佳）
2. **备选工具**：DALL-E 3（细节描述更准确）
3. **快速生成**：Stable Diffusion XL（免费/本地选项）

4. **风格统一**：所有配图保持相同的视觉风格和配色方案
5. **尺寸建议**：16:9 横版，适合公众号配图
6. **色调建议**：以蓝紫色调为主，白色背景，简洁科技感

---

## 快速生成命令（Midjourney）

直接复制以下命令到 Midjourney：

```
1. /imagine minimalist illustration of a robot brain being upgraded with modular plugin cards, each card represents a skill, clean white background, tech aesthetic, soft blue and purple gradients, --style raw --v 6 --ar 16:9

2. /imagine clean code editor screenshot showing a simple file structure, a single markdown file named SKILL.md in a folder, minimal interface, syntax highlighting, --style raw --v 6 --ar 16:9

3. /imagine close-up of a code editor showing YAML frontmatter and markdown content, clean syntax highlighting, the text shows "name: commit-helper" and "description: generate commit messages", professional code aesthetic, --style raw --v 6 --ar 16:9

4. /imagine split screen comparison, left side shows generic AI response, right side shows customized AI response following specific standards, visual representation of consistency vs inconsistency, minimalist style, --style raw --v 6 --ar 16:9

5. /imagine abstract illustration showing a search query matching with specific keywords, visual representation of pattern matching, clean infographic style, soft colors, --style raw --v 6 --ar 16:9

6. /imagine clean file tree diagram showing a skill folder with multiple files, SKILL.md as the main file, connected to examples.md, reference.md, and scripts folder, showing the progressive disclosure concept, minimal infographic style, --style raw --v 6 --ar 16:9

7. /imagine illustration of multiple developers working together, sharing skill files through a Git repository, concept of team collaboration and knowledge sharing, modern tech workplace aesthetic, diverse team, --style raw --v 6 --ar 16:9
```

# Mode: interview

前提：SKILL.md 的 Setup 已跑完（简历、最近 transcripts、weaknesses.md 已在工作记忆里）。

## Step 1 — 一次性收集 4 个参数

用 **一个** AskUserQuestion 调用，4 个 question 并列：

- 目标岗位：options 给 `后端工程师` / `算法 · AI Eng` / `数据工程师` / `产品经理`，其他岗位用户走 Other 自由填（例 "SDE @ FAANG"、"Product Manager 字节"）
- 题型：`behavioral` / `project deepdive` / `mixed`
- 题数：`3` / `5` / `7`
- 面试语言：`跟简历` / `中文` / `English`（默认跟简历；用户选了就覆盖全程语言）

## Step 2 — 建 transcript 文件（出第一题之前）

路径：`<DATA>/sessions/{YYYYMMDD-HHMM}-{role-slug}.md`

- `role-slug`：把岗位名小写化，非字母数字换 `-`，截断到 30 字符。中文保留（`数据工程师` → `数据工程师`），`SDE @ FAANG` → `sde-faang`
- 先只写 frontmatter：

```markdown
---
date: 2026-05-10 14:23
role: 数据工程师
round: project deepdive
resume_file: D:\code repos\personal-website\resume.tex
resume_sha: 3f8a2c1d
n_questions: 3
completed: 0
---
```

**增量写盘（关键）**：每答完一题（含追问和 feedback），立即把该题的完整块 append 到这个文件，并用 Edit 把 frontmatter 的 `completed` 更新。这样 session 中断、上下文被压缩、用户中途喊停，已完成的题都不丢，且回答原文不经过任何压缩。

## Step 3 — 出题循环

逐题进行，**绝对不一次性把所有题列出来**。

### 题目生成规则

- 每道题必须挂在简历某一具体 bullet 上。在脑里记下"这题打的是简历哪一条"
- **优先级 1（最高）**：复问历史弱点。从 `state/weaknesses.md` 找 tag，把对应项目重新挑战一遍。例如 weakness 是 `project:Polymarket盯盘:impact_unclear`，那本次出题就是"上次问你 Polymarket 的实盘收益率 10% 是怎么算出来的，你说不太清——这次详细讲讲样本量、时间窗、对照基准"。tag 来自旧版简历（resume_sha 不一致）→ 先核对该 bullet 还在不在，不在就跳过这个 tag
- **优先级 2**：覆盖简历里 transcripts 里**没被问过**的 bullet。让覆盖面拉开
- **题型规则**：
  - `project deepdive`：盯量化数字 / 技术选型 rationale / 失败教训 / "如果重来怎么改"
  - `behavioral`：用简历事实当锚（"你在 PICC 做事件会诊 agent 时，跨处室的最大阻力是什么？怎么解决的？"），不要泛泛而谈"讲个冲突的例子"
  - `mixed`：交替

### 用户答完后的内审（不要输出给用户，只用来决定追问策略）

按 3 维内审：
- **结构**：有没有 Situation / Task / Action / Result 四段？还是直接跳进 Action？
- **具体度**：有没有数字、人名、时间、技术栈？还是空话？
- **深度**：有没有 root cause / tradeoff / "为什么不选别的方案"？

### 追问策略

- 任一维度明显薄弱 → 追问 1 次（最多 2 次），针对该维度发问。例：
  - 结构薄弱 → "等等先回到背景——这件事发生在什么阶段？谁让你做的？"
  - 具体度薄弱 → "60% 提速——baseline 是多少？怎么测的？"
  - 深度薄弱 → "为什么选 Selenium 而不是直接 API？当时考虑过 API 吗？"
- 三维都过关 → 简短认可一句（"清楚，下一题"），进下一题
- **追问也不到位** → weakness tag 升级为 `:cant_articulate`，然后下一题

### 每题的 transcript 块（答完即 append）

```markdown
## Q1: <题目原文>
**Targets bullet**: <这题打的是简历哪条，照抄简历原文关键词>

### Answer
<用户原始回答原文>

### Followups
- Q1.1: <第一次追问>
  - Answer: <用户答>
- Q1.2: <第二次追问，如有>
  - Answer: <用户答>

### Coach feedback
- 结构：<具体观察，例 "跳过 Situation，听众抓不住背景">
- 具体度：<具体观察>
- 深度：<具体观察>

### Weakness tags
- project:小红书自动运营:metric_ambiguous

---
```

### Weakness tag 词表（封闭，禁止自创后缀）

格式：`{project|behavioral}:{锚点}:{后缀}`。锚点 = 项目 / 经历名，**照抄简历用词**（保证跨 session 字符串一致）。后缀只能从这份词表选：

| 后缀 | 含义 |
|---|---|
| `impact_unclear` | 说不清结果 / 收益怎么来的 |
| `metric_ambiguous` | 数字口径模糊（分子分母、时间窗、基准不明） |
| `no_structure` | 缺 STAR 结构，直接跳进 Action |
| `tech_choice_no_rationale` | 技术选型说不出为什么 |
| `no_tradeoff` | 说不出 tradeoff / 备选方案 |
| `no_failure_lesson` | 说不出失败点 / 教训 / "重来怎么改" |
| `ownership_unclear` | 个人贡献和团队贡献分不开 |
| `cant_articulate` | 追问后仍说不清（升级用，替换本题原 tag） |

### 用户中途喊停

- 用 Edit 在 frontmatter 加 `interrupted: true`
- 已答完的题照常走 Step 4 / Step 5，不作废

## Step 4 — 更新 weakness 累积文件

文件：`<DATA>/state/weaknesses.md`。对本次每个 tag：

- 文件里**已有**同名 `## <tag>` 小节 → 在该小节下追加一行 `- <date> mock <Q编号>`
- **没有** → 新建小节 + 第一行引用

```markdown
# Weaknesses (auto-tracked)

## project:Polymarket盯盘:impact_unclear
- 2026-04-12 mock Q3
- 2026-05-10 mock Q1

## project:小红书自动运营:metric_ambiguous
- 2026-05-10 mock Q2
```

引用行数 = 该弱点被打中的次数，debrief 和 polish 都靠它计频。

## Step 5 — 简短收尾

告诉用户：transcript 已写到哪里、识别出几个新 weakness tag、推荐下次怎么练（如 "下次专攻 polymarket 项目的量化表述"）。**不要**在这里同时给 polish 建议——那是 polish 模式的事。

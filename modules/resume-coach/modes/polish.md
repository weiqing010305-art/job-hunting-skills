# Mode: polish

前提：SKILL.md 的 Setup 已跑完（简历、最近 transcripts、weaknesses.md 已在工作记忆里）。

## Step 1 — 工作记忆就位

Setup 阶段已经把简历、最近 5 transcripts、weaknesses.md 读进来了，直接用。

## Step 2 — 按简历章节扫描

按简历自然章节顺序（教育 → 独立产品 → 工作经历 → 技能 → 其他）。每节给出一组建议。

## Step 3 — 每条建议必须分类标级

### A 级（来自 interview 历史）

- 模板：`[A] [{session_filename} {Q编号}] {weakness tag} → 改动：{具体改法}`
- 例：`[A] [20260412-1430-数据工程师.md Q3] project:Polymarket盯盘:impact_unclear → 改 bullet 加 "实盘 3 个月、对照大盘 -2%、收益率 10%+"`
- A 级必须能在 transcripts 里找到出处，**不能编**
- 出处 session 不在已读的最近 5 份里（weaknesses.md 引用了更早的）→ 按文件名**补读那一份**核实后再引用；文件缺失或核实不到 → 降为 B 级并说明
- 出处 session 的 `resume_sha` 与当前简历不一致 → 先核对对应 bullet 还在不在；在，照常给；改法要注明"基于旧版简历的 mock"

### B 级（通用 resume 启发，标启发名）

启发名清单（用这些固定标签，不要自创）：
- `quantification`：缺数字 / 数字模糊
- `weak-verb`：动词软（"参与"、"协助"）
- `redundant`：重复或填充字
- `jargon-overload`：堆术语
- `passive-voice`：被动语态
- `bullet-too-long`：超 2 行
- `no-impact`：只描述工作，没说结果
- `tech-stack-buried`：技术栈藏在末尾

格式：`[B] [{启发名}] → 改动：{具体改法}`

## Step 4 — 双通道输出

### 通道 1：写 draft 文件

- 路径：原 resume 文件旁；扩展名规则：
  - `.tex` → `resume.draft.tex`，`.md` → `resume.draft.md`
  - **源是 `.pdf`** → 写 `resume.draft.md`（LLM 生成不了 PDF），并在 chat 里说明：改动需要用户自己回填到原排版工具
- 内容：应用所有建议后的完整简历
- **如果 draft 文件已存在**：AskUserQuestion 二选一——覆盖 / 先把旧 draft rename 保留
- **绝不动原 `resume.{ext}`**

### 通道 2：在 chat 里贴改动清单

按章节列每条改动：

```
## 独立产品

- [A] [20260412-1430-数据工程师.md Q3] project:Polymarket盯盘:impact_unclear
  - 原: Polymarket 盯盘机器人 ... 实盘收益率 10%+
  - 改: Polymarket 盯盘机器人 ... 实盘 3 个月对照大盘 -2%，收益率 10%+，最大回撤 4%
  - 为什么: 上次 mock 问你怎么算的，没说清样本和基准

- [B] [quantification]
  - 原: 累计变现 ¥500+
  - 改: 累计变现 ¥500+（GMV ¥1200，扣广告 / 物料成本后净利润 ¥500）
  - 为什么: 数字模糊，¥500 是 GMV 还是净利润？
```

末尾告诉用户："改动写到了 `<draft path>`。如果满意，请你自己把 draft 转正 + commit。Skill 不会替你提交。"

---
name: resume-optimization
description: "通用简历优化权威版（来自 ResumeSkills）：ATS 兼容性检查、Match Score 关键词匹配、X-Y-Z / STAR / CAR bullet 量化改写、JD 加权匹配、求职信、LinkedIn 优化、offer 对比。本模块是 job-hunting 套件里简历优化的唯一权威，ats-breaker / llm-intern / ai-job-search 三个场景插件都引用它而非重述。"
agent_created: true
---

# 模块一：resume-optimization（通用简历优化权威版）

> 来源：ResumeSkills（Paramchoudhary/ResumeSkills，20 子技能库）。本模块将其核心方法论提炼为一份权威版，供全套件共用。

## 1. 适用场景

用户要改简历、写 bullet、量化经历、做 ATS 检查、按 JD 定制、写求职信、优化 LinkedIn、对比 offer。这是求职链路的**第一站**，其他模块的简历相关需求都先回到这里。

## 2. 核心工作流

```
用户贴简历 +（可选）JD
   → ① JD 匹配分析（job-description-analyzer）
   → ② bullet 改写 / 量化（bullet-writer + quantifier）
   → ③ ATS 兼容性检查（ats-optimizer）
   → ④ 按 JD 定制（tailor）
   → ⑤ 求职信（cover-letter）
   → ⑥ LinkedIn（linkedin-optimizer）
   → ⑦ offer 对比（offer-comparison）
```

## 3. 方法论

### 3.1 Bullet 改写：X-Y-Z 公式（核心）

每一条经历 bullet 用 **「Accomplished [X] as measured by [Y] by doing [Z]」**：

- **X** = 你做成了什么（动作结果）
- **Y** = 用什么指标衡量（必须≥1 个数字）
- **Z** = 你具体怎么做的（动作/手段）

变体模板：
- **STAR**：Situation（背景）→ Task（任务）→ Action（行动）→ Result（结果，带数字）
- **CAR**：Challenge（挑战）→ Action（行动）→ Result（结果，带数字）

改写前后示例：
- ❌ 「负责团队管理」 → ✅ 「带领 4 人小组，Q3 交付 XX 项目，团队效率提升 30%」
- ❌ 「优化了模型」 → ✅ 「重构召回链路（Z），将搜索准确率从 82% 提升至 91%（Y），支撑日均 200 万次查询（X）」

强动词表（替换「负责/参与/帮助」）：Led, Built, Designed, Reduced, Increased, Launched, Automated, Optimized, Drove, Shipped, Negotiated, Scaled。

**硬性规则**：每条 bullet 至少包含 1 个量化数字；杜绝「负责/参与/协助」等弱动词开头。

### 3.2 量化发现（quantifier）

用户说不出数字时，用问句挖：
- 规模：「这个项目服务多少用户 / 多少数据量 / 多少 QPS？」
- 影响：「上线后指标变化多少？省了多少钱 / 时间？」
- 对比：「相比之前提升 / 下降了多少 %？」
- 保守估算允许用区间或约数：`~40%`、`8-12 人`、`400+`；占比反推（「占团队 1/5」→「约 20%」）；时间反推（「做了 3 个月」→「约 13 周」）。

### 3.3 ATS 兼容性 + Match Score

**Match Score = 匹配上的关键词 / JD 必需关键词 × 100，目标 ≥ 80%。**

三类关键词要覆盖：硬技能（Python/PyTorch）、软技能（跨团队协调）、行业词（推荐系统/风控）。

ATS 兼容性清单（违反会丢分甚至被筛掉）：
- 用标准字体（Arial/Calibri/Times），不用艺术字；
- **不用表格、不用页眉页脚、不用图片式排版**（很多 ATS 读不出）；
- 章节标题用标准名：Experience / Education / Skills / Projects；
- 联系方式写在正文，不要只放页眉；
- 不要把文字做成图片。

### 3.4 JD 加权匹配

- 把 JD 拆成「必需技能（70% 权重）」和「优先技能（30% 权重）」。
- 加权匹配分 = 必需命中率×70 + 优先命中率×30。
- 判定：90-100 过高配 / 75-89 优秀 / 60-74 好 / 50-59 需拉伸 / <50 不匹配。
- **红旗词检测**：JD 里出现「wear many hats（啥都干）」「rockstar（摇滚明星式牛人）」「competitive salary（有竞争力薪酬，常=低）」等要谨慎，可能是小公司画饼。

### 3.5 求职信（cover-letter）

250-400 词，公式「对方需求 + 你的对应经验 + 可量化的结果」。5 种开场 hook：引述公司近期动态 / 用一段量化成就破题 / 讲一个与岗位强相关的故事 / 直接点出你最匹配的 1 个能力 / 用行业洞察切入。

### 3.6 LinkedIn 优化

- 标题公式：`[Role] | [Expertise] | [Value]`（≤220 字符），例：`NLP Engineer | RAG & 多模态 | 帮搜索准确率 +9pt`。
- About ≤2600 字符，用「我是谁 → 我解决什么问题 → 证据 → 召唤」结构。
- All-Star 清单：头像、标题、About、经历（带量化）、技能（≥5 且获背书）、推荐信。

### 3.7 offer 对比（offer-comparison）

不只看 base。总薪酬 = 现金（base+签字费+年终） + 股权（RSU/期权按现值） + 福利（保险/带薪假） + 津贴（餐补/房补/搬迁）。
用**用户自定义权重决策矩阵**：列出每个 offer 的各维度得分，按用户给的权重（如「成长 40% / 钱 30% / 地点 20% / 稳定 10%」）加权求和，输出排序 + 风险点（如「公司 B 股权占比高但未上市，流动性差」）。

## 4. 输出格式

每轮改写给出：
1. **Before → After** 逐条对照；
2. 改写依据（用了哪个公式 / 哪类量化）；
3. ATS 风险点清单（如有）；
4. 下一步建议（如「还差一个量化数字，补一下 XX 项目的用户规模」）。

## 5. 红线

只重组用户**已有的真实经历**，不虚构项目/指标/职责。数字拿不准用区间或「约」，并标注「需用户确认」。

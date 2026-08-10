---
name: ats-breaker
description: "技术/实习简历 /120 分硬核评分（来自 ATS Breaker / thekarananand）：用招聘 Agent 视角（评分卡移植自 HackerRank hiring-agent）给简历打分，接 gh CLI 抓 GitHub 贡献证据，扣分精确到点并对应具体修复动作。专攻技术/实习岗自查，非用于筛别人。"
agent_created: true
---

# 模块五：ats-breaker（技术/实习简历 /120 分评分）

> 来源：thekarananand/ats-breaker。强项是**对接真实 GitHub 证据 + 用招聘 Agent 同源评分卡 + 机器校验**。这是 resume-optimization 的「技术实习专项插件」，不重述通用 bullet 改写。

## 1. 适用场景

用户问「我的技术/实习简历会被自动筛选打几分」「GitHub 项目怎么写才加分」「低于 80 分别投」。通常在 resume-optimization 改完基础后，做技术岗专项体检。

## 2. 核心工作流

```
① 问简历路径（⚠️ 绝不自行扫文件系统，必须用户主动给路径）
② 读 PDF
③ gh api 抓 GitHub 贡献（过滤 <4 commits 的仓库，分类 open_source / self_project）
④ 选 top7 repo 作为证据
⑤ 按 rubric 打分（4 类 + bonus + deduction，写 JSON）
⑥ validate_scores.py 机器校验分数不超上限
⑦ 出报告：扣分精确到点 + 对应修复动作
```

## 3. 评分卡（"加 X 分 / 扣 X 分"规则）

**总分 = 4 类得分 + bonus − deduction，封顶 120。低于 80 建议先别投。**

### 3.1 四类上限

| 维度 | 上限 | 关键规则 |
|---|---|---|
| open_source | 0-35 | 若全为 personal repo，此项 ≤10 |
| self_projects | 0-30 | **基础 CRUD 强制 0 分**；无 URL/演示扣 30-50%；有 live demo +10-20%；链接失效 −20-30%；泛化命名（project1）−1 |
| production | 0-25 | 创业 / 早期员工额外加分 |
| technical_skills | 0-10 | 技术栈匹配度 |

### 3.2 Bonus（上限 20）

GSoC +5 / GirlScript +3 / 创业 +3-5 / 早期员工 +2-3 / portfolio +2 / LinkedIn +1 / blog +1-3。

### 3.3 Deductions

- 简单项目 −2~5（超过第 1 个后每个 −1~3，泛化名 −1，全 classroom 项目 −2）；
- 缺链接 −3~5/个（仅 GitHub −2~3，链接失效 −1~2）；
- OSS 全是 self_project −3~5；仅 Hacktoberfest −3~5。

### 3.4 Fairness 铁律

**绝不**依据姓名 / 性别 / 学校 / GPA / 地点打分。只评可验证的工程证据。

## 4. 依赖与前置

- Python 3.9+（stdlib-only，无需 pip）；
- **必须已 `gh auth login`**（GitHub CLI），**拒绝匿名 API**；
- 无 LaTeX、无爬虫（且明确拒绝匿名抓取路由）。

## 5. 与 resume-optimization 的关系

本模块只补「技术/实习岗被自动筛选打几分 + GitHub 证据」。通用 bullet 改写、ATS 关键词基础检查回 `modules/resume-optimization/SKILL.md`。

## 6. 红线

不扫用户文件系统（必须用户给路径）；不依据人口属性打分；分数必须机器校验不超上限；只用于自查，不用于筛别人。

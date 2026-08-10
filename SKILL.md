---
name: job-hunting
description: "求职全链路 AI 助手套件 —— 把 8 个开源求职 Skill（ResumeSkills / AI Job Search / Claude Interview Coach / InterviewRadar / ATS Breaker / LLMInternSkill / Resume Coach / Interview Skills）策展成一个统一套件，覆盖「简历优化 → 自动投岗 → 通用模拟面试 → 大厂定向模拟 → 弱点追踪 → 真实面经备考 → 技术/AI 实习专项评分 → 谈薪」全链路。This skill should be used when the user wants to 优化简历 / 改写 bullet / 做 ATS 检查 / 按 JD 定制简历 / 写求职信 / 优化 LinkedIn / 比 offer / 自动搜职位投简历 / 生成 LaTeX CV / 模拟面试 / 准备 STAR 故事 / 谈薪资 / 抓牛客小红书真实面经 / 给技术实习简历打分 / 给 AI/LLM 实习简历做证据闸门 / 面试复盘弱点追踪 / 大厂定向多轮模拟 / HR面与薪资谈判话术 / 中国初创岗位扫描。Trigger phrases include 帮我改简历, 简历优化, bullet 怎么写, ATS 评分, JD 匹配, 求职信, LinkedIn, offer 对比, 自动投简历, LaTeX 简历, 模拟面试, STAR, 面试准备, 面经, 真实面经, 技术简历打分, AI 实习简历, 证据闸门, 谈薪, 面试复盘, 弱点追踪, 大厂模拟, HR面, 薪资谈判, 中国初创扫描, or any full-cycle job-search / resume / interview request."
agent_created: true
---

# job-hunting 求职全链路套件（主编排器）

把 6 个开源求职 Skill 合并成一个可路由的套件。**核心理念**：这些工具不是帮你编经历，而是帮你用「系统能懂的语言」把已经有的东西讲清楚。

## 套件结构

```
job-hunting/
├── SKILL.md                      ← 你正在读的这个（路由器）
└── modules/
    ├── resume-optimization/      ← 通用简历优化权威版（ATS / bullet 量化 / JD 匹配 / 求职信 / LinkedIn / offer 对比）
    ├── ai-job-search/            ← 端到端投岗流水线（搜职位 → LaTeX CV → 双 Agent 审稿 → 编译校验）
    ├── interview-coach/          ← 面试教练（STAR 故事库 / 5 维评分 / 模拟面试 / 谈薪 / 跨会话校准）
    ├── interview-radar/          ← 真实中文面经锚定备考包（抓牛客/小红书/GitHub，⚠️ ToS 风险）
    ├── ats-breaker/              ← 技术/实习简历 /120 分评分（接 GitHub 证据，硬核筛选视角）
    ├── llm-intern/               ← AI/LLM 实习简历「证据闸门」（C0-C3 证据等级 + 面试拷打降级）
    ├── resume-coach/             ← 面试教练（跨会话弱点追踪 + 简历打磨 + 中国初创 research scout）
    └── interview-skills/         ← 大厂定向模拟面试官（好/差答案对比 + HR面 + 薪资谈判 + 多轮连贯模拟）
```

## 路由表（按用户意图选择模块）

| 用户要说的话 | 加载模块 | 路径 |
|---|---|---|
| 改简历、写 bullet、量化经历、ATS 检查、按 JD 改简历、求职信、LinkedIn、比 offer | **resume-optimization** | `modules/resume-optimization/SKILL.md` |
| 自动搜职位、批量投、生成 LaTeX PDF 简历、Drafter-Reviewer 审稿 | **ai-job-search** | `modules/ai-job-search/SKILL.md` |
| 模拟面试、STAR 故事、面试评分纠偏、谈薪话术 | **interview-coach** | `modules/interview-coach/SKILL.md` |
| 抓牛客/小红书**真实面经**、做针对性备考包、预测面试官追问 | **interview-radar** | `modules/interview-radar/SKILL.md` |
| 技术/实习简历「会被自动筛选打几分」、接 GitHub 贡献证据 | **ats-breaker** | `modules/ats-breaker/SKILL.md` |
| AI/LLM 实习简历、每条经历扛不扛得住追问、证据闸门、不虚 | **llm-intern** | `modules/llm-intern/SKILL.md` |
| 面试复盘、跨会话弱点累积追踪、简历打磨（反向引用弱点）、中国初创岗位扫描与公司研究 | **resume-coach** | `modules/resume-coach/SKILL.md` |
| 大厂定向模拟面试（阿里/腾讯/字节/Google…）、好答案vs差答案、HR面专项、薪资谈判话术、多轮连贯模拟 | **interview-skills** | `modules/interview-skills/SKILL.md` |

## 去重铁律（重要，避免 6 份重复写简历优化）

- **resume-optimization 是简历优化的唯一权威版**。它的 bullet 量化（X-Y-Z 公式）、ATS 关键词匹配、JD 加权匹配方法，其他 5 个模块都不再重述。
- **ats-breaker / llm-intern / ai-job-search 是「场景插件」**，各自只补自己独特的一块：
  - ats-breaker 补「技术/实习岗被自动筛选打几分 + GitHub 证据」；
  - llm-intern 补「AI 实习岗的证据闸门 C0-C3 + 简历↔面试联动」；
  - ai-job-search 补「LaTeX 真实出 PDF + 双 Agent 审稿工程」。
- 这三个插件在需要通用 bullet 改写 / ATS 基础检查时，**直接指引用户回 resume-optimization**，不另写一份。
- **resume-coach / interview-skills 是「面试训练插件」**，与 interview-coach 的边界（三者都会模拟面试，但切入点不同）：
  - interview-coach 是通用 STAR 教练（5 维评分 / 故事库 / 跨会话校准），偏「方法论」；
  - resume-coach 补「跨会话弱点累积追踪 + 简历打磨反向引用弱点 + 中国初创 research scout（聚合候选池、不打分）」，偏「本地状态持久化 + 中国初创研究」；
  - interview-skills 补「大厂定向题库（阿里/腾讯/字节/Google…）+ 好答案vs差答案对比 + HR面专项 + 薪资谈判话术 + 多轮连贯模拟」，偏「靶向大厂 + 话术模板」；
  - 在同一次对话里，按用户意图只加载其中一个面试模块即可，不要重复加载多个。

## 执行约定

1. 收到求职类请求，先判断意图落在路由表哪一行；命中则 `Read` 对应模块 `SKILL.md`，严格按该模块的方法论执行。
2. 多意图（如「改完简历再模拟面试」）：按链路顺序依次加载对应模块，上一模块产出作为下一模块输入。
3. 真实性是底线：6 个源 Skill 都强调「不编造」。任何改写只允许重组用户**已有的真实经历**，不得虚构项目、指标、职责。遇用户要求虚构，明确拒绝并说明这是套件红线。
4. 中文求职市场（牛客/小红书面经、中文 ATS）优先用 interview-radar + llm-intern；海外/英文岗优先 resume-optimization + ai-job-search + interview-coach。

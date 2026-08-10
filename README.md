# job-hunting · 求职全链路 AI 助手套件

把 8 个开源求职 Skill 策展成一个**可路由的统一套件**，覆盖「简历优化 → 自动投岗 → 通用模拟面试 → 大厂定向模拟 → 弱点追踪 → 真实面经备考 → 技术/AI 实习专项评分 → 谈薪」全链路。

核心理念：这些工具不是帮你编经历，而是帮你用「系统能懂的语言」把**已经有的东西**讲清楚。真实性是底线——任何改写只允许重组你的真实经历，不得虚构。

## 模块清单

| 模块 | 来源 | 作用 |
|---|---|---|
| `resume-optimization` | ResumeSkills | 通用简历优化权威版（ATS / bullet 量化 / JD 匹配 / 求职信 / LinkedIn / offer 对比） |
| `ai-job-search` | MadsLorentzen/ai-job-search | 端到端投岗流水线（搜职位 → LaTeX CV → 双 Agent 审稿 → 编译校验） |
| `interview-coach` | Anthropic interview-coach | 通用 STAR 教练（5 维评分 / 故事库 / 跨会话校准 / 谈薪） |
| `interview-radar` | KunChen1110/InterviewRadar | 真实中文面经锚定备考包（抓牛客/小红书/GitHub，⚠️ 注意各平台 ToS） |
| `ats-breaker` | thekarananand/ATS-Breaker | 技术/实习简历 /120 分硬核评分（接 GitHub 证据） |
| `llm-intern` | wanyichen06/LLMInternSkill | AI/LLM 实习简历「证据闸门」（C0-C3 证据等级 + 面试拷打降级） |
| `resume-coach` | JinzeWang10/resume-coach | 跨会话弱点累积追踪 + 简历打磨反向引用弱点 + 中国初创 research scout |
| `interview-skills` | jennifer88huang/interview-skills | 大厂定向题库（阿里/腾讯/字节/Google…）+ 好答案vs差答案 + HR面 + 薪资谈判 + 多轮连贯模拟 |

## 去重原则（套件铁律）

- `resume-optimization` 是简历优化的**唯一权威版**，其他模块不重述 bullet 量化 / ATS 基础检查。
- `ats-breaker` / `llm-intern` / `ai-job-search` 是「场景插件」，各自只补独特一块，需要通用改写时回指 `resume-optimization`。
- 三个面试模块（`interview-coach` / `resume-coach` / `interview-skills`）切入点不同，同一次对话只加载一个，不重复加载。

## 安装

方式一：git clone（推荐，便于后续 `git pull` 更新）

- **WorkBuddy**：
  ```bash
  git clone https://github.com/weiqing010305-art/job-hunting-skills.git ~/.workbuddy/skills/job-hunting
  ```
- **Claude Code**：
  ```bash
  git clone https://github.com/weiqing010305-art/job-hunting-skills.git ~/.claude/skills/job-hunting
  ```

方式二：手动复制
把本仓库的 `SKILL.md` 与 `modules/` 整体复制到上述 `skills/job-hunting/` 目录下（保持 `SKILL.md` 在根、`modules/` 在下）即可。

调用时只需说「模拟面试 / 改简历 / 面经 / 谈薪…」，主编排器 `SKILL.md` 会按意图路由到对应模块。

## 红线

不编造项目、指标、职责。遇要求虚构，直接拒绝。

## 致谢

本套件整合自以下开源项目（按其 LICENSE 使用）：ResumeSkills、MadsLorentzen/ai-job-search、Anthropic interview-coach、KunChen1110/InterviewRadar、thekarananand/ATS-Breaker、wanyichen06/LLMInternSkill、JinzeWang10/resume-coach、jennifer88huang/interview-skills。

## English

**job-hunting** is a curated, router-style bundle of 8 open-source job-search skills, covering the full loop: resume optimization → automated applying → general mock interviews → big-tech targeted mocks → weakness tracking → real interview-question prep → technical / AI-intern scoring → salary negotiation.

Drop the repo into your skills directory:

- WorkBuddy: `~/.workbuddy/skills/job-hunting`
- Claude Code: `~/.claude/skills/job-hunting`

The root `SKILL.md` acts as a router and dispatches each request to the right module (see the module table above). Everything is prompt/markdown only — no external network calls, no fabricated experience. MIT licensed.

## License

MIT —— 见 [LICENSE](LICENSE)。

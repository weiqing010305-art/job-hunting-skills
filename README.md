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

## 各模块怎么发挥作用

每个模块都是一份独立的方法论文档，主编排器按你一句话的意图把它们接进来。下面讲清楚每个模块**实际怎么干活**。

### resume-optimization — 简历优化的底盘
你贴简历（可选带 JD），它按七步走：JD 匹配分析 → bullet 量化改写 → ATS 兼容检查 → 按 JD 定制 → 求职信 → LinkedIn → offer 对比。核心是 **X-Y-Z 公式**（做成了什么 X / 用什么数字衡量 Y / 怎么做的 Z），每条 bullet 强制带 ≥1 个量化数字；再用 **Match Score**（命中关键词 ÷ JD 必需关键词）和 ATS 清单（不用表格 / 图片 / 页眉）保证机器筛得过。全套件其他模块的简历需求都先回这里。

### ai-job-search — 真出 PDF 的投岗工程
不是自动点「申请」的机器人。它跑一条本地流水线：`/scrape` 爬职位 → `/rank` 按 5 维 + 地点硬过滤批量打分排序 → `/apply` 对**单个**职位用 **Drafter–Reviewer 双 Agent** 起草 LaTeX CV + 求职信、互相挑刺修订、编译成真实 PDF，再用 `pdftotext` 抽文本层做 ATS 校验，**最后呈现给你由人提交**。偏英文 / 海外岗；爬站有 ToS + 翻墙风险，简历数据会进 git。

### interview-coach — 会越练越准的面试教练
地基是 **STAR 故事银行**（每条经历存成带「earned secrets」和 fit 等级的故事，避免多题抢同一个）。每次模拟面试打 **5 维分**（内容 / 结构 / 相关 / 可信 / 差异），映射到 root cause 派 drill。最高阶是 **校准引擎**：真实面 ≥3 场后比对「我内部给的分」vs「真实反馈」，外部反馈权重更大，越面越准而不是自我感觉良好。靠一个 `coaching_state.md` 做跨会话记忆，无代码依赖。

### interview-radar — 抓真实中文面经并锚定到你简历
从「简历 + 一句岗位方向」出发，迭代检索牛客 / 小红书 / GitHub 真实面经，按 **独立来源数 × 时效** 排序（≥2 个独立来源才算高频题，防单一帖误判），时效硬过滤保留近 730 天。核心是 **项目锚定**：每道高频题必须能同时追溯到「你的简历项目 / 技能」+「真实爬到的题」，否则降为通用八股题；输出固定 10 节备考包，每题可点回原帖。⚠️ 抓小红书需 MediaCrawler + 登录 + 翻墙，有 ToS 风险（你已确认接受）。

### ats-breaker — 技术 / 实习简历的 /120 分硬核体检
你给简历路径（它**绝不自己扫文件系统**），它用 `gh` 抓你 GitHub 贡献当证据，按四类评分卡（open_source / self_projects / production / technical_skills，封顶 120）逐点加分扣分，**分数机器校验不超上限**。铁律：绝不按姓名 / 性别 / 学校 / GPA 打分，只评可验证工程证据；低于 80 建议先别投。是 resume-optimization 的「技术实习专项插件」。

### llm-intern — AI / LLM 实习简历的「证据闸门」
给冲 LLM / AI 实习岗的人用。每条 claim 按 **C0–C3 证据等级** 定级（C3 必须有指标定义与记录，否则不许写），等级不够直接拦下。再检测 12 类 AI role type（rag / agent / posttraining…）做 fit 判定，然后 **5 轮面试拷打** 把 claim 转成「回答卡」（危险 / 及格 / 强 / 需补证据），最后用 **Project Scout** 推荐能补证据的开源项目——但学开源 ≠ 伪造成工作经历。纯 prompt，无代码依赖。

### resume-coach — 简历常驻 + 弱点跨会话累积
四个模式共享一份**写在磁盘上的状态**：interview（基于你简历出 grounded 的模拟题）、polish（改简历，A 级建议必须 cite 具体历史 session）、debrief（看练得怎么样、弱点排行）、scout（只研究中国初创公司、绝不替你投递）。关键护城河是**本地常驻**：简历、历史 transcript、弱点累积都存在 `~/.claude/resume-coach-data/`，SaaS / 网页 ChatGPT 做不到。八条不变量里最硬的三条：永不覆盖原简历、永不替你 git 提交、面试题必须挂在简历具体 bullet 上。

### interview-skills — 大厂定向模拟面试官
你给公司 + 岗位 + JD + 简历，它先**解析 JD 和简历**，再**匹配公司风格**（字节范 / 阿里味 / 腾讯味 / Google / Meta / Amazon…），然后生成 10 道针对性题（技术基础 + 项目深挖 + 行为面 + 反问预测），每题带难度、参考提示、追问方向。支持四种专项：**好 / 差答案对比**、**HR 面**、**薪资谈判话术**、**多轮连贯模拟**（一面 → 二面 → 三面 → HR，后轮继承前轮暴露的强弱点）。覆盖阿里 / 腾讯 / 字节 / 百度 / 美团 / 京东 / 华为 / 滴滴 / 拼多多 + Google / Meta / Amazon / Microsoft 等。

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

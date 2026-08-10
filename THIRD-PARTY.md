# 第三方组件与许可（THIRD-PARTY NOTICES）

本仓库 `modules/` 下各子模块为第三方开源作品，版权归各自原作者，按其各自许可证使用。本仓库根目录的 MIT 许可证与版权声明（Copyright (c) 2026 微青）**仅适用于本仓库的原创整合编排内容**（根目录 `SKILL.md` 路由器、`README.md`、模块整合与路由设计），**不覆盖**下方任何子模块。

各子模块的许可证文本以原仓库为准。以下为溯源与许可摘要：

| 模块 | 原作者 | 仓库 | 许可证 | 版权归属 |
|---|---|---|---|---|
| resume-optimization | Paramchoudhary | https://github.com/Paramchoudhary/ResumeSkills | MIT | 原作者 |
| ai-job-search | Mads Lorentzen | https://github.com/MadsLorentzen/ai-job-search | MIT | 原作者 |
| interview-coach | noamseg（基于 Anthropic interview-coach） | https://github.com/noamseg/interview-coach-skill | MIT | 原作者 |
| interview-radar | Kun Chen | https://github.com/KunChen1110/InterviewRadar | MIT | 原作者 |
| ats-breaker | Karan Anand | https://github.com/thekarananand/ats-breaker | ⚠️ 未声明（见下） | 原作者 |
| llm-intern | wanyichen06 | https://github.com/wanyichen06/LLMInternSkill | MIT | 原作者 |
| resume-coach | JinzeWang10 | https://github.com/JinzeWang10/resume-coach | MIT（README 声明） | 原作者 |
| interview-skills | jennifer88huang | https://github.com/jennifer88huang/interview-skills | MIT | 原作者 |

## ats-breaker 许可证说明（重要）

`ats-breaker` 模块（来源：<https://github.com/thekarananand/ats-breaker>，作者 Karan Anand `<thekarananand@gmail.com>`）**未在仓库中提供任何 LICENSE 文件**，其 `package.json` 也**未声明 `"license"` 字段**。

依据版权法默认规则：**未声明许可证 = 保留所有权利**。即作者未明文授权他人再分发、修改或制作衍生作品。

本仓库在以下前提下将其纳入并署名：

1. 该 skill 作为 Claude Code skill **公开发布**，其 README 明确提供 `npx skills add thekarananand/ats-breaker` 的安装方式，作者显然意在让人安装使用；
2. 本仓库**完整保留原作者署名与来源链接**，未声称对其拥有版权；
3. 使用者应知悉这属于**灰色地带**——作者未说"禁止"，但也未说"允许"。

**建议**：若你打算正式分发本仓库，最稳妥的做法是就 ats-breaker 向作者 `<thekarananand@gmail.com>` 索取一份明确的许可证授权（例如 MIT）。在此之前，ats-breaker 部分按"已署名、获作者默示许可"处理，风险由使用者自行承担。如不愿承担该风险，可从公开分发版本中移除 `modules/ats-breaker/`。

---

*本文件仅作署名与许可溯源之用，不替代任一原项目的许可证文本。如与原项目许可证有冲突，以原项目为准。*

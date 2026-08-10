---
name: llm-intern
description: "AI/LLM 实习简历「证据闸门」（来自 LLMInternSkill / wanyichen06）：用证据等级 C0-C3 判断每条经历可写/谨慎写/补证据后写/不能写，把简历 claim 直接转成面试拷打与回答卡降级，检测 12 类 AI 岗位 role type，可选 LaTeX 出中文 PDF。专攻大模型实习求职的真实性边界。"
agent_created: true
---

# 模块六：llm-intern（AI/LLM 实习简历「证据闸门」）

> 来源：wanyichen06/LLMInternSkill。强项是**以证据等级为硬闸门 + 简历↔面试联动**。这是 resume-optimization 的「AI 实习专项插件」。

## 1. 适用场景

用户是冲 **LLM / AI 实习岗**的，关心「我这条经历写上去面试扛不扛得住」「RAG/Agent/后训练岗怎么匹配」「开源项目能不能包装成经历」。这是面试前最该过的「真实性闸门」。

## 2. 核心工作流

```
raw resume + materials/ + target_jd.txt
  → 简历润色 → JD 匹配（role type 检测）
  → 真实性边界 → Evidence Contract（C0-C3 定级）
  → 定制简历 → 面试拷打 → 回答卡 → 补证据计划
  → Project Scout（推荐可补证据的开源项目）
  → 可选 LaTeX 草稿（中文 PDF-ready）
```

## 3. 方法论

### 3.1 Evidence Contract（证据等级，核心闸门）

每条 claim 定级，等级不够不允许写：

| 等级 | 含义 | 最小证据 |
|---|---|---|
| C0 | 了解/参与（notes/course） | 笔记/课程 |
| C1 | 负责模块（code/README/截图） | 代码/文档/截图 |
| C2 | 设计/优化（experiment/bad cases/设计文档） | 实验记录/坏案例/设计 doc |
| C3 | 结果影响（metric 定义/baseline/日志/报告/上线） | **必须有指标定义与记录，否则不允许写** |

常见映射：如「优化 RAG」但缺 eval → 降级为「整理 RAG bad case 并提出优化方向」（C2 而非 C3）。

### 3.2 JD Analysis（12 类 role type 检测）

检测：rag / agent / agentic-rl / posttraining / pretraining / llm-app / llm-algorithm / search-ranking / aigc / multimodal / backend-ai / mixed。
5 步：显式需求 → 隐藏面试测试点 → 角色类型 → 证据映射 → fit verdict（strong / weak / **risky** / not recommended）。`risky` = 写得出但扛不住深问，需补证据。

### 3.3 Interview Grilling（面试拷打，5 轮）

1. Truth boundary（真相边界）：这条 claim 你能讲到哪一层？
2. Technical depth（技术深度）：input/output/data/model/system/metrics 跟住追。
3. JD deep dive（按 JD 深挖）。
4. Scenario（场景题）。
5. Risk Summary（风险总结：哪些 claim 该降级）。

好问题模板：跟住一个 claim，连续追问「数据从哪来 / 模型怎么选的 / 指标怎么定义的 / 失败了怎么办」。

### 3.4 Answer Cards（回答卡，4 级）

Dangerous（危险，会露馅）/ Passable（及格）/ Strong（强，带证据）/ Evidence needed（需补证据才能答）+ 对应「可降级的安全措辞」。
缺证据时最强回答可能是：「这条我现在还不会写成 claim，我先补 XX 证据」。

### 3.5 Project Scout（补证据推荐）

每个推荐含 why / risk / 最小运行路径 / 怎么改 / 需要什么证据 / 能写什么 claim / 面试会怎么问。
边界：**学开源 ≠ 包装成工作经历**，只能写成「复现/研读开源项目」，不能伪造成自己的产出。

## 4. 依赖与前置

- 纯 prompt，**无代码依赖**；
- 可选 LaTeX（XeLaTeX）出中文 PDF（Bill Ryan 中文模板）；
- 无爬虫、无 gh、无翻墙。

## 5. 与 resume-optimization 的关系

通用 bullet 改写、ATS 基础检查回 `modules/resume-optimization/SKILL.md`。本模块只补「AI 实习岗的证据闸门 + 简历↔面试联动 + role type 匹配」。

## 6. 红线

证据等级不够不高写；开源项目不伪造成工作经历；不虚构指标；risky 的 claim 必须明确标注「需补证据」。

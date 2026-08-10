# Mode: debrief

前提：SKILL.md 的 Setup 已跑完（简历、最近 transcripts、weaknesses.md 已在工作记忆里）。

## Step 1 — 列 session

`<DATA>/sessions/` 全部文件都列出来（文件名本身带日期 + 岗位），最近 5 份因为已全文读入可以带题数 / round 细节：

```
共 12 次面试，最近 5 次：
1. 2026-05-10 14:23 · 数据工程师 · project deepdive · 3 题
2. 2026-04-12 14:30 · SDE @ FAANG · mixed · 5 题
...
（更早 7 次只列文件名）
```

## Step 2 — Top 5 weakness

从 `state/weaknesses.md` 数每个 tag 小节下的引用行数（每行一次），取 top 5：

```
高频弱点（按出现次数）：
1. ×3 project:Polymarket盯盘:impact_unclear
2. ×2 behavioral:conflict:no_resolution
3. ×2 project:小红书自动运营:metric_ambiguous
...
```

## Step 3 — 简历盲区扫描

- 简历里所有项目 / 工作经历 bullet 列出来
- **全量覆盖集**：用 Grep 在 `<DATA>/sessions/` 全部文件里搜 `Targets bullet` 行（不必把老 session 全文读入），汇总历史上被问过的 bullet
- 命中来自旧版简历的 session（`resume_sha` 不一致）→ 该命中标注"旧版简历"，对不上当前 bullet 的不算命中
- 找出**从没被问过**的 bullet：

```
从没被 mock 到的简历点（面试官可能也看不见）：
- 教育 / UPenn 设计学院研究助理
- 工作 / Souscout 实体匹配方法
- 独立产品 / 小包 ReadyToGo
建议下次 mock 把这些拿出来打一遍，看简历表述能不能撑住实战。
```

## Step 4 — 推荐下次重点

基于 Step 2 + 3，给一个**单句**的下次 mock 建议。例："下次重点：project deepdive，专攻 Polymarket（高频弱点）+ 小包 ReadyToGo（盲区）"。

不要在 debrief 里同时跑 interview——那是用户下一次的事。

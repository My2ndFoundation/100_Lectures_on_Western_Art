# Wiki Operations Log

Append-only。每条记录用 `## [YYYY-MM-DD] <event-type> | <subject>` 开头，便于 `grep "^## \[" log.md | tail -10` 检索。

Event types:
- `ingest` — `/art-ingest` 处理一篇 raw
- `query` — 一次综合性 query（非必记，sieve 后值得复盘的才记）
- `lint` — 一次健康检查
- `synthesis-filed` — 一次 query 答案回填为 `概念/<name>.md`
- `schema-update` — `CLAUDE.md` 改动

---

## [2026-05-13] schema-update | 初始化项目骨架

- 新建：`CLAUDE.md`、`README.md`、`index.md`、`log.md`
- 新建目录：`时代/`、`流派/`、`人物/`、`技法/`、`作品/`、`来源/`、`概念/`、`_meta/specs/`、`_meta/plans/`
- 新建 skill：`/art-ingest`、`/art-scan`
- 新建状态文件：`.ingested.tsv`（仅 header，零行）
- 设计文档：`_meta/specs/2026-05-13-art-wiki-design.md`
- 备注：架构与 skill 模式由 `DeDao-100 Modern Thinking Tools` 迁移而来；针对艺术史领域做了三处关键调整 — 双语命名、`pronunciation` frontmatter、作品 folder-per-artwork 约定。

## [2026-05-13] schema-update | 增加 course type + 概念 folder-mode

- 触发：002 ingest 的 Step 4 Checkpoint 暴露的两个 schema gap
- 变更：`CLAUDE.md` §3 type 枚举追加 `course`，新增 `课程/<课程全名>.md` section 模板；`概念/` 增加可选的 folder-per-concept 模式（用于承载图片，如类型样本）
- 新建目录：`课程/`、`_meta/lecture-decorations/`
- 备注：用户 Q3 + Q5 决策记录在 002 ingest checkpoint 对话中

## [2026-05-13] ingest | 002｜古希腊雕塑：为什么做得这么逼真？

- 新建：来源(1) 时代(1) 流派(3) 人物(3) 技法(4) 作品(7) 概念(3) 课程(1)
- 更新：index.md（首批实体录入）
- 图片：下载 9，复用 0，失败 0
- 备注：
  - 路人式人物（鲍德里亚、希罗多德、普萨美提克一世、荷马）按 Q1 决策跳过 stub，在来源页明确标注为"路人式引述"
  - 古埃及对照作品[[双人立像 (古埃及) Egyptian Pair Statue]] 按 Q2 决策建页
  - 库罗斯与科莱类型样本图按 Q3 决策放进 `概念/库罗斯 Kouros/01.jpg`（概念页 folder-mode 首次使用）
  - 末尾装饰图按 Q4 决策落地 `_meta/lecture-decorations/002.jpg`，来源页正文里改写为相对路径
  - 课程主页 `[[顾衡·西方美术100讲]]` 按 Q5 决策建页（新 `course` type）
  - 三位希腊雕塑家的 `pronunciation.original` (古希腊语 IPA) 按 Q6 决策全部留空，待用户补
  - 多处 `(*not from wiki*)` 标记：博物馆藏地、生卒年、原书已佚等训练数据补全部分

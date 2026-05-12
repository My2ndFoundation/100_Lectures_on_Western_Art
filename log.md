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

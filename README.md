# 100 Lectures on Western Art — Personal Wiki

顾衡《西方美术 100 讲》的 LLM 协同维护知识库。原文剪藏沉淀在 `raw/`，结构化的中英双语 wiki 由 LLM 增量构建在六个目录（`时代/`、`流派/`、`人物/`、`技法/`、`作品/`、`来源/`）+ 选填的 `概念/`，全部以 Obsidian `[[wikilinks]]` 互联。

详细规范见 [`CLAUDE.md`](./CLAUDE.md)；本文件只覆盖**人类怎么用**。

设计文档与决策历史在 [`_meta/specs/2026-05-13-art-wiki-design.md`](./_meta/specs/2026-05-13-art-wiki-design.md)。

---

## 目录布局

| 路径 | 写入方 | 内容 |
|---|---|---|
| `raw/` | **只有用户** | 从得到 App 剪藏的原文。LLM 只读，永不改写。 |
| `来源/` | LLM | 每篇课程一页：一句话总结、核心论点、关键概念、`[[wikilinks]]`，以及 **`## 原文`（自包含正文，便于静态 HTML 发布）** |
| `时代/` `流派/` `人物/` `技法/` | LLM | 实体页。一个实体一页，文件名**双语**（中文 English），原文/IPA/别名进 frontmatter |
| `作品/<bilingual>/` | LLM | **每件作品一个文件夹**：内含同名 `.md` + 该作品在多 lecture 中出现过的所有图片（`01.jpg`、`02.jpg` …） |
| `概念/` | LLM | Query 沉淀页（非必备）。综合性答案 ≥200 字可回填到这里 |
| `index.md` | LLM | 全 wiki 目录（按 type 分节） |
| `log.md` | LLM | append-only 操作日志（`grep "^## \["` 友好） |
| `_meta/` | 用户 + LLM | 设计文档、计划 |
| `.claude/` | LLM (skills) | Claude Code 配置：见下 |
| `.ingested.tsv` | LLM (`/art-ingest`) | 已 ingest 的 raw 文件清单（append-only） |

`raw/assets/` 是 Obsidian「Download attachments for current file」热键的落点；LLM 不会写入这里。

## 日常操作

### 1. 加新原文

把从得到 App 剪藏的 markdown 丢进 `raw/`。文件名建议保留原标题，例如：

```
raw/002｜古希腊雕塑：为什么做得这么逼真？ - 得到APP.md
```

` - 得到APP` 后缀可有可无。

### 2. 让 LLM 处理：两个 skill

#### `/art-scan` — 扫描未处理的 raw 文件

```
/art-scan
```

LLM 会：
1. 跑 diff: `find raw -maxdepth 1 -name '*.md'` 与 `.ingested.tsv` 对比
2. 列出所有未处理的新文件（按课程编号排序）
3. 问你要全部 ingest、挑选、还是按 [[时代]] 归组
4. 顺序调起 `/art-ingest`，**一篇一确认**

#### `/art-ingest <path>` — 处理单个 raw 文件

```
/art-ingest raw/002｜古希腊雕塑：为什么做得这么逼真？ - 得到APP.md
```

LLM 按 [`CLAUDE.md` §5](./CLAUDE.md) 的 11 步流程走完：

读原文 → 解析图片块 → alias 去重 → **Checkpoint** → 写来源页 → 图片本地化到 `作品/<bilingual>/NN.ext` → 建/更实体页 → 更新 `index.md` → 写 `log.md` → 追加 `.ingested.tsv` → 报告 → **不**自动 commit。

**Checkpoint（Step 4）是非常重要的暂停点**：LLM 会先把候选清单（"时代 X 新建、流派 Y 复用 [[…]]、作品 Z 是新作品/这是已有作品的第 03 张图…"）+ 双语命名提案 + IPA 草稿一起报给你，等你回话再写任何 wiki 页。这一步用于纠偏命名、合并别名、调整侧重、修正 IPA。

不带参数也可以触发，LLM 会问你处理哪一篇。也可以用自然语言"ingest 那篇文艺复兴 014"触发。

### 3. 提问 / 复盘

直接在聊天里问，例如：

> 印象派和后印象派的关键区别是什么？谁是承上启下的人？
> 失蜡法在希腊雕塑和中国青铜器中的运用有什么差异？
> 《掷铁饼者》的 S 造型和波留克列特斯的「持矛者」有什么传承关系？

LLM 走 [`CLAUDE.md` §6](./CLAUDE.md) 的 query 流程：先读 `index.md` → 读相关页 → 综合作答（带 `[[wikilinks]]`，训练数据补充打 `(*not from wiki*)`）。如果答案 ≥200 字或连接 ≥2 个未文档化概念，会主动问你要不要把答案沉淀回 `概念/<name>.md`。

### 4. 体检

```
lint
```

LLM 跑 [`CLAUDE.md` §7](./CLAUDE.md) 的 10 项检查（孤儿页、stub、缺页、`⚠️` 未决冲突、过时声明、断链、frontmatter 完整性、index 漂移、**作品文件夹特检**、`pronunciation` 留空率），输出报告，**不**自动修。

---

## 给 LLM 的硬约束（节选自 [`CLAUDE.md`](./CLAUDE.md) §9）

- `raw/` 永远只读
- 冲突用 `> ⚠️ 与 [[…]] 中的说法不同：…` 标注，不静默覆盖
- 训练数据来源的事实必须打 `(*not from wiki*)`
- 一个实体只能有一页（先 alias 搜索再创建）
- 双语文件名必须有 `name_en`（不能漏英文）
- IPA 不确定 → 留空，不能瞎填
- 图片落点是 `作品/<bilingual>/NN.ext`，不是根 `assets/`，更不是 `raw/assets/`
- ingest 不跳 Step 4 checkpoint
- 不主动 web 搜索
- 不自动 commit

---

## 文件参考

| 想看什么 | 去哪 |
|---|---|
| LLM 工作规范全文 | [`CLAUDE.md`](./CLAUDE.md) |
| 全 wiki 目录 | [`index.md`](./index.md) |
| 每次操作历史 | [`log.md`](./log.md) |
| Skill 实现 | `.claude/skills/art-ingest/SKILL.md`、`.claude/skills/art-scan/SKILL.md` |
| 已处理状态 | `.ingested.tsv` |
| 设计文档 | `_meta/specs/`、`_meta/plans/` |

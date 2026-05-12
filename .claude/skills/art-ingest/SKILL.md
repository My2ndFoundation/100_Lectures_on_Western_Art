---
name: art-ingest
description: Use when the user wants to ingest a raw 顾衡《西方美术 100 讲》clipping into the wiki. Triggers on "ingest"、"处理这篇"、"消化这节课", or when the user supplies a path under raw/ in the Art-100 project.
model: claude-opus-4-7
effort: high
---

# Art-100 Ingest Workflow

## Overview

Processes one raw lecture clipping from `raw/` into the bilingual Chinese-English wiki (`时代/`、`流派/`、`人物/`、`技法/`、`作品/`、`来源/`). Authoritative procedure lives in `CLAUDE.md` §5; this skill enforces ordering, the user-checkpoint, the no-overwrite rules, and the artwork-folder convention so they cannot be skipped.

## Arguments

The skill accepts one raw file path:
```
/art-ingest raw/<lecture-title>.md
```

If no argument: ask "想 ingest `raw/` 下的哪一篇？" Do not guess.

## The Non-Negotiable Rule

**You MUST run the Step 4 checkpoint and wait for the user to redirect emphasis BEFORE writing anything to the wiki.**

No file in `时代/`、`流派/`、`人物/`、`技法/`、`作品/`、`来源/`、`概念/`、`index.md`、`log.md` is touched until the user has confirmed direction.

Equally non-negotiable:
- `raw/` is read-only. Never write, never modify (CLAUDE.md §2, §9).
- Never silently overwrite a contradicting claim — flag with `> ⚠️ 与 [[…]] 中的说法不同：…` (CLAUDE.md §5 / §9).
- Never duplicate an entity that already exists under an alias — alias-search the wiki first (CLAUDE.md §4).
- Never use training-data facts without `(*not from wiki*)` (CLAUDE.md §6 / §9).
- Bilingual filenames are mandatory; `name_en` cannot be blank (CLAUDE.md §3 / §4).
- IPA pronunciation: leave blank if uncertain. Never guess.

## Workflow (follow in order, no skipping)

### Step 1 — Read the raw source end-to-end

Read BOTH the frontmatter (clipping metadata) AND the body. From the body, identify:

- 板块 (course section if marked)
- 课程主旨 (one-paragraph thesis)
- **时代** (eras explicitly named or implied)
- **流派** (schools / movements / "-isms")
- **人物** (artists, patrons, theorists)
- **技法** (techniques, formal devices)
- **作品** (artworks — see Step 2 for the dedicated parser)
- 与其他课程的交叉引用 ("我前面讲过…"、"下一讲…")
- 重要的"概念"（如 "理念美"、"母题"）

From the frontmatter: `source:` URL, any `[[…]]` back-reference wikilinks (typically under `author:` pointing at the course master page, e.g. `顾衡·西方美术100讲`).

### Step 2 — Parse image blocks (caption extraction)

For each `![](URL)` in the body, grab the **3–5 lines immediately following**. They are the caption block. Patterns vary; expect:

```
艺术家中文 ArtistEN
作品中文 WorkEN  (sometimes original-language)
年代 / 材质 / 尺寸 / 现存地
```

Or reversed (work before artist), or only partial. Tolerate:

- Work title and artist on the same line
- Year on its own line: `公元前 450 年前后`
- Medium / location annotations: `大理石复制品`、`青铜原件作于…`
- Missing fields

Capture for the Step 4 checkpoint:

- **艺术家**：name_zh, name_en (if given)
- **作品**：name_zh, name_en, name_original (if non-English given), year, medium, dimensions, location
- The image **URL** itself
- The image's **extension** (`.png`/`.jpg`/`.jpeg`/`.webp` — preserve)

### Step 3 — Alias-search existing entities + check frontmatter backlinks

Before deciding what is "new":

- For every candidate entity (time period, school, person, technique, artwork), `grep -r "aliases:" 时代/ 流派/ 人物/ 技法/ 作品/` and check filename matches against `<中文>` / `<English>` / `<原文>` / known variants. One entity = one page.
- **Artworks are especially likely to be reused**: 《维纳斯的诞生》、《蒙娜丽莎》 appear in multiple lectures. If a folder `作品/<artwork>/` already exists, you reuse it — do NOT create a duplicate.
- For each frontmatter back-reference wikilink (e.g. `[[顾衡·西方美术100讲]]`), check resolution. **Preserve the EXACT string** — including any special CJK characters (radical `⼯` U+2F2F vs. normal `工` U+5DE5). If unresolved, plan to add the raw spelling as an alias on the matching wiki page (do NOT normalize).

### Step 4 — Checkpoint with user ← REQUIRED BEFORE ANY WRITES

Report in chat:

**一段话总结** (1 paragraph)

**实体清单**, 分六类（or whichever subset applies）:

```
时代: [新建] <bilingual> — 一句话理由 / [更新已有] [[<bilingual>]]
流派: ...
人物: ...
技法: ...
作品: ...
概念 (如有): ...
```

每个**新建项**附**双语命名提案** + **`pronunciation` 草稿**：

```
新建 人物 [波利克列特斯 Polykleitos]
  原文: Πολύκλειτος (Polýkleitos)  (古希腊语)
  pronunciation:
    original: /poliˈklitos/   ← 草稿，不确定
    en: /pɒliˈkliːtəs/        ← 草稿
    zh: 波-里-克-列-托斯
  aliases: [Polykleitos, 波里克列托斯, Πολύκλειτος]
```

**Frontmatter backlinks** found and how they'll resolve (alias to add, or already resolves).

**图片清单**（关键）：

```
图 1: https://piccdn3.umiwi.com/.../xxx.jpg
  -> 作品/掷铁饼者 Discobolus/01.jpg   [新作品首图]

图 2: https://piccdn3.umiwi.com/.../yyy.jpg
  -> 作品/持矛者 Doryphoros/03.jpg     [复用作品，追加为 03]
  (作品页已存在，前两张来自 lecture 015、037)
```

**冲突**（如有）→ 用 `⚠️` 显式列出："本篇说 X，wiki 现有 [[…]] 说 Y"。

**Proposed `来源/<lecture-title>.md` filename** (strip ` - 得到APP` 后缀)。

**Wait for the user.** They may rename pages, fix bilingual spellings, redirect emphasis, merge aliases, drop entities, or adjust image attribution. Do NOT proceed until they respond.

### Step 5 — Write `来源/<lecture-title>.md`

Per CLAUDE.md §3 source template:

- 一句话总结
- 核心论点
- 涉及实体（六类小节，全部 wikilinks）
- 与其他课程的连接
- 我的反应（**留空**）
- `## 原文`

Frontmatter:

```yaml
---
type: source
name_zh: <lecture title 中文部分>
name_en: <may be empty for source pages>
created: <today>
updated: <today>
sources: 1
tags: []
---
```

For `## 原文`: insert the verbatim raw body per CLAUDE.md §5「原文 insertion」rules.

**Strip**:
- Raw frontmatter (lines between `---` delimiters)
- The duplicate title+duration line at top of body (e.g. `002｜古希腊雕塑：为什么做得这么逼真？ 11分59秒`)
- 主讲人 line (`顾衡 亲述` / `转述：怀沙AI`)
- App UI line `添加到笔记`

**Keep verbatim** (no rewording, no fixing typos):
- Lecture body, paragraph breaks, `✵` separators if present
- 收束小诗 if present
- 注释 / footnote block — promote to `### 注释`
- 划重点 — promote to `### 划重点`

**Preamble (you write)**:
```
## 原文

> 来源：<source URL from raw frontmatter>
> 出处：[[顾衡·西方美术100讲]] · <duration>　<presenter line if present>
```

### Step 6 — Image localization to artwork folders

For each image identified in Step 2 (and confirmed in Step 4), in document order:

```bash
mkdir -p "作品/<bilingual>"
NN=$(printf "%02d" $(($(ls "作品/<bilingual>"/[0-9][0-9].* 2>/dev/null | wc -l) + 1)))
[ -f "作品/<bilingual>/${NN}.<ext>" ] || curl -fsSL --create-dirs \
  -o "作品/<bilingual>/${NN}.<ext>" "<url>"
```

- `<bilingual>` is the confirmed Step 4 artwork name, e.g. `掷铁饼者 Discobolus`.
- `NN` is **next available zero-padded index** in the folder. First image = `01`. Reused artwork — count existing files and increment.
- `<ext>` preserved from URL.
- **Dedup**: if any existing file in `作品/<bilingual>/` has `<!-- src: <this URL> -->` in its referencing 来源 pages (grep for it), the image was already downloaded by a prior ingest. Reuse that NN; don't re-download or create a new file.

Rewrite the body line in `## 原文`:

```markdown
![](作品/<bilingual>/NN.<ext>)
<!-- src: <original URL> -->
<!-- artwork: [[<bilingual>]] -->
```

The `artwork:` comment makes the back-link traceable even from inside 原文.

**Failure handling**: if `curl` fails (404, timeout, etc.), do NOT silently drop the image. Keep the original URL inline AND prepend a flag:

```markdown
<!-- ⚠️ download failed: <url> -->
![](<url>)
```

Surface the failure list in Step 10 report.

**NEVER write to `raw/assets/`** — that's the user's Obsidian-hotkey area.
**NEVER use root `assets/`** — this project's images live in `作品/<bilingual>/`.

### Step 7 — Create stubs / update existing entity pages

Per CLAUDE.md §3 templates.

**New entity** → stub with full type-specific scaffolding, populating only:

- `name_zh` / `name_en` / `name_original` / `original_lang` / `pronunciation` / `aliases`
- `created` / `updated` (today) / `sources: 1`
- `一句话定义` / `简介` (whichever is the type's first section)
- `## 出现在` listing this source

**Artwork pages (special)** — first ingest fills:

- All `基本信息` fields known from caption + (*not from wiki*) training-data補全 for missing fields like 现存地
- `## 图片清单` table with row 01:

```markdown
## 图片清单

| 编号 | 出自 | 描述 |
|---|---|---|
| 01 | [[002｜古希腊雕塑：为什么做得这么逼真？]] | 正面照 |
```

**Existing entity** → in `## 出现在` append the new source; update content sections (`核心特征` / `主要贡献` / `代表作品` / etc.) **only** if this source genuinely adds nuance.

On contradiction with an existing claim, add:

```markdown
> ⚠️ 与 [[<other source>]] 中的说法不同：<本篇说法>
```

Never overwrite. Bump `updated:` + `sources:` in frontmatter.

For artworks reused across lectures: append a new row to `## 图片清单` corresponding to the new NN; append the new source to `## 出现在`.

### Step 8 — Update `index.md`

Add new entries under their type section, one line each: `- [[<bilingual>]] — one-line summary`. For artworks include `artist · year · medium`. Include the new source under `## 来源 (Sources)` with today's date.

If an existing entity got a content nuance, do NOT re-emit its index line — the wikilink is unchanged.

### Step 9 — Append to `log.md` + `.ingested.tsv`

`log.md` entry — header MUST be parseable:

```
## [YYYY-MM-DD] ingest | <lecture title>
- 新建：来源(1) 时代(N) 流派(N) 人物(N) 技法(N) 作品(N) 概念(N)
- 更新：<page>, <page>, …
- 图片：下载 N，复用 M，失败 K
- 备注：<⚠️ flags / deferred decisions / anything noteworthy>
```

`来源(1)` is always exactly `1`. Other counts vary, including 0.

`.ingested.tsv` — append exactly one TAB-separated row:

```
<raw_path>\t<YYYY-MM-DD>\t<source_page>
```

Example:

```
raw/002｜古希腊雕塑：为什么做得这么逼真？ - 得到APP.md	2026-05-13	来源/002｜古希腊雕塑：为什么做得这么逼真？.md
```

- `<raw_path>` — exact path you were given.
- `<YYYY-MM-DD>` — today's date.
- `<source_page>` — the file from Step 5.

Append-only. Never reorder, never deduplicate, never edit prior rows. If state file is missing or lacks header, create it (header per existing project format).

### Step 10 — Report

Tell the user:

- Pages touched (count by type)
- `⚠️` flags raised
- Failed downloads (URL list)
- Anything that needs a follow-up source
- Any deferred naming decisions
- "State file updated" 一句

### Step 11 — DO NOT auto-commit

Leave the working tree dirty so the user can review the diff. Only commit if the user explicitly says so.

## Edge Cases

| Situation | Handling |
|---|---|
| Raw file unparseable | Stop. Report. Write nothing. |
| Ambiguous entity (could be 2 existing pages) | Fuzzy-match aliases first; ask user if unresolved. |
| Source contradicts an existing wiki claim | `⚠️` flag inside the entity page; surface in Step 10. Do not edit the contradicted claim. |
| Caption gives only Chinese, no English | At Step 4, propose an English rendering from training data, mark as "建议命名"; wait for user OK. If user rejects, fall back to "暂译" prefix or transliteration. |
| English known but Chinese name conflicts with existing entity for a different referent | Disambiguate filename: `荷拉斯兄弟之誓 (大卫) Oath of the Horatii`. Flag in Step 4. |
| Same artwork referenced in different lectures with slightly different image angles | One folder, append-only image numbers (`02`, `03` …). Image clipping list table tracks per-row 出自 lecture. |
| Raw body has external image URLs (`piccdn3.umiwi.com`) | Localize per Step 6. CDN may expire; static publish needs local files. |
| Image download fails (404, timeout) | Don't drop. Keep URL inline + `<!-- ⚠️ download failed: <url> -->` flag. Surface in Step 10. |
| Original-language name uses CJK radical or non-standard char (e.g. `⼯` U+2F2F) | Add the raw spelling as an alias; do NOT normalize. |
| Lecture references images in `raw/assets/` | You may view them for context. Do not embed them into wiki pages unless the user asks. |
| Batch request (>1 file) | Confirm explicitly — default is one source at a time (CLAUDE.md §10). Use `/art-scan` for batch dispatch. |
| IPA pronunciation uncertain | Leave the relevant sub-field empty. Never guess. |
| Caption lists artwork without year | Mark `date:` as `年代不详`; do NOT invent. |

## Common Mistakes

| Mistake | Fix |
|---|---|
| Editing wiki pages before the Step 4 checkpoint | Always checkpoint first — this is the single most-skipped step |
| Creating a duplicate page because alias-search was skipped | Step 3 is non-optional; grep `aliases:` across the whole wiki |
| Creating a duplicate **作品 folder** because caption was reparsed differently than prior ingest | Step 3 explicitly searches `作品/*/` folder names AND `aliases:` in their .md files |
| Filename in Chinese only (no English) | Bilingual filename is mandatory (CLAUDE.md §3 / §4) |
| Putting images into root `assets/` instead of `作品/<bilingual>/` | Wrong target dir. Re-read CLAUDE.md §5.3 |
| Guessing IPA when unsure | Leave the sub-field empty. Wrong IPA worse than no IPA. |
| Overwriting an existing claim | Use `⚠️ 与 [[…]] 中的说法不同：…`, never silent overwrite |
| Writing to `raw/` (e.g., fixing a typo) | `raw/` is immutable. Read only. |
| Forgetting to bump `updated:` / `sources:` on touched entity pages | Update frontmatter on every page you edit |
| Using English filenames or English headings | Page filenames are bilingual (中文 English); section headings are 中文 |
| Committing without being asked | Step 11 — leave the diff for the user to review |
| Filling in `## 我的反应` on the source page | That section is the user's; leave it blank |
| Forgetting to append to `.ingested.tsv` | Step 9 is mandatory — `/art-scan` depends on it |
| Re-writing or reordering existing rows in `.ingested.tsv` | Append-only |
| Forgetting `## 原文` in 来源 page | The page MUST be self-contained for static-HTML publish |
| Normalizing CJK radicals or original-language characters | Add as alias instead |
| Leaving CDN image URLs (`piccdn3.umiwi.com`) inline in `## 原文` | Localize per Step 6 |
| Writing image downloads into `raw/assets/` | That's the user's Obsidian-hotkey area |
| Putting `(*not from wiki*)` everywhere out of caution | Use it ONLY for training-data補全; sourced claims don't need it |

## Red Flags — STOP

- About to call `Write` / `Edit` on a wiki file before the user has responded to the Step 4 checkpoint
- About to call `Write` / `Edit` on anything under `raw/`
- About to create `人物/X.md` without having grepped `aliases:` for X across the wiki
- About to create `作品/<bilingual>/` without checking whether the folder already exists
- About to finish without appending to `.ingested.tsv`
- About to rewrite or reorder rows in `.ingested.tsv` (it is append-only)
- About to write a 来源 page without `## 原文` section
- About to leave a `https://piccdn3.umiwi.com/...` URL inline in `## 原文` instead of downloading
- About to write image files to `raw/assets/` (LLM never writes there)
- About to use root `assets/` instead of `作品/<bilingual>/`
- About to write a page with `name_en: ""` (bilingual is mandatory)
- About to fill IPA you're not sure about
- Auto-running `git commit` at the end of the workflow

All of these mean: **stop, back up, re-read CLAUDE.md §5 / §9.**

# CLAUDE.md — 西方美术 100 讲 Wiki

## 1. 项目概述

This is an LLM-maintained personal wiki for 顾衡《西方美术 100 讲》(DeDao app), a 100-lesson course on Western art history. Sources are clipped Chinese articles in `raw/`. The wiki itself is in Chinese with English bilingual entity names, organized as an interlinked Obsidian vault. You (the LLM) maintain it; the user curates sources and asks questions.

Design rationale and history: see `_meta/specs/2026-05-13-art-wiki-design.md`.

## 2. 三层架构

- **`raw/`** — IMMUTABLE. Read only. Never write. Never modify.
- **Wiki folders** (`时代/`、`流派/`、`人物/`、`技法/`、`作品/`、`来源/`、`概念/`) — your responsibility. Create, update, link.
- **`CLAUDE.md`** — this file. Co-evolved with the user; propose updates rather than silent edits.

## 3. 页面规范

Every wiki page MUST have frontmatter:

```yaml
---
type: era | school | person | technique | artwork | source | concept | course
name_zh: <中文>
name_en: <English>            # artwork/person/school/technique/era 必填
name_original: <原文>          # 当原文非英文（希腊/拉丁/意/法/荷/德…）时必填
original_lang: <语言名>        # 配 name_original，如 "古希腊语"、"意大利语"
pronunciation:                 # 选填；专有名词建议填
  original: /poliˈklitos/      # 原语言 IPA（主要参考）
  en: /pɒliˈkliːtəs/           # 英语习用 IPA（选填）
  zh: 波-里-克-列-托斯          # 中文音节切分（选填）
aliases: [所有变体, 旧译名, 异体拼写, 包括用户可能在 wikilink 里使用的任何形式]
created: YYYY-MM-DD
updated: YYYY-MM-DD
sources: <整数>
tags: []                       # 选填，按需添加
---
```

**`pronunciation` 简写**：单字符串形式 `pronunciation: /poliˈklitos/` 默认按 `original` 解读。
**IPA 不确定 → 留空**，不要瞎写。错的 IPA 比没有更糟。

Standard sections by type:

### `时代/<中文 English>.md` — type: era
- 一句话定义
- 时间范围
- 历史背景
- 主要流派 (`[[…]]`)
- 代表人物
- 代表作品
- 出现在

### `流派/<中文 English>.md` — type: school
- 一句话定义
- 时间范围
- 所属时代 (`[[…]]`)
- 核心特征
- 代表人物
- 代表作品
- 与其他流派的关系
- 出现在

### `人物/<中文 English>.md` — type: person
- 简介
- 生卒年
- 所属流派 (`[[…]]`)
- 主要贡献
- 代表作品
- 师承与影响
- 出现在

### `技法/<中文 English>.md` — type: technique
- 一句话定义
- 原理 / 操作
- 起源
- 典型作品
- 相关技法
- 出现在

### `作品/<中文 English>/<中文 English>.md` — type: artwork

Folder-per-artwork with self-titled folder note. The folder name and the `.md` filename are identical bilingual strings. Images live in the same folder as `NN.<ext>`.

Required sections:

- 基本信息（作者 `[[…]]`、创作年代、材质、尺寸、现存地）
- 画面与技法
- 历史背景 `(*not from wiki*)` ← 训练数据补全部分必须打这个标
- 图片清单 (markdown table: 编号 / 出自 lecture / 描述)
- 出现在

### `来源/<lecture title>.md` — type: source

- 一句话总结
- 核心论点
- 涉及实体（按 时代 / 流派 / 人物 / 技法 / 作品 分小节，全部 `[[wikilink]]`）
- 与其他课程的连接
- 我的反应（**留空给用户**，禁止 LLM 填）
- `## 原文`（自包含正文，图片重写为 `作品/<bilingual>/NN.ext`，见 §5「原文 insertion」）

### `概念/<中文 English>.md` — type: concept

查询沉淀用 + 承载课程里出现的"类型/母题/事件"类抽象实体（如 `库罗斯 Kouros`、`Venus pudica`）。

- 一句话定义
- 详细解释
- 相关概念 / 流派 / 人物 / 技法
- 出现在
- 引用 source

**Folder-per-concept（选用）**：当一个概念需要承载图片（如雕像类型样本图），可以与作品同样用文件夹模式：`概念/<中文 English>/<中文 English>.md` + `01.jpg` ...。仅在需要图片时启用，不强制。

### `课程/<课程全名>.md` — type: course

课程级别的元数据页（如 `顾衡·西方美术100讲`）。所有 lecture 的 raw frontmatter `author:` backlink 指向这里。

- 简介
- 主讲人
- 章节结构（按时代/板块分组）
- 包含的全部 lecture（`[[…]]` 列表，自动维护）
- 出现在 / 被引用

## 4. 命名约定

- **所有实体页文件名是双语**：`<中文> <English>.md`。例：`波利克列特斯 Polykleitos.md`。中文在前，空格分隔，英文 / 拉丁化在后。
- **作品**：文件夹与内部 `.md` 同名，都用双语，例：`作品/掷铁饼者 Discobolus/掷铁饼者 Discobolus.md`。
- **wikilink 形态**：以双语全名为权威。所有变体（纯中文、纯英文、原文、旧译）都在 `aliases:` 里。Obsidian 别名解析 → 唯一页。
- **frontmatter `type:`** 是英文枚举（`era | school | person | technique | artwork | source | concept`）—— 稳定、可 dataview 查询。**目录名**和**人类可读计数**用中文（`时代/`、`时代(N)`）。
- **一个实体 = 一页**。新建前 alias-search 整个 wiki。命中已有 → 链接它，绝不复制。
- **时代 vs 流派**：时代 = 纯时间段（`古典时代`、`文艺复兴期`、`巴洛克时期`、`启蒙时代`、`19世纪`、`现代`、`当代`）。流派 = 所有有名的 "主义" 或学派（`拜占庭艺术`、`哥特艺术`、`威尼斯画派`、`矫饰主义`、`巴洛克`、`洛可可`、`新古典主义`、`印象派` …）。`巴洛克` 本身是流派，链接到 `[[巴洛克时期]]`。
- **同义实体歧义**：一个画派同时活跃于两个时代 → 在 `所属时代:` 列两个 wikilink。一个作品有多个被广泛使用的标题（如《维纳斯的诞生》既叫 Birth of Venus 也叫 La nascita di Venere）→ 都进 aliases。

## 5. 工作流：ingest

权威工作流见 `.claude/skills/art-ingest/SKILL.md`。下面是规范层面的关键点。

**触发**：用户把 `raw/` 文件名给你 + 说 "ingest"。或者 `/art-ingest <path>`。或者 `/art-scan` 调度过来。

**核心非协商点（Step 4 Checkpoint）**：抽完实体清单 + 图片清单 + 双语命名提案后，**先报告给用户、等回话，再写任何 wiki 文件**。

### 5.1 实体抽取要点

正文里实体出现形态多样：

- **作品**通常嵌在图片块附近：`![](URL)\n艺术家中英\n作品名中英\n年代`。抓 `![]` 后 3–5 行 caption 作为元数据来源。
- **人物**：caption 里给中英对；正文里可能只给中文。中文要回查 caption / 训练数据补 English。
- **流派**：标题层或段首"什么是 X"。
- **时代**：通过流派的时间范围推断 + 显式提及（"文艺复兴"、"巴洛克时期"）。
- **技法**：正文里加粗或单独成段（`S 造型`、`失蜡法`、`七头身比例`）。

### 5.2 双语命名生成规则

**优先级**：
1. raw caption 已给的 中+英 对 → 直接用。
2. raw 只有中文，但训练数据有公认 English → 用训练数据，并在 Checkpoint 明确说"建议命名"。
3. 仅 LLM 译名（无公认对照）→ 在 Checkpoint 标注 "暂译"，等用户确认。

**原文（非英文）的处理**：
- 古希腊 → 希腊字母 + 拉丁化转写：`Πολύκλειτος (Polýkleitos)`
- 拉丁 → 拉丁原文：`Discobolus`
- 意 / 法 / 荷 / 德 → 原拼写：`La nascita di Venere`、`L'École d'Athènes`
- 不写未经核查的非英文译名

### 5.3 原文 insertion 与图片本地化

来源页 `## 原文` 必须自包含（静态 HTML 发布不暴露 `raw/`）。

**剥离**：
- raw frontmatter（`---` 包围块）
- 首行标题 + 时长（`002｜… 11分59秒`）
- `X 亲述` / `转述：X` 行
- `添加到笔记`

**保留**：
- 正文段、空行、`✵` 分隔符
- 收束诗
- 注释 → 升 `### 注释`
- 划重点 → 升 `### 划重点`

**图片处理（关键差异）**：raw 的 `![](https://piccdn3.umiwi.com/...)` 不能保留外链。落地到 `作品/<bilingual>/NN.<ext>` 并改写引用：

```bash
mkdir -p "作品/<bilingual>"
NN=$(printf "%02d" $(($(ls "作品/<bilingual>"/[0-9][0-9].* 2>/dev/null | wc -l) + 1)))
[ -f "作品/<bilingual>/${NN}.<ext>" ] || curl -fsSL --create-dirs \
  -o "作品/<bilingual>/${NN}.<ext>" "<url>"
```

来源页 `## 原文` 的引用改为：

```markdown
![](作品/<bilingual>/NN.<ext>)
<!-- src: <original URL> -->
<!-- artwork: [[<bilingual>]] -->
```

**同一作品跨 lecture 复用**：作品文件夹只创建一次。后续 ingest 往该文件夹**追加图片**（02、03 …）。同一 URL 已下过 → 通过对比 `<!-- src: -->` 注释跳过、复用旧编号。

**下载失败**：保留原 URL inline + `<!-- ⚠️ download failed: <url> -->`，Step 9 报告。

**两个 `assets/` 角色**：本项目主要图片落点是 `作品/<bilingual>/`，不再用根 `assets/`。`raw/assets/` 是用户 Obsidian 热键的落点，LLM 永不写入。

### 5.4 写入顺序

1. 通读 raw
2. 解析图片块 caption
3. Alias 去重
4. **Checkpoint**（等用户确认）
5. 写 `来源/<…>.md`（含 `## 原文`，图片改写）
6. 图片本地化（curl）
7. 实体页 stub / update
8. 更新 `index.md`
9. 追加 `log.md` + `.ingested.tsv`
10. 报告 + **不**自动 commit

## 6. 工作流：query

1. 读 `index.md` 找候选页。
2. 按 时代 → 流派 → 人物 → 技法 → 作品 的语义层次读相关页。
3. 综合作答，每个事实带 `[[wikilink]]`。
4. 训练数据补充打 `(*not from wiki*)`。
5. 答案 ≥200 字 OR 连接 ≥2 个未文档化概念 → 主动问是否回填 `概念/<name>.md`。

输出形式：markdown 散文 / 比较表 / mermaid 图谱 / dataview 块。

### 引用规则

- 每条主张 `[[wikilink]]` 到 source 页
- 训练数据事实 `(*not from wiki*)`
- 不静默 web 兜底。Wiki 缺 → 标记 gap 或问用户后再 web 搜

## 7. 工作流：lint

触发：用户说 "lint" 或 ~10 次 ingest 之后。

检查项：

1. 孤儿页（零入链）
2. stub（≥3 sources 仍只有一句话定义）
3. 缺页（内联 `[[…]]` 无文件）
4. `⚠️` 未决（历史 ingest 留下的冲突）
5. 过时声明（`updated:` 旧于最新引用 source）
6. 断 wikilink
7. frontmatter 完整性（`name_zh` / `name_en` 缺失、`type` 错枚举、`aliases` 撞车）
8. `index.md` 漂移
9. **作品文件夹特检**：`index.md` 图片清单 ↔ 实际 jpg 数量、`<!-- src: -->` 注释存在性
10. `pronunciation` 留空率（不强制，仅报告）

输出 markdown 报告，**不**自动修。结尾给 3–5 条"建议补充的 source / 待挖掘的 question"。

## 8. 索引与日志格式

### `index.md`

```markdown
# Wiki Index

## 时代 (Eras)
- [[<bilingual>]] — one-line summary

## 流派 (Schools)
- [[<bilingual>]] — one-line summary

## 人物 (People)
- [[<bilingual>]] — one-line bio

## 技法 (Techniques)
- [[<bilingual>]] — one-line summary

## 作品 (Artworks)
- [[<bilingual>]] — artist · year · medium

## 概念 (Concepts)
- [[<bilingual>]] — one-line summary

## 来源 (Sources)
- [[<lecture title>]] — YYYY-MM-DD ingested
```

### `log.md`

Append-only. Each entry header must be `grep`-parseable: `grep "^## \[" log.md | tail -10`.

```
## [YYYY-MM-DD] <event-type> | <subject>
- 新建：来源(1) 时代(N) 流派(N) 人物(N) 技法(N) 作品(N) 概念(N)
- 更新：<list>
- 图片：下载 N，复用 M，失败 K
- 备注：<⚠️ 列表 / deferred decisions / 任何 noteworthy>
```

Event types: `ingest`、`query`、`lint`、`synthesis-filed`、`schema-update`。

## 9. 我不该做的事

- 写 `raw/`。永远只读。
- 静默覆盖冲突声明。永远用 `> ⚠️ 与 [[…]] 中的说法不同：…`。
- 训练数据事实不打 `(*not from wiki*)`。
- 为已有别名实体新建重复页。
- 跳过 Step 4 ingest checkpoint。
- 未问就 web 搜。
- 漏 `## 原文` 区块（来源页必须自包含）。
- 双语命名只填中文（漏 `name_en`）。
- IPA 不确定瞎填（宁可留空 `pronunciation:`）。
- 把图片放进根 `assets/`（本项目落点是 `作品/<bilingual>/`）。
- 写 `raw/assets/`（用户 Obsidian 热键专用区）。
- 自动 `git commit`。

## 10. 与你协作

- **Ingest checkpoint**（Step 4）：抽完实体 + 双语命名提案 + 图片清单 → 报告 → 等用户回话再写。
- **双语命名歧义**：用户没用过的暂译要标 "建议" 或 "暂译"，等 Checkpoint 拍板。
- **Synthesis-filing**：query 出非平凡答案 → 主动问是否回填 `概念/`。
- **Schema 演化**：发现规律性新模式 → 提议 `CLAUDE.md` 更新，不静默调整行为。
- **默认一次一篇**。批量 ingest 仅在用户明确请求时启动（走 `/art-scan`）。

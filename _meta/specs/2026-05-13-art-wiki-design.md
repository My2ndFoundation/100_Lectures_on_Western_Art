---
title: 西方美术 100 讲 Wiki — 设计文档
date: 2026-05-13
status: accepted
adapted_from: ../../DeDao-100 Modern Thinking Tools/CLAUDE.md
---

# 西方美术 100 讲 Wiki — 设计文档

LLM 协同维护的个人知识库，覆盖顾衡《西方美术 100 讲》。基于 DeDao-100 项目同源架构，针对艺术史领域做了三处关键调整：实体维度、命名约定、作品文件夹。

## §1 — 整体架构

**三层**（继承 DeDao）：

- **`raw/`** 不可变。100 篇得到 App 剪藏，LLM 只读。
- **Wiki 实体目录** LLM 拥有：`时代/`、`流派/`、`人物/`、`技法/`、`作品/`、`来源/`，外加 `概念/`（query 沉淀用）。
- **`CLAUDE.md`** schema，人机共同演化。

**目录命名全部中文**，与 DeDao 一致。Frontmatter `type:` 用英文枚举：`era | school | person | technique | artwork | source | concept`。

**与 DeDao 关键差异**：

| 维度 | DeDao | Art |
|---|---|---|
| 实体目录 | 工具 / 概念 / 人物 / 著作 | 时代 / 流派 / 人物 / 技法 / **作品**（新） |
| 文件名 | 纯中文 | **中英双语**（必要时含原文） |
| 图片归属 | `assets/<lesson>/NN.ext` | **`作品/<bilingual>/NN.ext`** |
| 实体跨 lecture 行为 | 实体页 update | 同上 + **作品文件夹累积图片** |

**底层不变**：`index.md`、`log.md`、`.ingested.tsv`、`/art-scan` + `/art-ingest` skill 模式、checkpoint 流程、`⚠️` 冲突标记、`(*not from wiki*)` 训练数据标记、`## 原文` 自包含约定。

## §2 — 页面规范

### Frontmatter

```yaml
---
type: era | school | person | technique | artwork | source | concept
name_zh: <中文>
name_en: <English>            # artwork/person/school/technique/era 必填
name_original: <原文>          # 当原文非英文时必填
original_lang: <语言名>        # 配 name_original
pronunciation:                 # 选填，专有名词建议填
  original: /poliˈklitos/      # 原语言 IPA（主要参考）
  en: /pɒliˈkliːtəs/           # 英语习用 IPA（选填）
  zh: 波-里-克-列-托斯          # 中文音节切分（选填）
aliases: [所有变体, 旧译名, 异体拼写]
created: YYYY-MM-DD
updated: YYYY-MM-DD
sources: <整数>
---
```

`pronunciation` 也可写单字符串：`pronunciation: /poliˈklitos/`（默认按 original 解读）。
IPA 不确定 → 留空，**不要瞎写**。

### Section 模板（按 type）

**`时代/<中文 English>.md`** · type: era
- 一句话定义
- 时间范围
- 历史背景
- 主要流派 `[[…]]`
- 代表人物
- 代表作品
- 出现在

**`流派/<中文 English>.md`** · type: school
- 一句话定义
- 时间范围
- 所属时代 `[[…]]`
- 核心特征
- 代表人物
- 代表作品
- 与其他流派的关系
- 出现在

**`人物/<中文 English>.md`** · type: person
- 简介
- 生卒年
- 所属流派 `[[…]]`
- 主要贡献
- 代表作品
- 师承与影响
- 出现在

**`技法/<中文 English>.md`** · type: technique
- 一句话定义
- 原理/操作
- 起源
- 典型作品
- 相关技法
- 出现在

**`作品/<中文 English>/<中文 English>.md`** · type: artwork
- 基本信息（作者、年代、材质、尺寸、现存地）
- 画面与技法
- 历史背景 `(*not from wiki*)` 训练数据补全部分必须标
- 图片清单（表格：编号 / 出自 lecture / 描述）
- 出现在

**`来源/<lecture title>.md`** · type: source
- 一句话总结
- 核心论点
- 涉及实体（按 时代 / 流派 / 人物 / 技法 / 作品 分类，全部 `[[wikilink]]`）
- 与其他课程的连接
- 我的反应（留空给用户）
- `## 原文`（自包含正文，图片重写为 `作品/<bilingual>/NN.ext`）

**`概念/<中文 English>.md`** · type: concept（query 沉淀用，非必备）
- 一句话定义
- 详细解释
- 相关概念 / 流派 / 人物 / 技法
- 出现在 / 引用 source

### 命名一致性

所有 `<中文 English>` 字段是同一个 bilingual 字符串，作为文件名、文件夹名（作品）、wikilink 目标、graph 节点。这保证：

- Obsidian graph view 节点名直接是双语标题
- `[[Mona Lisa]]` 和 `[[蒙娜丽莎]]` 都通过 `aliases` 解析到唯一页

### 作品文件夹（self-titled folder note）

```
作品/
└── 掷铁饼者 Discobolus/
    ├── 掷铁饼者 Discobolus.md   ← 与文件夹同名，做"folder note"
    ├── 01.jpg                  ← 来自 lecture 002
    ├── 02.jpg                  ← lecture 037 引用的另一角度
    └── 03.jpg                  ← lecture 045 细节
```

Obsidian 不需插件即识别 `[[掷铁饼者 Discobolus]]`；graph 节点是作品标题，不是 "index"。

## §3 — Ingest 工作流

**触发**：`/art-ingest raw/<lecture>.md` 或自然语言 "ingest 那篇巴洛克"。

**Step 1 — 通读 raw**
读完 frontmatter + 正文。识别：板块、主旨、提到的 时代 / 流派 / 人物 / 技法 / 作品、与其他 lecture 的交叉引用。

**Step 2 — 解析图片块**
对正文里每个 `![](URL)`：抓后续 3–5 行 caption，提取艺术家（中+英）、作品标题（中+英+原文）、年代、材质、尺寸、现存地。caption 格式不规整 → 容忍标题/作者次序变化、年代独立行、字段缺失。

**Step 3 — Alias 去重搜索**
对所有候选实体跑 `grep aliases:`。**作品**尤其关键：跨 lecture 复用。命中 → 复用页面；未命中 → 标记新建。

**Step 4 — Checkpoint（写文件前必须）**
聊天里报告：
- 一段话总结
- 实体清单按 时代 / 流派 / 人物 / 技法 / 作品 分类
- 每项标 **新建 stub** 或 **更新 `[[…]]`**
- 每个新建项的**双语命名提案** + `pronunciation` 草稿（IPA 不确定就留空）
- 图片清单：URL → 拟落地路径 `作品/<bilingual>/NN.ext`，标明是新作品首图还是复用作品追加图
- `⚠️` 与现有 wiki 的冲突

**等用户确认后**才继续。用户可纠正双语名、合并别名、删去无关实体、调整图片归属。

**Step 5 — 写 `来源/<lecture title>.md`**
按 §2 来源模板。`## 原文` 区块：
- 剥离：raw frontmatter、首行标题+时长、`X 亲述/转述`、`添加到笔记`
- 保留：正文、`✵`、收束诗、注释（升 `### 注释`）、划重点（升 `### 划重点`）
- 图片重写：`![](作品/<bilingual>/NN.ext)` + 注释 `<!-- src: <url> --><!-- artwork: [[<bilingual>]] -->`

**Step 6 — 图片本地化到作品文件夹**

```bash
mkdir -p "作品/<bilingual>"
NN=$(printf "%02d" $(($(ls "作品/<bilingual>"/[0-9][0-9].* 2>/dev/null | wc -l) + 1)))
[ -f "作品/<bilingual>/${NN}.<ext>" ] || curl -fsSL --create-dirs \
  -o "作品/<bilingual>/${NN}.<ext>" "<url>"
```

- 同一作品多 lecture 复用 → `NN` 递增（02、03 …）
- 同一图 URL 已存在（旧 ingest 下过）→ 用 `<!-- src: -->` 注释比对、跳过、复用旧编号
- 失败：保留原 URL inline + `<!-- ⚠️ download failed: <url> -->`，Step 9 汇总

**Step 7 — 实体页 stub / 更新**

- **新建**：写 type-specific 全套 section 骨架（§2），只填 `name_*` / `pronunciation` / `一句话定义` / `## 出现在 [[<source>]]`
- **作品页**：除上述外，**必填表格"图片清单"**（编号 / 出自 / 描述），首次 ingest 即录入 01
- **已存在**：在 `## 出现在` 追加 source；只在新增 nuance 时改正文段；冲突用 `⚠️ 与 [[…]] 中的说法不同：…`，不静默覆盖；bump `updated:` + `sources:`

**Step 8 — 更新 `index.md`**
在对应 type section 加一行：`- [[<bilingual>]] — 一句话`。来源页加到 `## 来源` 并附今日日期。

**Step 9 — 追加 `log.md` + `.ingested.tsv`**

```
## [YYYY-MM-DD] ingest | <lecture title>
- 新建：来源(1) 时代(N) 流派(N) 人物(N) 技法(N) 作品(N)
- 更新：<pages>
- 图片：下载 N，复用 M，失败 K
- 备注：<⚠️ / deferred / notable>
```

`.ingested.tsv` 追加一行：`<raw_path>\t<YYYY-MM-DD>\t<source_page>`

**Step 10 — 报告 + 不自动 commit**
报告触动页数、`⚠️` 列表、失败下载、需后续 source 的 gap。留 dirty tree 给用户 review。

## §4 — Query / Lint / 硬约束

### Query

1. 读 `index.md` 找候选页
2. 按 时代 → 流派 → 人物 → 技法 → 作品 的语义层次读相关页
3. 综合作答，每个事实带 `[[wikilink]]`；训练数据事实打 `(*not from wiki*)`
4. 若答案 ≥200 字或连接 ≥2 个未文档化概念 → 主动询问回填 `概念/<name>.md`

输出形式按问题选：markdown 散文 / 比较表 / mermaid 图谱 / dataview 块。

### Lint

触发：用户说 "lint" 或 ~10 次 ingest 之后。检查：

1. 孤儿页（零入链）
2. stub（≥3 sources 仍只有一句话定义）
3. 缺页（内联 `[[…]]` 无文件）
4. `⚠️` 未决
5. 过时声明（`updated:` 旧于最新引用 source）
6. 断 wikilink
7. frontmatter 完整性（`name_zh`/`name_en` 缺失、`type` 错枚举、`aliases` 撞车）
8. index 漂移
9. **作品文件夹特检**：index.md 图片清单 ↔ 实际 jpg 数量、`<!-- src: -->` 注释存在性
10. `pronunciation` 留空率（不强制）

输出 md 报告，**不**自动修。结尾给 3–5 条"建议补充的 source / 待挖掘的 question"。

### 硬约束（CLAUDE.md §9）

- `raw/` 永远只读
- 跳过 Step 4 checkpoint = 错
- 命名前不做 alias 搜索 = 错
- 静默覆盖冲突 = 错（用 `⚠️`）
- 训练数据不打 `(*not from wiki*)` = 错
- 写 `raw/assets/` 或漏 `## 原文` = 错
- 双语文件名只写中文 = 错
- caption 图片放进根 `assets/` 而非作品文件夹 = 错
- IPA 不确定瞎填 = 错
- 自动 `git commit` = 错

## 实施清单

落地文件：

- `_meta/specs/2026-05-13-art-wiki-design.md`（本文）
- `CLAUDE.md`
- `README.md`
- `index.md`、`log.md` 骨架
- `.ingested.tsv`（仅 header）
- `.claude/skills/art-ingest/SKILL.md`
- `.claude/skills/art-scan/SKILL.md`
- `.claude/settings.local.json`
- `.gitignore` 补丁
- 顶层目录：`时代/`、`流派/`、`人物/`、`技法/`、`作品/`、`来源/`、`概念/`
- `_meta/specs/`、`_meta/plans/`

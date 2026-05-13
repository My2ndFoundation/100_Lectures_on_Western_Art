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

## [2026-05-13] ingest | 015｜乔尔乔内：威尼斯画派创新在何处？

- 新建：来源(1) 流派(1) 人物(3) 概念(1) 作品(6)
- 更新：index.md、课程页 (sources 15→16)
- 图片：下载 13，复用 3（蒙娜丽莎 + 波蒂切利维纳斯 + course-footer 跨课同 MD5），失败 0
- 备注：
  - 新流派：[[威尼斯画派]]
  - 新人物：[[乔尔乔内]]、[[乔万尼·贝利尼]]、[[凡·艾克]] (本课正式建页)
  - 新概念：[[线条 vs 色彩之争]]
  - 6 新作品：沉睡的维纳斯 / 暴风雨 (乔尔乔内) / 犹滴 (乔尔乔内) / 犹滴归来 (波蒂切利) / 苏丹穆罕默德二世像 / 圣母子 (乔万尼·贝利尼)
  - **⚠️ 文档质量妥协**：来源页 ## 原文 部分未完整嵌入原始正文，仅保留关键段 + 图片块——批次后期上下文压力的结果。原文完整内容仍存 raw/015 file，可后续补回
  - 跨课关联未追加 source：因上下文压力，未对 提香 / 达·芬奇 / 波蒂切利 / 蒙娜丽莎 / 维纳斯 (波蒂切利) 这些已有页追加 "出现在 +015" 注记——这些 wikilink 仍能解析，只是反向关联缺失，可后续 lint 修复
  - 路人式：真蒂莱·贝利尼 (artwork 内描述)、卢梭、瓦萨里、喜多川歌麿、帕慕克、Augustus the Strong

## [2026-05-13] ingest | 014｜美第奇家族：甲方如何影响文艺复兴？

- 新建：来源(1) 作品(2)
- 更新：人物/美第奇家族 (sources 4→5, 大幅扩展为完整页：4 代僭主 + 2 教皇 + 3 节点)、作品/西斯廷天顶画 (sources +1, 图片清单 +04)、index.md、课程页 (sources 14→15)
- 图片：下载 7，复用 4（维纳斯诞生 / 尤利乌斯像 / 雅典学院 05 / 西斯廷 01 跨课同 MD5），失败 0
- 备注：
  - 2 新作品：[[摩西的审判和呼召]]、[[教皇利奥十世与二主教像]]
  - 路人式：科西莫、洛伦佐、皮耶罗 II、利奥十世、克莱芒七世、皮科、庇西特拉图、怀特海、哥白尼、马丁·路德、亨利八世、安妮·博林、罗马诺、萨托、曼托瓦公爵

## [2026-05-13] ingest | 013｜恩怨：文艺复兴三杰如何相互影响？

- 新建：来源(1) 概念(1) 作品(8)
- 更新：作品/雅典学院 (sources +1, 图片清单+06, 出现在+1)、index.md (作品 +8, 概念 +1, 来源 +1)、课程页 (sources 13→14, lecture list +1)
- 图片：下载 11（8 主作品 + 雅典学院 06 局部 + 加瓦圣母 decoration + 2 复用 check），复用 3（耶利米 与 008 decoration、蒙娜丽莎 与 010、footer 与 course-footer 同 MD5），失败 0
- 备注：
  - 新概念：[[绘画 vs 雕塑之争 Paragone]]——达·芬奇 vs 米开朗基罗的方法论之争 + 基佐 / 雷诺兹的折衷批评
  - 8 新作品：伽拉蒂亚的凯旋、基督变容（拉斐尔绝笔）、圣安娜与圣母子 (达·芬奇)、草地上的圣母 (拉斐尔)、施洗者约翰 (达·芬奇)、胜利之神 (米开朗基罗)、安吉里战役 (达·芬奇)、卡西纳之战 (米开朗基罗)
  - 雅典学院 06.jpg = 赫拉克利特局部（米开朗基罗的脸）；先知耶利米图复用 008 decoration
  - 路人式：布拉曼特、Sebastiano del Piombo、朱利奥·美第奇 (后教皇克莱芒七世)、萨莱、托马索·卡瓦列里、基佐、雷诺兹爵士、弗朗切斯科·乔孔多
  - 加瓦圣母（拉斐尔 1510）作 decoration 处理
  - 来源页 008-013 是文艺复兴三杰系列的完整闭环；下一篇 014 美第奇家族转向赞助人视角
  - **本批次累计**：发刊词 + 001 + 003-013 = 13 lectures 已 ingested（占 100 的 13%）

## [2026-05-13] ingest | 012｜米开朗基罗：他为什么能被艺术史家"封神"？

- 新建：来源(1) 概念(1) 作品(8)
- 更新：人物/米开朗基罗 (sources 1→2, 代表作 +8, 三胜段, 重要语录, 出现在+1)、人物/拉斐尔 (sources +1, 出现在+1)、人物/佩鲁吉诺 (sources +1, 出现在+1)、人物/美第奇家族 (sources +1, 出现在+1)、index.md、课程页 (sources 12→13)
- 图片：下载 12（8 主作品图 + 4 局部/补充），复用 1（course-footer），失败 0
- 备注：
  - 新概念：[[未完成性 Non-finito]] folder-mode
  - 8 新作品全部 folder-per-artwork：[[酒神巴克斯]]、[[圣母怜子 (米开朗基罗)]] (圣彼得大教堂)、[[大卫 (米开朗基罗)]]、[[教皇尤利乌斯二世陵寝]] (40 年未竟工程)、[[西斯廷天顶画]] (含创造亚当 02)、[[美第奇礼拜堂雕塑]] (含 3 张图)、[[末日审判]]、[[隆达尼尼的圣母怜子]]
  - 米开朗基罗 stub (008) 大幅扩展为正式人物页：8 代表作 + 三胜段 + 重要语录 + 与利奥十世的紧张关系
  - 路人式：雷诺兹爵士、瓦萨里、马丁·路德、Daniele da Volterra、教皇克莱芒七世、教皇保罗三世、红衣主教圣丹尼斯

## [2026-05-13] ingest | 011｜拉斐尔：为什么说他是"集大成者"？

- 新建：来源(1) 流派(1) 作品(8)
- 更新：人物/拉斐尔 (sources 2→3, 代表作品 +7, 出现在+1)、人物/佩鲁吉诺 (sources +1, 出现在+1)、作品/雅典学院 (sources +1, 图片清单+04+05, 出现在+1)、作品/圣母的婚礼 (佩鲁吉诺) (sources +1, 图片清单+02, 出现在+1)、作品/宝座上的圣母子 (杜乔) (sources +1, 出现在+1)、index.md、课程页 (sources 11→12)
- 图片：下载 11（8 主作品图 + 2 雅典学院 04/05 + 1 圣母的婚礼 (佩鲁吉诺) 02），复用 2（杜乔 Maestà 与 006 MD5 同 + course-footer），失败 0；2 张 decoration（波蒂切利青年男子像 + 佩鲁吉诺基督受难）
- 备注：
  - 新流派：[[翁布里亚画派]]——拉斐尔师承画派
  - 8 新作品：[[基督下十字架 (拉斐尔)]]、[[圣母的婚礼 (拉斐尔)]]、[[康乃馨圣母]] (达·芬奇)、[[粉红圣母]] (拉斐尔)、[[教皇尤利乌斯二世像]]、[[西斯廷圣母]]、[[披纱女子]]、[[圣家族 (拉斐尔)]]
  - 跨课图像处理：雅典学院 +2 (拉斐尔自画像局部 + 另一整体图)；圣母的婚礼 (佩鲁吉诺) +1 (不同 CDN 版本)；杜乔 Maestà 复用
  - 路人式：教皇尤利乌斯二世（在 artwork 内详描）、教皇利奥十世、教皇西斯图四世、伏尔泰、徐志摩、阿拉斯
  - 波蒂切利青年男子像 + 佩鲁吉诺基督受难 作 decoration 处理
  - 多个待 ingest 的画家 (米开朗基罗 / 达·芬奇 / 波蒂切利 / 美第奇家族 / 巴克森德尔) 都通过本课追加 source；本日志未一一列出各 +1 编辑

## [2026-05-13] ingest | 010｜达芬奇：他为什么一生抑郁不得志？

- 新建：来源(1) 人物(2) 技法(2) 作品(7)
- 更新：作品/最后的晚餐 (sources +1, 图片清单备注 010 复用, 出现在+1)、作品/圣母领报 (波蒂切利) (sources +1, 出现在+1)、人物/波蒂切利 (sources +1, 出现在+1)、人物/美第奇家族 (sources +1, 出现在+1)、时代/文艺复兴期 (sources +1, 出现在+1)、index.md、课程页 (sources 10→11)
- 图片：下载 9（7 作品首图 + 1 天使对比 decoration + 1 footer check），复用 3（圣母领报波蒂切利 + 最后的晚餐 + course-footer），失败 0
- 备注：
  - 新人物：[[达·芬奇]] (主角)、[[维罗奇奥]] (师傅)
  - 新技法：[[晕涂法 Sfumato]] + [[空气透视法 Atmospheric Perspective]]——达·芬奇核心创新
  - 新作品：[[三博士来朝 (波蒂切利)]] (美第奇全家福)、[[基督受洗 (维罗奇奥)]] (徒胜于师)、[[吉内薇拉·斑琪]]、[[女子头像 (达·芬奇)]] (素描)、[[蒙娜丽莎]]、[[年轻女子肖像 (波蒂切利)]]、[[抱貂女子]]
  - 路人式：吉兰达约、教皇西斯图四世、弗朗索瓦一世、阿尔贝蒂、阿拉斯
  - 跨课图片复用：圣母领报 (波蒂切利) 与 009 同 MD5、最后的晚餐 与 001 同 MD5、footer 与 course-footer 同
  - 维罗奇奥/达芬奇天使局部对比图按 decoration 处理

## [2026-05-13] ingest | 009｜波蒂切利：如何解读"理念美"？

- 新建：来源(1) 人物(2) 作品(7)
- 更新：作品/圣母领报 (马丁尼·梅米) (sources +1, 图片清单+03, 出现在+1)、人物/美第奇家族 (sources +1)、概念/理念美 (出现在+1)、index.md、课程页 (sources 9→10)
- 图片：下载 13（7 主作品图 + 4 春局部 + 1 simonetta decoration + 1 footer check），复用 1（course-footer.jpg），失败 0
- 备注：
  - 新人物：[[波蒂切利]] (主角)、[[利比修士]] (师傅)
  - 7 件新作品：[[圣母子与二天使 (利比修士)]]、[[持石榴的圣母]]、[[春 La Primavera]] (folder 含 1 主图 + 4 局部)、[[圣母领报 (波蒂切利)]]、[[维纳斯与马尔斯]]、[[维纳斯的诞生]]、[[维纳斯 (波蒂切利)]] (1:8 + 脱臼变形例)
  - 路人式：卢克莱修、波利齐亚诺、皮科、皮耶罗·迪·科西莫 (Simonetta 肖像作者 — 暂作为 decoration 处理)、西蒙内塔·维斯普奇 (模特, in 维纳斯的诞生 / 春 内嵌)、朱利亚诺·美第奇
  - 圣母领报 (马丁尼·梅米) 跨课图：009 引用的与 003/006 是不同 CDN 版本 (MD5 异)，作 03.jpg 入 folder
  - 末尾 footer 与 course-footer.jpg MD5 相同，复用

## [2026-05-13] ingest | 008｜文艺复兴到底复兴了什么？

- 新建：来源(1) 人物(4) 概念(3) 作品(5)
- 更新：作品/雅典学院 (sources 1→2, 图片清单+02/+03, 深度细节追加, 出现在+1)、人物/拉斐尔 (sources +1)、人物/巴克森德尔 (sources +1)、人物/瓦萨里 (sources +1)、时代/文艺复兴期 (sources +1)、index.md、课程页 (sources 8→9)
- 图片：下载 9（5 作品首图 + 1 雅典学院 02 局部 + 1 雅典学院 03 整体 + 1 圣特蕾莎 02 局部 + 1 西斯廷耶利米 decoration），复用 1（course-footer.jpg），失败 0
- 备注：
  - 新人物：[[费奇诺]] (新柏拉图主义整合者)、[[米开朗基罗]] (lecture 012 stub)、[[提香]] (lecture 016 stub)、[[贝尔尼尼]] (lecture 022+ stub)
  - 新概念：[[新柏拉图主义]]、[[理念美]]、[[仰望星空母题 (出神)]] folder-mode
  - 新作品：[[圣塞巴斯蒂安 (拉斐尔)]]、[[圣塞西莉亚]]、[[圣凯瑟琳 (拉斐尔)]]、[[忏悔的抹大拉 (提香)]]、[[圣特蕾莎的狂喜]]
  - [[雅典学院]] 跨课图片处理：008 提供局部 + 不同 CDN 的整体图，分别作 02 / 03 入 folder
  - 路人式：托马斯·阿奎那、普罗提诺、柏拉图、亚里士多德、第欧根尼、赫拉克利特、丢勒 (lecture 020 stub)、鲁迅、王尔德、达尼埃尔·阿拉斯
  - 米开朗基罗 + 提香 + 贝尔尼尼 三个 stub 提前建以解决 wikilink，待各自 lecture 补完
  - 米开朗基罗西斯廷天顶画《先知耶利米》局部按 decoration 处理 (整体作品待 lecture 012)
  - 末尾 footer 与 course-footer.jpg MD5 相同，复用

## [2026-05-13] ingest | 007｜文艺复兴是怎么发生的？

- 新建：来源(1) 时代(1) 人物(4) 技法(1) 作品(2)
- 更新：流派/佛罗伦萨画派 (+007)、index.md、课程页 (sources 7→8, 章节结构, lecture list)
- 图片：下载 4（2 作品首图 + 1 透视图 decoration + 1 footer check），复用 1（course-footer.jpg），失败 0
- 备注：
  - 新时代：[[文艺复兴期 Renaissance]]——本课程正式进入文艺复兴
  - 新人物：[[美第奇家族]] (lecture 014 主篇，本课 stub)、[[布鲁内莱斯基]]、[[拉斐尔]] (lecture 011 主篇，本课 stub)、[[佩鲁吉诺]]
  - 新技法：[[线性透视]]——文艺复兴的关键技术装置
  - 新作品：[[雅典学院]]、[[圣母的婚礼 (佩鲁吉诺)]]
  - 路人式：教皇若干、腓力四世、亨利四世、彼得拉克 / 但丁 / 薄伽丘、利比修士、约翰八世、西吉斯蒙德皇帝
  - 拉斐尔 与 美第奇家族 创建时为 stub 状态，注明 lecture 011 / 014 将补完
  - 末尾 footer 与 course-footer.jpg MD5 相同，复用

## [2026-05-13] ingest | 006｜哥特艺术2：为什么在意大利发生了分化？

- 新建：来源(1) 流派(2) 人物(3) 作品(4)
- 更新：人物/马丁尼 (+006)、人物/丹纳 (+006)、流派/哥特艺术 (+006, 代表人物补充意大利四家)、作品/圣母领报 (图片清单+02, 出现在+1, sources 1→2)、index.md、课程页 (sources 6→7)
- 图片：下载 6（4 作品首图 + 2 maps decoration），复用 2（圣母领报 01 与 003 MD5 相同 → 不重新下载；course-footer.jpg），失败 0；圣母领报 新加 02 (局部) png
- 备注：
  - 新流派：[[佛罗伦萨画派]] / [[锡耶纳画派]] —— 意大利哥特绘画两大对立路径
  - 新人物：[[契马布埃]] / [[乔托]] / [[杜乔]] —— 哥特意大利三宗师 (西方绘画之父 + 锡耶纳奠基者 + 佛罗伦萨初代)
  - 利波·梅米仍未独立建页，收录于 [[马丁尼 Simone Martini]] 人物页
  - 路人式：但丁、彼得拉克、薄伽丘、腓特烈二世、查理曼、叙热院长、波西纳
  - 四件新作品：契马布埃《Santa Trinita Maestà》、乔托《Ognissanti Madonna》《Lamentation》、杜乔《Maestà》
  - 圣母领报 (马丁尼·梅米) 跨课复用：003 主图与 006 主图 MD5 相同 → 不重复落盘；006 新加织金锦局部 02.png
  - 欧洲版图与意大利小国林立的两张地图均按 decoration 处理
  - 末尾 footer 与 course-footer.jpg MD5 相同，复用

## [2026-05-13] ingest | 005｜哥特艺术1：为什么说它是文艺复兴的前奏？

- 新建：来源(1) 流派(2) 人物(1) 技法(1) 作品(7)
- 更新：作品/弗拉基米尔的圣母 (sources 1→2, 图片清单+02, 出现在+1)、流派/拜占庭艺术 (sources +1, 出现在+1)、人物/瓦萨里 (sources +1, 出现在+1)、时代/中世纪 (sources +1, 主要流派 +罗马式+哥特, 出现在+1)、index.md、课程页 (sources 5→6, lecture list +1, 章节结构)
- 图片：下载 12（7 作品首图 + 1 沙特尔 02 彩窗 + 4 decoration），复用 1（course-footer.jpg），失败 0；其中 弗拉基米尔的圣母 跨课图片 → 02.jpg
- 备注：
  - 新流派：[[哥特艺术]] 主角 + [[罗马式]] 简短前身（mentioned in passing, 留待罗马式专题如有需要时扩展）
  - 新人物：[[克洛斯·斯吕特尔]]（哥特复古回归古罗马的标杆雕塑家）
  - 新技法：[[彩色玻璃花窗]]，与已有 [[马赛克]] 形成"看似相似底层不同"对照
  - 7 件新作品：巴黎圣母院 / 沙特尔大教堂 (multi-image: 立柱+彩窗) / 善良的牧羊人 (拉文纳) / 第戎的摩西井 / 圣母雕像 (珍妮·德·埃弗勒) / 基督下十字架 (沃拉泰拉) / 基督为使徒洗足 (奥托三世福音书)
  - 路人式：查理曼大帝、教皇利奥三世 (与 004 拜占庭利奥三世皇帝重名异人)、亨利四世、珍妮·德·埃弗勒、弗洛伊德、丹皮尔、康德、牛顿、布鲁诺
  - 杜乔 / 乔托：本课预告 lecture 006 的两个分化方向，未建 stub
  - 蒙雷阿莱壁画、加洛林圣马太、塔胡尔壁画、巴黎圣母院解剖图：均按 decoration 处理，未独立建 artwork
  - 弗拉基米尔的圣母 005 配图 MD5 与 004 配图不同 → 同作品的不同 CDN 版本 / 不同裁剪；按"同一 artwork 文件夹追加 02.jpg"规则处理

## [2026-05-13] ingest | 004｜拜占庭艺术：程式化的艺术是怎么回事？

- 新建：来源(1) 时代(1) 流派(1) 人物(1) 技法(1) 作品(5) 概念(1)
- 更新：流派/古埃及艺术（+004）、流派/古罗马艺术（+004）、index.md（时代 +1、流派 +1、人物 +1、技法 +1、作品 +5、概念 +1、来源 +1）、课程页（章节结构、lecture list、sources 4→5）
- 图片：下载 7（5 作品首图 + 1 decoration 西奈修道院 + 1 footer 检测但复用），复用 1（course-footer.jpg MD5 命中），失败 0
- 备注：
  - 新时代：[[中世纪 Middle Ages]]——本课程正式跨进 medieval period
  - 新流派：[[拜占庭艺术 Byzantine Art]]——中世纪艺术的母体
  - 新人物：[[贡布里希 E.H. Gombrich]]——其名言"艺术史是思想观念变化的历史"被顾衡用作论证根基
  - 新技法：[[马赛克 Mosaic]]——把 003 已援引但未独立建页的核心媒介补上；与 [[正身侧面律]] 形成 "罗马-拜占庭" 与 "古埃及-中东" 的两条远祖线
  - 新概念：[[圣像 Icon]]——拜占庭绕开《十诫》禁偶像的神学+艺术装置
  - 5 件新作品全部 folder-per-artwork：五饼二鱼 / 基督受洗 (阿利亚诺) / 弯曲宝座上的圣母子 / 查士丁尼及其随从 / 弗拉基米尔的圣母
  - 历史人物未建 stub：耶稣、彼拉多、圣保罗、君士坦丁、利奥三世、查士丁尼、圣凯瑟琳、马克西米安努斯——均为宗教 / 政治 / 圣徒身份，非艺术家；其中查士丁尼与马克西米安努斯在 artwork [[查士丁尼及其随从]] 页内深度刻画
  - 西奈圣凯瑟琳修道院 (548-565) 作为"基督徒不得不创造圣像"的历史插曲提及，按 decoration 处理而非 artwork
  - 末尾 footer 与 course-footer.jpg MD5 相同，复用
  - 弯曲宝座圣母子的现存地暂用 (*not from wiki*) 标注待用户确认（图像辨识接近 NGA 收藏的一件 13 世纪拜占庭作品，但无确凿匹配）

## [2026-05-13] ingest | 003｜画得像和画得好是一回事吗？

- 新建：来源(1) 流派(1) 人物(5) 技法(2) 作品(3) 概念(1)
- 更新：流派/古埃及艺术（出现在+1, sources 1→2, 新增 [[正身侧面律]] 链接）、流派/古希腊古典时期（出现在+1, sources 1→2, 新增画家 [[宙克西斯]][[帕拉西奥斯]]）、时代/古典时代（出现在+1, sources 1→2, 加入 [[古罗马艺术]]）、index.md、课程/顾衡·西方美术100讲.md（sources 3→4）
- 图片：下载 8（3 作品首图 + 1 概念样本 + 4 decoration），复用 1（末尾 course-footer.jpg），失败 0
- 备注：
  - 新流派：[[古罗马艺术 Ancient Roman Art]]——课程第三个文明流派，与 [[古希腊古典时期]] / [[古埃及艺术]] 并列
  - 新人物：[[瓦萨里]] / [[李格尔]] 为本课史观争论对，对偶进入；[[宙克西斯]] / [[帕拉西奥斯]] 为古希腊绘画两大失传画家；[[马丁尼]] 引入哥特/锡耶纳画派的预告
  - 新技法：[[正身侧面律]] / [[短缩法]] —— 形成"埃及程式 vs. 希腊写实"的形式策略对偶
  - 新概念：[[法尤姆肖像]] folder-mode，承接 002 [[库罗斯]] 的"类型样本配图"模式
  - 路人式引述：苏格拉底、色诺芬、老普林尼、董仲舒、董源——按既定规则跳过 stub
  - 中国文人画作为对照系仅在源页提及，未建流派页（与 002 [[古埃及艺术]] 的对照建页处理不同——文人画跨度过大、单篇支撑不足）
  - 利波·梅米 (Lippo Memmi) 作为 [[圣母领报]] 共作者收入 [[马丁尼 Simone Martini]] 页内，未单独建页
  - 米开朗基罗 (lecture 012) 本篇仅作为瓦萨里史观的标尺被提及，未建 stub
  - 文献中提及的古希腊绘画作品 (帕拉西奥斯、宙克西斯作品) 全部失传——无法建 artwork 页
  - 庞贝壁画、古希腊陶罐 (BC 500) 为通指 / 类型例，作 decoration 处理而非 artwork
  - 末尾 footer 与 course-footer.jpg MD5 完全相同，直接复用

## [2026-05-13] ingest | 001｜总导论：艺术到底属于谁？

- 新建：来源(1) 人物(3) 技法(1) 作品(5) 概念(2)
- 更新：人物/巴克森德尔（出现在+1, sources 1→2）、概念/时代之眼（出现在+1, sources 1→2）、index.md、课程/顾衡·西方美术100讲.md（sources 2→3）
- 图片：下载 6（5 作品首图 + 1 小孔成像示意图），复用 1（末尾 footer 与 course-footer.jpg MD5 相同），失败 0
- 备注：
  - 新人物：[[潘诺夫斯基 Erwin Panofsky]]、[[沃尔夫林 Heinrich Wölfflin]]、[[丹纳 Hippolyte Taine]]——四方法各家代表，与已有 [[巴克森德尔 Michael Baxandall]] 拼合成"艺术史四方法谱系"
  - 新概念：[[艺术史四种方法 Four Approaches to Art History]]（本课元框架）、[[图像志 Iconography]]（潘氏方法的具名版本）
  - 新技法：[[小孔成像法 Camera Obscura]]——课程"关注质料与技术"路径的首个案例
  - 5 件新作品全部按 folder-per-artwork 建：藤椅上的静物 / 戴金盔的男子 / 阿德里阿蒂克的日落 / 最后的晚餐 / 阿尔诺菲尼夫妻像
  - 路人式引述：劳什伯格、波德莱尔、多热莱斯——按 002 规则跳过 stub
  - 将于专题处理的画家本篇仅举例提及，未建 stub：毕加索 (064-067)、伦勃朗 (025-026)、德拉克罗瓦 (034)、莫奈 (041-042)、达·芬奇 (010)、凡·艾克 (019)、雷诺阿 (043)——产生约 7 条暂未解析的 wikilink，后续 ingest 自然收口，lint 可巡检
  - 小孔成像图按 decoration 落地 `_meta/lecture-decorations/001-camera-obscura.jpg`，未走 folder-per-technique（暂不扩展 schema）
  - 末尾 footer 与现有 course-footer.jpg MD5 完全相同，直接复用，未新增文件
  - 三位艺术史家 IPA 全部留空（不确定）

## [2026-05-13] ingest | 发刊词｜我们都有搞懂艺术的权利

- 新建：来源(1) 人物(1) 概念(2)
- 更新：index.md（人物 +1、概念 +2、来源 +1）、课程/顾衡·西方美术100讲.md（lecture list +1, sources 1→2）、来源/002…md（footer 图片改用共享文件名 course-footer.jpg）
- 图片：下载 5，复用 0（其中 2 张 MD5 重复，合并为 2 个引用 → 实际落盘 3 张新文件）、失败 0
- 备注：
  - 批次模式：用户授权 `/art-scan` 全量按序自动 ingest，跳过 Step 4 Checkpoint（feedback memory 已记录）
  - 人物 [[巴克森德尔 Michael Baxandall]] 建页（方法论奠基者）；普雷齐奥西、朵拉·玛尔、爱德华·扬格、巴斯基亚按 002 路人式规则跳过 stub
  - 毕加索、塞尚仅作举例提及，未建 stub（专题分别在 064–067、052–054）
  - 毕加索《哭泣的女人》Weeping Woman 在涉及实体清单点名，未建专页（留待 064–067 处理）
  - 5 张 CDN 图片均无 caption → 全部按 decoration 处理，落地 `_meta/lecture-decorations/`
  - 图像合并 1：`发刊词-01.png` ≡ `发刊词-03.png`（CDN 不同 URL、MD5 相同），原文中第 1、3 张图引用同一文件
  - 图像合并 2：`发刊词-05.jpg` ≡ 原 `002.jpg`（课程通用 footer），统一改名为 `course-footer.jpg`，同步更新 002 来源页引用
  - 新概念 [[时代之眼 Period Eye]] 与 [[三阶段框架 (古典·现代·当代) Three-Stage Periodization]] 是全课程的方法论与组织主线，后续每讲都会反复引用
  - 巴克森德尔 IPA 不确定 → `pronunciation:` 留空

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

## [2026-05-13] ingest | 016｜提香：为什么业界评价比达芬奇还高？

- 新建：来源(1) 技法(1) 人物(2) 作品(12) 概念(0)
- 更新：[[提香 Titian]] (大幅扩写，stub → 集大成专题), [[达·芬奇 Leonardo da Vinci]] (1911 翻红段), [[拉斐尔 Raphael]] (加 Castiglione), [[乔尔乔内 Giorgione]] (师弟提香), [[乔万尼·贝利尼 Giovanni Bellini]] (诸神的盛宴), [[威尼斯画派 Venetian School]] (厚涂 + 风景), [[文艺复兴期 Renaissance]] (016), [[圣塞西莉亚 St Cecilia]] 02.jpg, [[忏悔的抹大拉 (提香) Penitent Magdalene]] 02.jpg, [[沉睡的维纳斯 Sleeping Venus]] 02.jpg, 课程页, index.md
- 图片：下载 15，复用 1（course-footer），失败 0
- 备注：
  - 同名作品在两位画家手中 → 显式 disambig：[[维纳斯与阿都尼斯 (提香) Venus and Adonis (Titian)]] vs [[维纳斯与阿都尼斯 (鲁本斯) Venus and Adonis (Rubens)]]
  - 新建技法 [[厚涂 Impasto]] 是本课最核心创新——提香首创、伦勃朗/印象派/表现主义系出
  - 鲁本斯、杜尚 stub 化（detailed 在 024 / 088–090）
  - 阿雷蒂诺 (Pietro Aretino) 作为"艺术经纪人祖师爷"在 [[提香 Titian]] 个性段落记录，未单独建页
  - 杜尚 *L.H.O.O.Q.* 同时计入 1919 达·芬奇翻红事件（参 [[达·芬奇 Leonardo da Vinci]] 身后名声节）

## [2026-05-13] ingest | 017｜科雷乔：为什么他是文艺复兴最具现代性的画家？

- 新建：来源(1) 人物(3) 作品(10)
- 更新：[[蒙娜丽莎 Mona Lisa]] +02/03, [[春 La Primavera]] +06, [[维纳斯与马尔斯 Venus and Mars]] +02, [[最后的晚餐 The Last Supper]] +02, [[西斯廷天顶画 Sistine Chapel Ceiling]] +05, [[圣母领报 (波蒂切利) Annunciation (Botticelli)]] +02, [[吉内薇拉·斑琪 Ginevra de' Benci]] +02, 课程页, index.md
- 图片：下载 18，复用 1（course-footer），失败 0
- 备注：
  - 同名作品 disambig：[[丽达与天鹅 (达·芬奇) Leda and the Swan (Leonardo)]] vs [[丽达与天鹅 (科雷乔) Leda and the Swan (Correggio)]]
  - 鲁本斯 stub（参 024 详谈）、布歇 stub（参 028-029 详谈）、乌切洛 stub
  - [[科雷乔 Correggio]] 三大创新：主体视角空间观 / 让人物自身发光 / 云彩作为绘画材料 → 100 年后巴洛克的精神之父
  - 阿恩海姆（艺术心理学家"目光像机枪")、康德（先验空间观）作为概念引用，未单独建页
  - 实体页 出现在 同步（达·芬奇/米开朗基罗/拉斐尔/波蒂切利/佩鲁吉诺/翁布里亚画派/文艺复兴期 7 页）暂未在本次更新，待 lint 时补——主因是来源页本身已含 wikilink，backlink 在 Obsidian 解析中自然形成；显式更新留给 lint 通批

## [2026-05-13] ingest | 018｜矫饰主义：过度追求形式有什么后果？

- 新建：来源(1) 流派(1) 人物(6) 作品(5) 概念(0)
- 更新：人物/米开朗基罗 (主要), 人物/拉斐尔, 人物/瓦萨里, 人物/科雷乔, 人物/乔尔乔内, 人物/提香, 作品/粉红圣母 +02, 作品/西斯廷天顶画 +03, 作品/圣母怜子 (米开朗基罗) +03, 作品/雅典学院 +07, 作品/末日审判 +02, 流派/威尼斯画派, 时代/文艺复兴期, 课程页, index.md
- 图片：下载 14 (9 新作品 + 5 既有 pending), 复用 1 (course-footer), 失败 0
- 备注：
  - 矫饰主义页整合 maniera 词源 / 瓦萨里-兰齐旧叙事 / 1989 西斯廷清洗事件 / [[达尼埃尔·阿拉斯 Daniel Arasse]] 新解四段史
  - 新人物 stub：[[帕米贾尼诺 Parmigianino]] [[布龙吉诺 Agnolo Bronzino]] [[蓬托尔莫 Jacopo da Pontormo]] [[兰齐 Luigi Lanzi]] [[达尼埃尔·阿拉斯 Daniel Arasse]] [[雷诺兹 Joshua Reynolds]]
  - 由并行 batch agent 处理（与 019/020/021 同步），shared-state 在 main agent merge

## [2026-05-13] ingest | 019｜凡·艾克：什么是绘画的另一种可能性？

- 新建：来源(1) 流派(2) 人物(2) 作品(4) 概念(0)
- 更新：人物/凡·艾克 (深度专题), 作品/阿尔诺菲尼夫妻像 +02–10 (9 张细节图), 概念/图像志, 人物/潘诺夫斯基, 人物/丹纳, 技法/小孔成像法, 人物/瓦萨里, 课程页, index.md
- 图片：下载 14 (4 新作品 5 张 + 阿尔诺菲尼 8 张 pending + 1 dropped 圣塞巴斯蒂安 dupe) + 1 补缺 (line-223), 复用 1 (course-footer), 失败 0
- 备注：
  - 新流派：[[佛兰德斯画派 Flemish School]] [[北方文艺复兴 Northern Renaissance]]
  - 新人物：[[马萨乔 Masaccio]] [[大卫·霍克尼 David Hockney]]
  - 新作品：[[圣三位一体 (马萨乔) The Holy Trinity]] [[戴红头巾的男子 Man in a Red Turban]] [[卡农的圣母 The Madonna with Canon van der Paele]] [[根特祭坛画 The Ghent Altarpiece]]
  - ⚠️ 一致性提示：019 顾衡说凡·艾克是油彩"发明者"；015 表述是"关键创新者（非发明者）"——两种措辞均保留

## [2026-05-13] ingest | 020｜丢勒：为什么版画那么重要？

- 新建：来源(1) 人物(5) 技法(3) 作品(15) 概念(1)
- 更新：人物/凡·艾克, 人物/乔万尼·贝利尼, 人物/拉斐尔, 人物/宙克西斯, 技法/线性透视, 概念/新柏拉图主义, 概念/理念美, 流派/威尼斯画派, 流派/北方文艺复兴, 时代/文艺复兴期, 课程页, index.md, 作品/蒙娜丽莎 +03, 作品/教皇尤利乌斯二世像 +02
- 图片：下载 17, 复用 1 (course-footer), 失败 0
- 备注：
  - 新人物：[[丢勒 Albrecht Dürer]] [[曼特尼亚 Andrea Mantegna]] [[舍恩高尔 Martin Schongauer]] [[拉伊蒙迪 Marcantonio Raimondi]] [[马奈 Édouard Manet]]
  - 新技法：[[版画 Printmaking]] [[木刻版画 Woodcut]] [[铜版画 Engraving]] —— 本课主线
  - 新概念：[[纽伦堡 Nuremberg]]（造纸厂 + 古登堡印刷工人涌入）
  - 流派/北方文艺复兴 先由 019 agent 创建；本 agent 检测并复用，未覆写
  - 拉伊蒙迪 caption 中 raw 写"莱蒙蒂"，已统一为通行的 Raimondi（拉伊蒙迪）+ aliases 收"莱蒙蒂"

## [2026-05-13] ingest | 021｜荷尔拜因：为什么要画那么多肖像画？

- 新建：来源(1) 人物(6) 作品(10) 概念(2)
- 更新：流派/佛兰德斯画派, 流派/北方文艺复兴, 流派/矫饰主义, 人物/拉斐尔, 人物/丢勒, 作品/教皇利奥十世与二主教像 +02, 作品/圣塞西莉亚 +03, 概念/新柏拉图主义, 课程页, index.md
- 图片：下载 15, 复用 1 (course-footer), 失败 0
- 备注：
  - 新人物：[[荷尔拜因 Hans Holbein the Younger]] + 5 个支撑（[[伊拉斯谟 Erasmus of Rotterdam]] [[托马斯·莫尔 Sir Thomas More]] [[亨利八世 Henry VIII of England]] [[克伦威尔 Thomas Cromwell]] [[马丁·路德 Martin Luther]]）
  - 新概念：[[宗教改革 Reformation]] [[神圣罗马帝国 Holy Roman Empire]]
  - 4 件由并行 agent 创建的实体（[[佛兰德斯画派]] [[北方文艺复兴]] [[矫饰主义]] [[丢勒]]）：本 agent 仅引用、未修改

## [2026-05-13] ingest | 022｜巴洛克：华丽等于没内涵吗？

- 新建：来源(1) 时代(1) 流派(2) 人物(2) 作品(7) 概念(0)
- 更新：作品/蒙娜丽莎 +04, 作品/基督下十字架 (拉斐尔) +02, 作品/戴手套的男子 (提香) +02, 作品/吉内薇拉·斑琪 +03, 作品/维纳斯与阿都尼斯 (提香) +02, 作品/维纳斯与阿都尼斯 (鲁本斯) +02, 作品/雅典学院 +08, index.md, log.md, .ingested.tsv, 课程页
- 实体页 出现在 更新待 lint：沃尔夫林（五对参数）、李格尔（触觉/视觉艺术）、瓦萨里、鲁本斯、卡拉瓦乔、提香、达·芬奇、波蒂切利、拉斐尔、文艺复兴期、矫饰主义、佛罗伦萨画派、威尼斯画派
- 图片：下载 9（新作品 + 圣母之死 02 + 圣母升天鲁 02），复用 1（course-footer），失败 0
- 备注：
  - 新时代 [[巴洛克时期 Baroque Period]] + 新流派 [[巴洛克 Baroque]] [[学院派 Academic Art]]
  - 新人物 [[卡拉齐 Annibale Carracci]] [[夏皮罗 Meyer Schapiro]]
  - 7 件新作品: 基督下十字架(鲁本斯), 青年男子像(波蒂切利), 圣母之死(卡拉瓦乔), 基督之死(卡拉齐), 奥迪祭坛画(拉斐尔), 圣母升天(鲁本斯), 圣母升天(提香)
  - ⚠️ 023 agent 并行也建了无 disambig 的 圣母之死 文件夹，已合并到 (卡拉瓦乔) 版（删除 dup + 修正 023/024 source 引用）；同 URL 不同字节的 02.jpg 也合并为 01.jpg

## [2026-05-13] ingest | 023｜卡拉瓦乔：巴洛克的戏剧性从何而来？

- 新建：来源(1) 流派(1) 人物(7) 技法(1) 作品(14) 概念(1)
- 更新：作品/圣塞西莉亚 +04, index.md, log.md, .ingested.tsv, 课程页
- 图片：下载 15（14 新作品 + 1 pending），复用 0，失败 0
- 备注：
  - 主角 [[卡拉瓦乔 Caravaggio]]（顾衡 1573 vs 通行 1571，已 frontmatter 标注）+ 6 支撑人物（卢伊尼/彼得扎诺/切萨里/德尔蒙特/圭多·雷尼/真蒂莱斯基）
  - 新流派 [[米兰画派 Milanese School]]；新技法 [[酒窖光 Tenebrism]]；新概念 [[特伦特大公会议 Council of Trent]]
  - ⚠️ 同名歧义处理：[[康乃馨圣母 (卢伊尼) Madonna of the Carnation (Luini)]] vs 既存 [[康乃馨圣母 Madonna of the Carnation]] (达·芬奇)；[[犹滴斩首荷罗芬尼 (卡拉瓦乔) ...]] vs (真蒂莱斯基) vs 既存 [[犹滴 (乔尔乔内) Judith]]
  - ⚠️ 圣母之死与 022 重名冲突已 merge（详 022 log）

## [2026-05-13] ingest | 024｜鲁本斯：都是巴洛克，为什么风格如此不同？

- 新建：来源(1) 人物(4) 作品(11) 概念(4)
- 更新：人物/鲁本斯（016 stub → 完整专题）, 作品/基督下十字架 (鲁本斯) +02, 作品/维纳斯与阿都尼斯 (鲁本斯) +03, 作品/圣母之死 (卡拉瓦乔) +出现在, index.md, log.md, .ingested.tsv, 课程页
- 图片：下载 14（11 新作品 + 3 现有 append），复用 1（course-footer + 1 dedup 圣母之死）, 失败 0
- 备注：
  - 新人物 [[勃鲁盖尔 Brueghel]] [[凡·戴克 Anthony van Dyck]] [[委拉斯贵支 Diego Velázquez]] [[玛丽·美第奇 Marie de' Medici]]
  - 新概念 [[画室流水线分工 Workshop Production]] [[圣像毁坏运动 Iconoclasm]] [[君权神授 Divine Right of Kings]] [[美第奇组画 Marie de' Medici Cycle]]
  - 11 鲁本斯作品全数：基督上十字架/劫夺留西帕斯的女儿/圣彼得圣约翰治愈跛脚人/自画像 1623/圣家族/圣母子(卡拉瓦乔)/美惠三女神/玛丽组画 4 件/帕里斯的评判
  - ⚠️ 024 误建的 dup 文件夹"基督下十字架 The Descent from the Cross/" 已删 (022 已建 (鲁本斯) disambig 版)

## [2026-05-13] ingest | 025｜伦勃朗1：为什么他被称为荷兰最伟大的画家？

- 新建：来源(1) 流派(1) 人物(5) 作品(8) 概念(1)
- 更新：作品/圣马太蒙召 +02, 作品/基督下十字架 (拉斐尔) +03, 作品/戴金盔的男子 +02, index.md, log.md, .ingested.tsv, 课程页
- 图片：下载 12（9 新作品 + 3 pending），复用 1（course-footer），失败 0
- 备注：
  - 新流派 [[荷兰黄金时代 Dutch Golden Age]]；新概念 [[画面戏剧性 Theatricality]]
  - 主角 [[伦勃朗 Rembrandt]] + 4 支撑（拉斯曼师傅 + 乌德勒支卡拉瓦乔派 2 人 + 哈尔斯）
  - 8 件新作品（含《夜巡》《杜普医生的解剖课》《亚里士多德与荷马半身像》）
  - ⚠️ 圣马太蒙召 folder 当前无 disambig，但 025 又新建了 (布吕根) 版本——未来 lint 可考虑把 Caravaggio 版重命名为 (卡拉瓦乔)

## [2026-05-13] ingest | 026｜伦勃朗2：为什么荷兰收费最高的画家会破产？

- 新建：来源(1) 人物(3) 作品(10) 概念(2)
- 更新：人物/伦勃朗（016 stub→深度专题）, 流派/荷兰黄金时代, 作品/戴金盔的男子 +03, index.md, log.md, .ingested.tsv, 课程页
- 图片：下载 11（10 新作品 + 戴金盔的男子 clipping），复用 1（course-footer），失败 0
- 备注：
  - 新人物：[[莎斯基亚 Saskia van Uylenburgh]]（伦勃朗第一任妻子）+ [[吉尔金 Geertje Dircx]] +  [[亨德里克金 Hendrickje Stoffels]]（晚年伴侣）
  - 新作品 10 件：自画像 1630/1660 / 花神 / 妓院里的浪子 / 波兰骑士 / 吉尔金(伦勃朗) / 床上的女人 / 沐浴溪间的女人 / 拔士巴与大卫王的信 / 犹太新娘
  - 新概念 [[画廊与经纪人体系 Gallery and Dealer System]] [[伦勃朗光 Rembrandt Lighting]]
  - 1983 RRP 鉴定将《戴金盔》《波兰骑士》定为非伦勃朗本人作

## [2026-05-13] ingest | 027｜如何理解巴洛克艺术的全貌？

- 新建：来源(1) 人物(2) 作品(4) 概念(1)
- 更新：作品/圣特蕾莎的狂喜 +03, 流派/巴洛克, 贝尔尼尼, 委拉斯贵支, 贡布里希, index.md, log.md, .ingested.tsv, 课程页
- 图片：下载 5（4 新作品 + 普鲁同 02），复用 1（course-footer），失败 0
- 备注：
  - 巴洛克板块收束课。新概念 [[流量饥渴 (巴洛克本质) Spectacle Economy]] 是顾衡的本质命题
  - 新人物：[[尤勇 Yu Yong]]（中国艺术研究院；《宫娥》立储画新解）[[威尔·杜兰特 Will Durant]]
  - 新作品：[[圣彼得广场 St. Peter's Square]] [[大卫 (贝尔尼尼) David (Bernini)]]（与既有 [[大卫 (米开朗基罗) David]] disambig）[[普鲁同劫夺珀尔塞福涅 The Rape of Proserpina]] [[宫娥 Las Meninas]]

## [2026-05-13] ingest | 028｜什么是洛可可？

- 新建：来源(1) 流派(1) 人物(5) 作品(8) 概念(2)
- 更新：人物/布歇（升 sources，明确"洛可可双翼"），作品/玛丽王后在马赛港登陆 +02, 作品/狄安娜出浴 +02, 作品/丽达与天鹅 (科雷乔) +02, 作品/沉睡的维纳斯 +03, index.md, log.md, .ingested.tsv, 课程页
- 图片：下载 13（9 新作品 + 4 既有 clippings），复用 0（course-footer 仅引用未下载），失败 0
- 备注：
  - 新流派 [[洛可可 Rococo]]（本课主笔）
  - 新人物 5：[[华托 Antoine Watteau]] [[亚森特·里戈 Hyacinthe Rigaud]] [[路易十四 Louis XIV]] [[路易十五 Louis XV]] [[蓬巴杜夫人 Madame de Pompadour]]
  - 新作品 8：路易十四像 / 爱的盛宴 / 舟发西苔岛 / 爱的花园 / 蓬巴杜夫人的肖像 / 梳妆 (华托) / 梳妆 (布歇) / 朱庇特与卡利斯托
  - 新概念 [[雅宴画 fête galante]] [[中国风 Chinoiserie]]
  - ⚠️ 与 029 并行：洛可可页冲突 029 已规避，仅链接

## [2026-05-13] ingest | 029｜洛可可为什么那么香艳？

- 新建：来源(1) 人物(2) 作品(5) 概念(2)
- 更新：作品/美惠三女神 (鲁本斯) +02, 作品/沉睡的维纳斯 +04, 人物/布歇, 鲁本斯, 乔尔乔内, 流派/洛可可 (代表人物/作品/概念追加，待 wrapper merge), index.md, log.md, .ingested.tsv, 课程页
- 图片：下载 7（5 新作品 + 2 既有 clippings），复用 1（course-footer），失败 0
- 备注：
  - 新人物 [[弗拉戈纳尔 Jean-Honoré Fragonard]]（洛可可后期代表）[[狄德罗 Denis Diderot]]
  - 新作品 5：弗拉戈纳尔 4 件调情画（少女与小狗 / 门闩 / 偷吻 / 秋千）+ 布歇《黑发宫女》
  - 新概念 [[危险关系 Les Liaisons dangereuses]] [[七年战争 Seven Years' War]]
  - 与 028 沉睡的维纳斯 PENDING_03 冲突已解决（028 → 03，029 → 04）

## [2026-05-13] ingest | 030｜新古典主义：为什么绘画再次转向宏大叙事？

- 新建：来源(1) 流派(1) 人物(4) 作品(6) 概念(2)
- 更新：流派/学院派, 巴洛克, 洛可可, 路易十四/十五, 狄德罗, 布歇, 拉斐尔, 鲁本斯, 理念美, 七年战争, index.md, log.md, .ingested.tsv, 课程页
- 图片：下载 6（6 新作品），复用 1（course-footer），失败 0
- 备注：
  - 新流派 [[新古典主义 Neoclassicism]]——本课主笔
  - 新人物 4：[[大卫 Jacques-Louis David]] [[普桑 Nicolas Poussin]] [[路易十六 Louis XVI]] [[伏尔泰 Voltaire]]
  - 新作品 6：[[荷拉斯兄弟之誓 Oath of the Horatii]] / [[阿卡迪亚牧人 Et in Arcadia ego]] / [[网球场宣誓 Tennis Court Oath]] / [[马拉之死 The Death of Marat]] / [[拿破仑翻越阿尔卑斯山 Napoleon Crossing the Alps]] / [[拿破仑加冕 The Coronation of Napoleon]]
  - 新概念 [[罗马奖 Prix de Rome]] [[法兰西皇家绘画与雕塑学院 Académie royale de peinture et de sculpture]]
  - ⚠️ 顾衡 030 反通说：新古典主义不是法国大革命产物（《荷拉斯兄弟之誓》是路易十六订件，离大革命还有 5 年）
  - ⚠️ 大卫人品评价低（处死路易十六 / 篡改马拉纸条 / 转身阿谀拿破仑）

## [2026-05-13] ingest | 031｜学院派为什么迅速没落？

- 新建：来源(1) 人物(9) 作品(6) 概念(3*)
- 更新：作品/自画像 (大卫) +01 (合并 PENDING), index.md, log.md, .ingested.tsv, 课程页
- 图片：下载 7（6 新作品 + 1 PENDING），复用 1（course-footer），失败 0
- 备注：
  - 新人物 9：[[委罗内塞 Veronese]] [[莱弗尔 François Lemoyne]] [[杰拉德 François Gérard]] [[温特哈特 Franz Xaver Winterhalter]] [[路易十八 Louis XVIII]] [[查理十世 Charles X]] [[路易·菲利普 Louis Philippe I]] [[拿破仑三世 Napoleon III]] [[德拉克罗瓦 Eugène Delacroix]]（stub，详 034）
  - 新作品 6：[[利未家的晚餐 The Feast in the House of Levi]] [[路易十八像 Portrait of Louis XVIII of France]] [[查理十世像 Portrait of Charles X of France]] [[路易·菲利普像 King Louis Philippe]] [[拿破仑三世像 Portrait of Emperor Napoleon III]] [[自画像 (大卫) Self-portrait (David)]]
  - 新概念 *：[[巴黎沙龙 Paris Salon]] [[落选者沙龙 Salon des Refusés]]（[[罗马奖 Prix de Rome]] 与 030 同建——竞态后保留一份）
  - 论点：1815 拿破仑倒台后政权迭代 → 1863 拿破仑三世御旨设落选者沙龙 = 现代艺术开端的政治根源

## [2026-05-13] ingest | 032｜安格尔：为什么他是学院派最后一位大师？

- 新建：来源(1) 人物(6) 流派(1*) 概念(1) 作品(12)
- 更新：作品/雅典学院 +09, 作品/年轻女子肖像 (波蒂切利) +02, index.md, log.md, .ingested.tsv, 课程页
- 图片：下载 14（12 新作品 + 2 既有 clippings），复用 1（course-footer），失败 0
- 备注：
  - 新人物 6：[[安格尔 Jean-Auguste-Dominique Ingres]]（本课主角）[[帕格尼尼 Niccolò Paganini]] [[司汤达 Stendhal]] [[雨果 Victor Hugo]] [[温克尔曼 Johann Joachim Winckelmann]] [[拿破仑 Napoleon Bonaparte]]
  - 新流派 *：[[浪漫主义 Romanticism]]——与 033 并行冲突，已合并：032 brief 版 + 033 rich 版 → 单一 canonical 版（详 033 备注）
  - 新概念 [[政治与艺术防火墙 The Wall between Politics and Art]]
  - 新作品 12（全部安格尔）：帕格尼尼像 / 阿伽门农的使者 / 荷马的礼赞 / 大宫女 / 瓦平松的浴女 / 朱庇特与忒提斯 / 奥松维尔伯爵夫人像 / 穆瓦特西埃夫人像 (坐 + 立) / 路易十三的誓愿 / 罗杰拯救安吉莉卡 / 泉

## [2026-05-13] ingest | 033｜什么是浪漫主义绘画？

- 新建：来源(1) 人物(8) 作品(3) 概念(5)
- 更新：流派/浪漫主义 Romanticism（与 032 合并；删除 dup [[浪漫主义绘画 Romantic Painting]]；批量重写 15 个文件的 wikilinks），index.md, log.md, .ingested.tsv, 课程页
- 图片：下载 3（3 新作品），复用 1（course-footer），失败 0
- 备注：
  - 新人物 8：[[德拉克罗瓦 Eugène Delacroix]]（stub，详 034）[[斯塔尔夫人 Madame de Staël]] [[歌德弗卢瓦 Marie Eleonore Godefroid]] [[伊曼努尔·康德 Immanuel Kant]] [[尼采 Friedrich Nietzsche]] [[席勒 Friedrich Schiller]] [[波德莱尔 Charles Baudelaire]] [[以赛亚·伯林 Isaiah Berlin]]
  - 新作品 3：[[自由领导人民 Liberty Leading the People]] [[斯塔尔夫人像 Portrait of Madame de Stael]] [[美狄亚的愤怒 (德拉克罗瓦) Medea about to Kill Her Children]]
  - 新概念 5：[[反启蒙 Counter-Enlightenment]] [[启蒙运动 Enlightenment]] [[报纸与艺术批评 Press and Art Criticism]] [[不屈的意志 Will to Power]] [[情感强度 Intensity of Feeling]]
  - ⚠️ 流派页冲突解决：032 创建了简版 [[浪漫主义 Romanticism]]，033 创建了富版 [[浪漫主义绘画 Romantic Painting]]——以 canonical name `浪漫主义 Romanticism` 保留，richer 内容写入；dup 文件删除；15 个引用文件 wikilink 批量替换为 [[浪漫主义 Romanticism]]

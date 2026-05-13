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

## [2026-05-13] ingest | 034｜德拉克罗瓦：为什么他成了浪漫主义的旗手？

- 新建：来源(1) 人物(5) 作品(7)
- 更新：人物/德拉克罗瓦（033 stub → 完整传记升级，待 lint）, 作品/自由领导人民 +02, 作品/玛丽王后在马赛港登陆 +03, 作品/劫夺留西帕斯的女儿 +02, 作品/大宫女 +02, 概念/线条 vs 色彩之争 / 报纸与艺术批评（待 lint backlinks）, index.md, log.md, .ingested.tsv, 课程页
- 图片：下载 12（新作品 7 文件夹 8 张 + pending 4 张），复用 2（自由领导人民/01.jpg 同 033 URL + 萨尔丹纳帕拉之死 02 dedup → 01），失败 0
- 备注：
  - 本批次 `batch-034-037` 并行处理（用户授权 batch-unattended，跳过 Step 4）
  - 5 新人物：[[籍里柯 Théodore Géricault]] [[杰夫·沃尔 Jeff Wall]] [[谢弗勒尔 Michel Eugène Chevreul]] [[塔列朗 Charles-Maurice de Talleyrand-Périgord]] [[盖兰 Pierre-Narcisse Guérin]]
  - 7 新作品（folder-per-artwork）：萨尔丹纳帕拉之死 / 遭洗劫的房间（杰夫·沃尔 1978）/ 轻骑兵军官的冲锋 / 美杜莎之筏 / 疯女人 / 但丁和维吉尔共渡冥河 / 阿尔及利亚女人
  - 4 既有作品文件夹接入新角度图：自由领导人民→02 / 玛丽王后在马赛港登陆→03 / 劫夺留西帕斯的女儿→02 / 大宫女→02
  - ⚠️ 路径冲突修正：agent 写出的 `../作品/` + `%20` 路径已由 merger 全量改回 `作品/` + 空格
  - 路人式：维克多·雨果、乔治·桑（artwork 内描述）

## [2026-05-13] ingest | 035｜库尔贝：为什么现实主义的开创者争议那么大？

- 新建：来源(1) 流派(1) 人物(2) 概念(4) 作品(12)
- 更新（待 lint backlinks）：人物/波德莱尔, 马奈, 德拉克罗瓦, 拿破仑三世, 大卫, 安格尔, 鲁本斯, 流派/学院派, 浪漫主义, 新古典主义, 作品/美惠三女神 (鲁本斯)（dedup 01.jpg）, 概念/巴黎沙龙, 落选者沙龙, 启蒙运动, 时代之眼, index.md, log.md, .ingested.tsv, 课程页
- 图片：下载 13（其中《美惠三女神 (鲁本斯)》一张 MD5 命中既有 01.jpg → dedup），课程页脚复用 1，失败 0
- 备注：
  - 本批次 `batch-034-037` 并行处理
  - 新流派 [[现实主义 Realism]]——库尔贝开创，与 036 视角互补
  - 主角 [[居斯塔夫·库尔贝 Gustave Courbet]] + [[孔德 Auguste Comte]]（实证主义思想之父）
  - 4 新概念 [[实证主义 Positivism]] / [[现代性 Modernité]]（波德莱尔 1863 首发明）/ [[巴黎公社 Paris Commune]] / [[旺多姆柱 Vendôme Column]]
  - 12 库尔贝作品：在奥尔南的晚餐后 / 库尔贝自画像(黑狗) / 村子里的年轻女士向放牛女孩儿施舍 / 艺术家的画室 / 奥尔南的葬礼 / 筛麦女 / 碎石工 / 浴女 / 逗鹦鹉的女子 / 猎狐 / L夫人肖像 / 集会归来
  - ⚠️ 路径冲突修正：1 张 agent 写的 `../作品/...PENDING_01.jpg` 已 dedup 改写为 `作品/美惠三女神 (鲁本斯)/01.jpg`
  - 顾衡判语预告：'马奈现代性比库尔贝深刻'——下一步 038 马奈讲再谈

## [2026-05-13] ingest | 036｜米勒：什么是"伟大的现实主义"？

- 新建：来源(1) 人物(7) 作品(12) 概念(3)
- 更新（待 lint backlinks）：人物/勃鲁盖尔, 波德莱尔, 伏尔泰, 狄德罗, 路易·菲利普, 居斯塔夫·库尔贝 (035 新建), 德拉克罗瓦, 伦勃朗, 流派/现实主义 (035 新建), 威尼斯画派, 学院派, 技法/厚涂, 版画, index.md, log.md, .ingested.tsv, 课程页
- 图片：下载 12，外加 1 张 PENDING（浴女 / 与 035 同 URL 同 MD5 → merger dedup 到 01.jpg），课程页脚复用 1，失败 0
- 备注：
  - 本批次 `batch-034-037` 并行处理
  - 主角 [[米勒 Jean-François Millet]]（伟大的现实主义）+ [[杜米埃 Honoré Daumier]]（批判现实主义）
  - 4 支撑人物：[[路易·勒南 Louis Le Nain]] / [[格勒兹 Jean-Baptiste Greuze]] / [[卢梭 Jean-Jacques Rousseau]] / [[休谟 David Hume]] / [[罗丹 Auguste Rodin]]
  - 3 新概念：[[农民画传统 Peasant Painting Tradition]]（四阶段框架）/ [[高贵的野蛮人 Noble Savage]] / [[石版印刷术 Lithography]]
  - 12 作品：晚钟 / 拾穗者 / 牧羊女 / 播种者 / 去劳动 / 扶锄男子（米勒 6）+ 高康大 / 三等车厢（杜米埃 2）+ 农民的舞蹈 / 农民的婚礼（勃鲁盖尔 2）+ 农民的晚餐（路易·勒南 1）+ 乡村订婚（格勒兹 1）
  - ⚠️ 并行冲突已规避：[[现实主义 Realism]] / [[居斯塔夫·库尔贝 Gustave Courbet]] / 作品/浴女 The Bathers (Courbet)/01.jpg 由 035 创建，036 仅引用未覆写

## [2026-05-13] ingest | 037｜为什么说古典时代没有风景画？

- 新建：来源(1) 流派(1) 人物(9) 作品(11) 概念(3)
- 更新（待 lint backlinks）：作品/维纳斯与马尔斯 +03, 作品/基督下十字架 (拉斐尔) +04, 作品/圣安娜与圣母子 +02, 作品/荒漠中的圣方济各 +02, 作品/美惠三女神 (鲁本斯) (dedup 01.jpg); 人物/马萨乔 / 波蒂切利 / 拉斐尔 / 达·芬奇 / 乔万尼·贝利尼 / 提香 / 鲁本斯 / 米开朗基罗 / 普桑 / 马奈; 技法/线性透视 / 空气透视法 / 小孔成像法; 时代/中世纪 / 文艺复兴期 / 巴洛克时期; 流派/拜占庭艺术 / 佛罗伦萨画派 / 锡耶纳画派 / 威尼斯画派 / 佛兰德斯画派 / 荷兰黄金时代 / 学院派, index.md, log.md, .ingested.tsv, 课程页
- 图片：下载 16，复用课程页脚 1，失败 0；5 张 PENDING（维纳斯与马尔斯→03 / 基督下十字架(拉斐尔)→04 / 圣安娜与圣母子→02 / 荒漠中的圣方济各→02 / 美惠三女神(鲁本斯) MD5 dedup→01）
- 备注：
  - 本批次 `batch-034-037` 并行处理
  - 新流派 [[巴比松画派 Barbizon School]]——柯罗领衔，承接洛兰/普桑'披神话外衣画风景'路线但摘下外衣
  - 9 新人物：[[戈佐利 Benozzo Gozzoli]] [[乔瓦尼·迪·保罗 Giovanni di Paolo]] [[波拉约洛 Antonio del Pollaiuolo]] [[维米尔 Johannes Vermeer]] [[洛兰 Claude Lorrain]] [[柯罗 Camille Corot]] [[康斯泰布尔 John Constable]] [[翁贝托·艾柯 Umberto Eco]] [[肯尼斯·克拉克 Kenneth Clark]]
  - 3 新概念：[[风景画 Landscape Painting]]（完整谱系）/ [[为艺术而艺术 Art for Art's Sake]]（理解马奈的钥匙）/ [[象征时期风景 Symbolic Landscape]]（肯尼斯·克拉克分期）
  - 11 新作品（按时代序）：纳税银（马萨乔 1425）/ 三博士来朝 (戈佐利) / 施洗者约翰归隐荒野 / 圣塞巴斯蒂安殉难（波拉约洛）/ 神圣爱与世俗爱（提香 1514）/ 戴珍珠耳环的少女 / 代尔夫特一景（维米尔）/ 阿斯卡尼俄斯猎鹿（洛兰）/ 第欧根尼扔掉他的碗（普桑）/ 库布隆森林（柯罗）/ 埃塞克斯威文荷公园（康斯泰布尔）
  - ⚠️ 路径冲突修正：agent 写的 5 个 `../作品/...PENDING_NN.jpg` 已由 merger 全部改回 `作品/...NN.jpg`
  - ⚠️ 索引修正：agent 写的 `[[维米尔 Vermeer]]` 不匹配文件名 `维米尔 Johannes Vermeer.md`，merger 已改为 `[[维米尔 Johannes Vermeer]]`
  - 候选未建：'画家五等 / Hierarchy of Genres'（顾衡 037 引法国学院题材等级，多次出现，未来值得单建）
  - 本课作为 [[038]] 马奈讲的铺垫——逻辑链：风景画地位上升 → 对叙事性主题拒斥 → 为艺术而艺术 → 古典-现代分水岭

## [2026-05-13] merge | batch-034-037 后处理

- 4 个 lecture 并行 ingest（agents 034 / 035 / 036 / 037）→ main agent merge
- 跨 agent 冲突解决：
  - **图片去重**（MD5 命中既有文件）：035→《美惠三女神 (鲁本斯)》PENDING_01、036→《浴女 The Bathers (Courbet)》PENDING_01、037→《美惠三女神 (鲁本斯)》PENDING_03，三处均 dedup 到既有 01.jpg
  - **既有文件夹接入新角度图**（共 8 个 folder × 不同 NN）：034 自由领导人民/02 玛丽王后/03 劫夺留西帕斯/02 大宫女/02 ｜ 037 维纳斯与马尔斯/03 基督下十字架(拉斐尔)/04 圣安娜与圣母子/02 荒漠中的圣方济各/02
  - **共建实体**（035 创建、036 引用）：[[现实主义 Realism]] / [[居斯塔夫·库尔贝 Gustave Courbet]] / 作品/浴女 The Bathers (Courbet)/——036 未覆写
- 路径前缀冲突：3 个 agent（034/035/037）误用 `../作品/...PENDING_NN.<ext>` + 034 还误用 `%20` URL 编码，merger 全量重写为 wiki 约定 `作品/... NN.<ext>` + 字面空格
- 索引修正：037 agent 写的 `[[维米尔 Vermeer]]` 不匹配文件名 `维米尔 Johannes Vermeer.md`，merger 在 index.md 改为 `[[维米尔 Johannes Vermeer]]`
- Backlog（留 lint）：约 60 个既有人物/流派/技法/时代/作品页的 `## 出现在` 反向链接 + 各作品页的 `图片清单` 表格新行

## [2026-05-13] ingest | 038｜马奈1：为什么他是西方现代绘画的鼻祖？

- 新建：来源(1) 人物(4) 作品(8) 概念(3)
- 更新（待 lint backlinks）：人物/马奈（020 stub → 主体传记升级）, 人物/居斯塔夫·库尔贝, 概念/现代性 (035 基础上三层综合: 本雅明时间观 + 弗洛姆消费异化 + 帕特南社会资本), 人物/孔德, 波德莱尔, 概念/实证主义 / 启蒙运动 / 画廊与经纪人体系, 流派/浪漫主义 / 现实主义
- 图片：下载 8 新作品首图，复用 1 (course-footer)，0 失败；2 张 PENDING dedup 到既有 01.jpg（草地上的午餐 / 浴女 Courbet —— 同 MD5）
- 备注：
  - 本批次 `batch-038-041` 并行处理（refined prompt：vault-root-relative paths + 文件名-wikilink 匹配，agents 全部遵守）
  - 4 新人物：[[奥斯曼男爵 Baron Haussmann]] [[本雅明 Walter Benjamin]] [[弗洛姆 Erich Fromm]] [[帕特南 Robert Putnam]]
  - 8 新作品（马奈 7 + 库尔贝 1）：梅子白兰地 / 苦艾酒 / 拾荒者 / 在咖啡馆 / 奥林匹亚 / 娜娜 / 胜利女神游乐场 / 谷中泉水
  - 3 新概念：[[巴黎大改造 Haussmann's renovation of Paris]] / [[玻马舍 Bon Marché]] / [[妓女母题 (马奈) Prostitute Motif (Manet)]]
  - ⚠️ 跨 agent 协作：奥林匹亚 folder 由 038 创建，039 race-condition 检测后仅追加图（dedup 到 01.jpg）

## [2026-05-13] ingest | 039｜马奈2：画家如何应对照相机的冲击？

- 新建：来源(1) 人物(5) 作品(8) 概念(3)
- 更新（待 lint backlinks）：人物/马奈 (038/020 基础上'照相机危机 + 西班牙风 + 向二维平面回归'扩展), 委拉斯贵支, 哈尔斯, 拉伊蒙迪, 提香, 拉斐尔, 居斯塔夫·库尔贝, 德拉克罗瓦, 安格尔, 拿破仑三世, 波德莱尔; 作品/乌尔比诺的维纳斯 +02, 鲁特琴手 +02 (新角度)
- 图片：下载 13（8 新作品首图 + 5 PENDING），课程页脚复用 1，失败 0；5 PENDING 中 3 张 dedup 到既有 01.jpg（草地上的午餐 / 帕里斯的审判(拉伊蒙迪) / 奥林匹亚），2 张追加为 02.jpg（乌尔比诺的维纳斯 / 鲁特琴手）
- 备注：
  - 本批次 `batch-038-041` 并行处理
  - 5 新人物：[[库退尔 Thomas Couture]] [[卡巴内尔 Alexandre Cabanel]] [[马拉美 Stéphane Mallarmé]] [[西美尔 Georg Simmel]] [[维多琳 Victorine Meurent]]
  - 3 新概念：[[照相机的冲击 Photography's Impact]] / [[建立绘画的内在传承 Pictorial Self-Reference]] / [[向二维平面回归 Return to Flatness]]
  - 8 新作品：蓝沙发上的马奈夫人 / 颓废的罗马人（库退尔 1847 沙龙金奖）/ 穿斗牛士服的维多琳小姐 / 吹短笛的少年 / 对镜维纳斯 (委拉斯贵支) / 弹吉他的人 / 维纳斯的诞生 (卡巴内尔)（与波蒂切利版 disambig）/ 阳台
  - ⚠️ 跨 agent 协作：奥林匹亚 race-condition 处理得当——038 创建文件夹，039 检测后只追加图不覆写 .md

## [2026-05-13] ingest | 040｜什么是印象派?

- 新建：来源(1) 人物(5) 作品(2) 概念(2)
- 更新（待 lint backlinks 与流派合并）：流派/印象派（041 创建；040 内容待 merger 注入：5 行 学院派 vs 印象派 对照表 / 两大成因 (实证主义 + 银版照相法) / 谢弗勒尔+贝克勒尔+约翰·兰德 三件套 / 顾衡 reframe 'Realism vs Impressionism' / 盖尔布瓦咖啡馆）; 孔德, 谢弗勒尔, 安格尔, 德拉克罗瓦, 马奈, 波德莱尔, 居斯塔夫·库尔贝, 提香, 乔尔乔内, 现实主义, 学院派, 新古典主义, 威尼斯画派, 马赛克, 小孔成像法, 实证主义; 作品/大宫女 +02 (dedup 到 02 — 同 034 批次 MD5)
- 图片：下载 4 (3 落新文件夹 + 1 PENDING)，复用 1 (course-footer)，失败 0；PENDING_01 (大宫女) MD5 dedup 到既有 02.jpg
- 备注：
  - 本批次 `batch-038-041` 并行处理
  - 5 新人物：[[毕沙罗 Camille Pissarro]] [[莫奈 Claude Monet]]（041 主角，本课先建 stub）[[达盖尔 Louis Daguerre]] [[埃德蒙·贝克勒尔 Edmond Becquerel]] [[约翰·兰德 John Rand]]
  - 2 新概念：[[银版照相法 Daguerreotype]] folder-mode（含 1845 摄影样图）/ [[盖尔布瓦咖啡馆 Café Guerbois]]
  - 2 新作品：[[牧羊女 (毕沙罗) Girl with a Stick]]（与米勒《牧羊女》disambig）/ [[阿让特伊的花园 The Artist's Garden at Argenteuil]]
  - ⚠️ 跨 agent 协作：流派/印象派 race-condition——041 先创建，040 检测后仅在 existing_entities_to_update 标注 40 自有内容，未覆写文件；040 的 5 行对照表 / 两大成因结构 / 顾衡 reframe 留在源页正文，merger 未注入流派页（lint 时合并）

## [2026-05-13] ingest | 041｜莫奈1：颠覆式的创新从何而来？

- 新建：来源(1) 流派(1) 人物(9) 作品(9)
- 更新（待 lint backlinks）：人物/莫奈 (040 stub→ 第一篇专题), 毕沙罗 (040 stub), 马奈, 柯罗 (《风暴天》1870), 米勒, 居斯塔夫·库尔贝 (与莫奈《花园里的女人》分道扬镳), 波德莱尔, 德拉克罗瓦, 伦勃朗; 流派/学院派 (1912 拍卖落败方), 现实主义 (印象派源理念), 巴比松画派 (杜比尼影响莫奈); 技法/厚涂 (杜比尼厚涂引); 概念/巴黎沙龙
- 图片：下载 9 新作品首图（含 1 无 caption 的莫奈早期人物漫画 — 独立成页）, 课程页脚复用 1, 失败 0
- 备注：
  - 本批次 `batch-038-041` 并行处理
  - 新流派 [[印象派 Impressionism]]——041 作为主创建者
  - 9 新人物：[[雷诺阿 Pierre-Auguste Renoir]] [[巴齐依 Frédéric Bazille]]（普法战争阵亡）[[西斯莱 Alfred Sisley]] [[德加 Edgar Degas]] [[布丹 Eugène Boudin]]（莫奈思想源头）[[格莱尔 Charles Gleyre]]（反向培养印象派四骨干）[[杜比尼 Charles-François Daubigny]]（巴比松粗犷派 / 对莫奈影响最大）[[梅索尼埃 Ernest Meissonier]] [[卡美伊·东西厄 Camille Doncieux]]
  - 9 新作品：把杆的舞女（德加 1905 / 1912 拍卖纪录画）/ 莫奈早期人物漫画 / 特鲁维尔的帆船（布丹 1884）/ 傍晚：消逝的幻觉（格莱尔学院派代表）/ 风暴天（柯罗 1870）/ 春天的景色（杜比尼 1862）/ 塞纳河口（莫奈首次入选沙龙）/ 绿衣女子（模特卡美伊）/ 花园里的女人（莫奈 205×260cm 户外 + 白色打底）
  - 1912 Henri Rouart 拍卖会节点确认——印象派在艺术市场击败学院派

## [2026-05-13] merge | batch-038-041 后处理

- 4 个 lecture 并行 ingest（agents 038 / 039 / 040 / 041）→ main agent merge
- ✅ Refined prompt 显效：4 个 agents 全部遵守 vault-root-relative path 约定 (`作品/`，无 `../` / 无 `%20`)；4 个 index_additions 全部 wikilink-filename 匹配（无字符串重命名修补）
- 跨 agent 冲突解决：
  - **大量 MD5 dedup**（6/8 PENDING 命中已有文件）：038 草地上的午餐 + 浴女(Courbet)；039 草地上的午餐 + 帕里斯的审判(拉伊蒙迪) + 奥林匹亚；040 大宫女——这些 URL 不同但内容同，agent 重复下载已存图。merger 全部 dedup 到既有 01.jpg/02.jpg。
  - **真新角度图**（2/8 PENDING 落地为新 NN）：039 乌尔比诺的维纳斯/02.jpg + 鲁特琴手/02.jpg
  - **奥林匹亚 race-condition**：038 创建 .md + 01.jpg；039 看到 folder 已有 01.jpg/无 .md，仅追加图（dedup 到 01.jpg）；merger 验证后无操作。
  - **流派/印象派 race-condition**：041 先创建文件；040 退让，记 existing_entities_to_update。merger 决定 ✅ 保留 041 创建版（基础内容齐全），040 的 5 行对照表 / 两大成因 / 顾衡 reframe 留在 040 源页 + 标记 lint 合并
  - **共建实体**（040 创建、041 引用）：[[莫奈 Claude Monet]] / [[毕沙罗 Camille Pissarro]]——041 未覆写
- Backlog（留 lint）：
  - ~80 个既有人物/流派/技法/时代/作品页的 `## 出现在` 反向链接 + 各作品页的 `图片清单` 表格新行
  - 流派/印象派 + 040 内容合并（5 行对照表 / 两大成因 / Realism reframe）
  - 人物/马奈 stub → 完整传记升级（020 stub + 038/039 大量素材待整合）
  - 概念/现代性 stub → 三层综合（038 的本雅明 + 弗洛姆 + 帕特南 + 妓女母题 layer）

## [2026-05-13] ingest | 042｜莫奈2：《日出·印象》是不是印象派作品？

- 新建：来源(1) 人物(7) 作品(11) 概念(2)
- 更新（待 lint）：人物/莫奈（040 stub→ 042 完整传记中枢）, 流派/印象派 (1871 笔触诞生 + 1874 首展 + 莫奈晚期'光的外壳'), 人物/雷诺阿/毕沙罗/卡美伊·东西厄/杜比尼/马拉美/巴齐依/德加/西斯莱/马奈/莫利索, 概念/照相机的冲击/巴黎沙龙/报纸与艺术批评/画廊与经纪人体系
- 图片：下载 20 + 复用 1 (course-footer) + 1 dedup（卡普辛大道/01.jpg 与 043 同 URL 同字节）, 失败 0
- 备注：
  - 本批次 `batch-042-045` 并行处理
  - 7 新人物：[[透纳 J. M. W. Turner]] [[丢朗-吕厄 Paul Durand-Ruel]] [[塞尚 Paul Cézanne]] [[勒鲁瓦 Louis Leroy]] [[奥什逮 Ernest Hoschedé]] [[爱丽丝·奥什逮 Alice Hoschedé]] [[左拉 Émile Zola]]
  - 11 新作品：被拖去解体的无畏号战舰（透纳 1839）/ 日出·印象 / 阿让特伊的秋天 / 阿让特伊的房子 / 红罂粟 / 夏日（莫利索）/ 撑阳伞的女人 / 临终的卡美依 / 干草垛系列 / 鲁昂大教堂系列 / 睡莲系列
  - 2 新概念：[[印象派首展 (1874) First Impressionist Exhibition]] / [[组画 Series Paintings]]
  - ⚠️ 顾衡反直觉判断：《日出·印象》本身并非印象派作品而是对透纳的致敬，仅给流派提供了名字
  - ⚠️ 跨 agent 协作：卡普辛大道 race-condition（042 vs 043 同时引用），042 dedup 到 043 创建的 01.jpg；莫利索 race-condition（042 vs 045），042 只链接，045 拥有该页

## [2026-05-13] ingest | 043｜雷诺阿：妥协如何造就大师？

- 新建：来源(1) 人物(2) 作品(16)
- 更新：(parallel-safe mode：所有现成实体页留待 lint 添加 backlink)
- 图片：下载 16 新作品首图，3 PENDING 全部 MD5 dedup（奥林匹亚/娜娜/大宫女）→ 01.jpg 引用, 失败 0
- 备注：
  - 本批次 `batch-042-045` 并行处理
  - 2 新人物：[[古诺 Charles Gounod]] [[夏庞蒂埃 Georges Charpentier]]
  - 16 新作品（雷诺阿 11 + 莫奈 2 + 马奈 1 + 跨 agent 共建 1）：男人与狗 / 蛙塘 / 卡普辛大道（与 042 共建）/ 包厢 / 阳光下的裸女 / 穿和服的卡美伊 / 萨玛丽夫人 / 摘花 / 夏庞蒂埃夫人和她的孩子们 / 达威尔小姐像 / 划船者的午餐 / 左拉肖像 (马奈) / 女人在花园里 (Renoir disambig) / 金发浴女 / 浴女们 / 翘二郎腿的浴女
  - ⚠️ 同名近义 disambig：[[女人在花园里 Woman at the Garden (Renoir)]]（雷诺阿 1890）vs 既存 [[花园里的女人 Women in the Garden]]（莫奈 1866）

## [2026-05-13] ingest | 044｜莫利索和毕沙罗：最纯正的印象派什么样？

- 新建：来源(1) 人物(2) 作品(14)
- 更新：人物/毕沙罗 Camille Pissarro（040 stub → 完整传记）, 其他实体页待 lint backlink
- 图片：下载 14 新作品首图 + 4 PENDING（全部 MD5 dedup 到既有 01.jpg：秋千 / 阳台 / 奥林匹亚 / 牧羊女(毕沙罗)），失败 0
- 备注：
  - 本批次 `batch-042-045` 并行处理
  - 2 新人物：[[戈雅 Francisco Goya]]（《阳台上的玛哈》是马奈《阳台》构图来源）[[高更 Paul Gauguin]]（毕沙罗引入印象派画展）
  - 14 新作品（莫利索 6 + 毕沙罗 7 + 马奈 1 + 戈雅 1）
  - ⚠️ 跨 agent 协作：莫利索人物页 race-condition——045 用 `莫利索 Berthe Morisot.md` 名称先创建；044 删除自己写的 `贝尔特·莫利索` 重复页，所有 wikilink 重指。Alias `贝尔特·莫利索` 建议 lint 时加入 045 版的页

## [2026-05-13] ingest | 045｜德加：为什么印象派以他结束？

- 新建：来源(1) 人物(4) 作品(12)
- 更新：人物/德加 Edgar Degas（041 stub → 完整专题：五大不同 / 线条系统 / 物哀 / 凡·高误读 vs 瓦雷里真解 / 终生未娶 / 刻薄性格 / 普法战争眼疾，50→122 行）
- 图片：下载 13 新作品首图 + 2 PENDING（全部 MD5 dedup 到既有 01.jpg：把杆的舞女 / 瓦平松的浴女），失败 0
- 备注：
  - 本批次 `batch-042-045` 并行处理
  - 4 新人物：[[莫利索 Berthe Morisot]]（044 专题主角，本课先建页）[[凡·高 Vincent van Gogh]] [[瓦雷里 Paul Valéry]] [[阿尔弗雷德·德·缪塞 Alfred de Musset]]
  - 12 新作品（德加 11 + 莫利索 1）：贝列里一家 / 舞女在台上 / 舞女登台 / 芭蕾明星 / 蓝衣舞女 / 着蝴蝶舞衣的舞女 / 舞蹈考试 / 舞蹈课 / 彩排 / 浴盆 / 迈入盆中的浴女 / 姐妹 (莫利索)
  - ⚠️ 索引旧 bug 发现（不在本批 scope）：index.md `[[瓦平松的浴女 La Grande Baigneuse]]` 不匹配实际文件夹 `瓦平松的浴女 Valpinçon Bather`，broken wikilink 从 032 留下；lint 时统一

## [2026-05-13] merge | batch-042-045 后处理

- 4 个 lecture 并行 ingest（agents 042 / 043 / 044 / 045）→ main agent merge
- ✅ Refined prompt（vault-root paths + 文件名-wikilink 匹配）依然显效：4 agents 全部无路径漂移、无 wikilink 错位
- 🆕 100% dedup 率：所有 9 个 PENDING clippings 全部 MD5 dedup 到既有 01.jpg（agents 重复下载已存图）。其中 042 还在 inline dedup 了卡普辛大道。
- 跨 agent race-condition 解决：
  - **卡普辛大道 Boulevard des Capucines**：042 vs 043 同时引用，043 先创建文件夹，042 inline dedup 到 043 的 01.jpg
  - **莫利索 Berthe Morisot**：044 vs 045 同时创建，044 自我撤销重复页（删除 `贝尔特·莫利索` 自写版），wikilink 全部指向 045 版本
  - **stub → 完整传记**（agents 安全扩展由 prompt 允许）：人物/毕沙罗 (040 stub→ 044 完整传记)；人物/德加 (041 stub→ 045 完整专题)；人物/莫奈 (040 stub→ 042 完整传记的主源)
- 旧 bug 发现（留 lint）：
  - 大宫女/01.jpg 与 大宫女/02.jpg MD5 byte-identical（从 034 batch 1 留下；merge 时未发现）
  - index.md `[[瓦平松的浴女 La Grande Baigneuse]]` 链接错（应为 `Valpinçon Bather`）
- Backlog（留 lint）：
  - ~100+ 既有人物/流派/技法/时代/作品页的 `## 出现在` 反向链接 + 各作品页的 `图片清单` 表格新行
  - 流派/印象派 持续合并 040 的 5 行对照表 + 042 的'1871 笔触诞生 + 1874 首展 + 光的外壳'扩写
  - 莫利索页 alias 「贝尔特·莫利索」 添加 + 044 传记内容注入
  - 人物/马奈 大幅扩写（040/038/039/042 累计大量素材待整合）

## [2026-05-13] ingest | 046｜如何运用"时代之眼"来看画？

- 新建：来源(1) 0 实体 — 期中复习课
- 更新（待 lint）：~20 既有实体 backlink；merger 新建 [[黄色的基督 The Yellow Christ]] artwork stub（046 顾衡用为"印象派之后看不懂"样本，未来 Gauguin 专题扩展）
- 图片：下载 7 全部 PENDING；merger 处理后 4 dedup（卡普辛大道 / 奥林匹亚 / 吉斯泽肖像 / 教皇利奥十世）+ 2 真新角度图（劫夺留西帕斯 03 / 萨尔丹纳帕拉 03）+ 1 新作品（黄色的基督 01）
- 备注：本批次 `batch-046-049` 并行处理；046 是期中复习课，0 件新实体；6/7 张图为既有 + 1 张《黄色的基督》merger 创建新 folder stub

## [2026-05-13] ingest | 047｜修拉：新印象主义为什么走进了死胡同？

- 新建：来源(1) 流派(1) 人物(6) 技法(2) 作品(6) 概念(3)
- 更新：（parallel-safe 模式，既有页留 lint 回填 backlink）
- 图片：下载 7（含 1 张色轮 concept-illustration 落 概念/分色主义/01.png），复用 1 course-footer，失败 0；0 PENDING
- 备注：
  - 本批次 `batch-046-049` 并行处理
  - 新流派 [[新印象主义 Neo-Impressionism]]——修拉开创、科学化印象派
  - 6 新人物：[[修拉 Georges Seurat]] [[西涅克 Paul Signac]] [[费奈昂 Félix Fénéon]]（命名人）[[大卫·苏特 David Sutter]] [[昂里 Charles Henry]]（格式塔先声）[[莱曼 Henri Lehmann]]（修拉师傅）
  - 2 新技法：[[点彩 Pointillism]] / [[视觉混和 Optical Mixing]]
  - 6 新作品：大碗岛的星期天下午 / 收干草(毕沙罗) / 弹钢琴的女人(凡高) / 康康舞 / 马戏（修拉遗作）/ 擦粉的少女
  - 3 新概念：[[分色主义 Divisionism]] folder-mode（含色轮 01.png）/ [[更细笔触致画面变暗 Smaller Dot Darkening]] / [[艺术中的科学主义 Scientism in Art]]
  - 与 048 race: 大碗岛 文件夹 047 owns；048 staged dup clipping，merger MD5 dedup 到 01.jpg

## [2026-05-13] ingest | 048｜什么是象征主义？

- 新建：来源(1) 流派(1: 象征主义) 人物(7) 作品(3) 概念(3)
- 更新（待 lint）：马拉美 / 孔德 / 马奈 / 左拉 — 仅追加出现在
- 图片：下载 3，复用 1 course-footer，1 PENDING (大碗岛 — agent 自己 MD5-confirm 与 047 同 → dedup 到 01.jpg)，失败 0
- 备注：
  - 本批次 `batch-046-049` 并行处理
  - 新流派 [[象征主义 Symbolism]]——048 owns 导论 lecture，049 是案例
  - 7 新人物：[[莫罗 Gustave Moreau]]（早期代表）[[加缪 Albert Camus]] [[古斯塔夫·康恩 Gustave Kahn]]（'主观的客观化'金句）[[让·莫亚雷斯 Jean Moréas]]（1886 宣言作者）[[斯金纳 B. F. Skinner]] [[徐志摩 Xu Zhimo]]（马拉美中文同构）[[丢沙丹 Édouard Dujardin]]
  - 3 新作品：[[俄狄浦斯与狮身人面像 (莫罗) Oedipus and the Sphinx]] / [[幻想 (夏凡纳) Fantasy]] / [[马拉美的肖像 Portrait of Stéphane Mallarmé]]（马奈 1876）
  - 3 新概念：[[主观的客观化 Objectification of the Subjective]] / [[象征主义宣言 Symbolist Manifesto]] / [[牧神的午后 (诗) The Afternoon of a Faun]]
  - 顾衡核心命题：象征主义=主观的客观化 + 西方现代绘画'看不懂'起点；与新印象主义共享实证主义/科学方法论支撑

## [2026-05-13] ingest | 049｜夏凡纳：如何制作象征主义的密电码？

- 新建：来源(1) 人物(5) 作品(9)
- 更新（待 lint）：乔托 / 杜乔（夏凡纳真正师承）/ 德拉克罗瓦 / 库退尔（挂名师徒）/ 马拉美 / 左拉 / 流派/象征主义 / 流派/拜占庭艺术（跨 45 讲回响）
- 图片：下载 9，复用 1 course-footer，失败 0；0 PENDING
- 备注：
  - 本批次 `batch-046-049` 并行处理
  - 5 新人物：[[夏凡纳 Pierre Puvis de Chavannes]]（主角，象征主义"简化路径"代表）+ 4 中国当代画家（[[刘春华 Liu Chunhua]] [[孟禄丁 Meng Luding]] [[张群 Zhang Qun]] [[毛旭辉 Mao Xuhui]]）
  - 9 新作品（夏凡纳 4 + 乔托 1 + 杜乔 1 + 中国当代 3）：贫穷的渔夫 / 希望(夏凡纳) / 死亡与少女(夏凡纳) / 冥想(夏凡纳) / 犹大之吻(乔托) / 耶稣进入耶路撒冷(杜乔) / 毛主席去安源 / 在新时代——亚当夏娃的启示 / 红色人体
  - 核心命题：象征主义在绘画端的'简化'路径——夏凡纳借鉴乔托/杜乔蛋彩壁画 → 颜色雅淡 + 构图简单 + 舞台剧标准动作 → 密电码式造型 → 模特可有可无 → 西方绘画再次抛弃眼睛所见的真实，回到拜占庭式造型逻辑
  - merger 新建 [[八五新潮 '85 New Wave]] concept stub 解决 049 中 7 处 wikilink 未指（5 中国画家页 + 2 作品页）

## [2026-05-13] merge | batch-046-049 后处理

- 4 个 lecture 并行 ingest（agents 046 / 047 / 048 / 049）→ main agent merge
- ✅ 0 路径漂移，0 wikilink 错位（refined prompt 持续显效）
- PENDING 处理：8 个总数（046 有 7 个 + 048 有 1 个），其中 5 个 dedup（卡普辛大道 / 奥林匹亚 / 吉斯泽肖像 / 教皇利奥十世 + 048 大碗岛）+ 2 真新角度图（劫夺留西帕斯/03 + 萨尔丹纳帕拉/03）+ 1 全新作品文件夹（黄色的基督 / 高更 / 1889 由 046 引为'印象派之后看不懂'样本，merger 创建 stub）
- 047 vs 048 race-condition：大碗岛 The Grande Jatte 文件夹 047 创建 + 01.jpg；048 staged 同 URL clipping，agent 自己 MD5-confirm 后标 dedup；merger 验证后 drop clipping，rewrite PENDING_02 → 01
- 047 vs 048 vs 049 wikilink 委托正常：修拉/新印象主义/西涅克/费奈昂/昂里 → 047；象征主义流派页 → 048；夏凡纳 → 049
- merger 自建：
  - [[黄色的基督 The Yellow Christ]]（artwork stub，folder + 01.jpg + .md）—— 046 PENDING 引用了不存在的文件夹，merger 落地
  - [[八五新潮 '85 New Wave]]（concept stub）—— 049 在 5 中国画家页 + 2 中国作品页中 wikilink 引用但未创建，merger 落地解决断链
- Backlog（留 lint）：
  - ~50 既有人物/流派/技法/时代/作品页的 `## 出现在` 反向链接 + 各作品页 `图片清单` 表格新行
  - 人物/马拉美 stub → 完整传记（039 + 048 + 049 累计大量素材）
  - 流派/拜占庭艺术 跨 45 讲回响节（049 提到象征主义=回到拜占庭式程式化）
  - 黄色的基督 stub → 完整作品页（待 Gauguin 专题 lecture，约 050+）
  - 历史 bug：047 创建的 [[新印象主义 Neo-Impressionism]] vs 既有 `流派/` 命名规范——若有 vs 应在 lint 时一致化

## [2026-05-13] ingest | 050｜莫罗：象征主义绘画为什么走向朦胧？

- 新建：来源(1) 人物(3) 作品(5) 概念(1)
- 更新：人物/莫罗 (048 stub → full, 莫罗 EXCEPTION), 人物/于斯曼 + 人物/兰波（051 并行新建，050 增 backlink）
- 图片：下载 5 新作品首图, 2 PENDING 全部 MD5 dedup (俄狄浦斯 + 希望) → 01.jpg, 复用 1 course-footer, 失败 0
- 备注：
  - 本批次 `batch-050-053` 并行处理
  - 3 新人物：[[夏塞里奥 Théodore Chassériau]] [[泰奥多尔·德·维塞瓦 Teodor de Wyzewa]] [[阿当 Paul Adam]]
  - 5 新作品：法厄同 (莫罗) / 在希律王前舞蹈的莎乐美 / 显灵 / 莎乐美 (莫罗 1875) / 帕卡与死亡天使
  - 1 新概念：[[莎乐美 Salome]]（圣经母题升级为致命女性象征）
  - 顾衡核心命题：象征主义朦胧路径——繁复细节 + 拒斥具体含义 + '女人是老虎'母题
  - 与 051 race：兰波/于斯曼/逆流 由 051 创建，050 按约 backlink 即可

## [2026-05-13] ingest | 051｜雷东：怪诞是不是象征主义的方向？

- 新建：来源(1) 人物(8) 作品(11) 概念(3)
- 更新：（parallel-safe, 既有页留 lint 回填）
- 图片：下载 11 新作品首图, 复用 1 course-footer, 失败 0; 0 PENDING
- 备注：
  - 本批次 `batch-050-053` 并行处理
  - 8 新人物：[[雷东 Odilon Redon]] [[于斯曼 Joris-Karl Huysmans]] [[兰波 Arthur Rimbaud]] [[叶芝 W. B. Yeats]] [[贝克特 Samuel Beckett]] [[塞万提斯 Miguel de Cervantes]] [[热罗姆 Jean-Léon Gérôme]] [[达利 Salvador Dalí]]
  - 11 新作品（雷东早期黑白 + 中期 + 晚期色彩）：眼睛像奇诡的气球飘向无穷 / 大卫与歌利亚(雷东) / 哭泣的蜘蛛 / 展望 / 佛陀(雷东) / 花瓶中的花 / 花瓶 / 独眼巨人 / 黄色背景的树 / 哥特式拱门下的女人 / 维纳斯的诞生(雷东)
  - 3 新概念：[[逆流 (于斯曼) À rebours]] / [[等待戈多 Waiting for Godot]] / [[大铁鸟 (货物崇拜) Cargo Cult]]（顾衡核心比喻）
  - 顾衡核心命题：象征主义第三条路径——梦境/怪诞；与 049 简化 / 050 繁复并列构成三部曲收束

## [2026-05-13] ingest | 052｜塞尚1：为什么他是西方现代绘画之父？

- 新建：来源(1) 流派(1: 后印象派) 人物(1: 罗杰·弗莱) 作品(4) 概念(1)
- 更新：人物/塞尚 (042 stub → 主页, 052 EXCEPTION, 留 053 sibling 后续扩展)
- 图片：下载 4 新作品首图, 1 PENDING dedup 到既有 01.jpg (草地上的午餐 Manet), 复用 1 course-footer, 失败 0
- 备注：
  - 本批次 `batch-050-053` 并行处理
  - 新流派 [[后印象派 Post-Impressionism]]——1910 罗杰·弗莱命名（塞尚/高更/凡·高三人）
  - 新人物 [[罗杰·弗莱 Roger Fry]]——后印象派的命名者
  - 4 新作品：读《事件》报的父亲 / 草地上的午餐 (塞尚) / 耶稣在灵薄狱 / 风景 (塞尚 1867)
  - 1 新概念：[[艺术的道统 (形式美) Artistic Lineage]]（顾衡用语）
  - 顾衡核心命题：塞尚的三大贡献——色彩塑形 / 颜料质地独立 / 画我所想；042 已预告其'西方现代绘画之父'地位，052 完整兑现
  - 与 053 race：草地上的午餐 (塞尚) 文件夹 052 用 1869 标注，053 提出 1865 异议（顾衡 053 caption 不同）；merger 决定保留 052 命名

## [2026-05-13] ingest | 053｜塞尚2：如何打造艺术的平行世界？

- 新建：来源(1) 人物(2) 技法(2) 作品(7) 概念(2)
- 更新（待 lint）：人物/塞尚 (deferred to lint; 052 已 extension, 053 内容待合并), 人物/罗杰·弗莱 (052 创建; 053 增'分节'内容), 人物/毕沙罗 / 马奈 / 库尔贝 / 左拉 / 德拉克罗瓦 / 流派/印象派 / 概念/印象派首展 / 技法/厚涂 / 技法/线性透视; 作品/草地上的午餐(塞尚) +02 (053 新角度图)
- 图片：下载 7 新作品首图, 4 PENDING (3 dedup: 草地上的午餐Manet/奥林匹亚/草地上的午餐塞尚部分; 2 真新角度图: 草地上的午餐(塞尚)/02 + 萨尔丹纳帕拉/04), 复用 1 course-footer, 失败 0
- 备注：
  - 本批次 `batch-050-053` 并行处理
  - 2 新人物：[[贝尔纳 Émile Bernard]]（塞尚晚年观察记录者）[[索绪尔 Ferdinand de Saussure]]（沃尔夫'分节'对立面）
  - 2 新技法：[[平行笔触 Parallel Brushstrokes]] / [[主观色彩序列 Subjective Colour Sequence]]
  - 7 新作品：现代奥林匹亚 / 奥维尔的环路 / 蓬图瓦兹的道路(毕沙罗) / 蓬图瓦兹的道路(塞尚) / 曼西之桥 / 三个浴女 / 圣维多利亚山
  - 2 新概念：[[沃尔夫假说 Whorfian Hypothesis]] / [[分节 Articulation]]
  - 顾衡核心命题：塞尚以平行短笔触 + 主观色彩序列 + 分节式结构性 → 打造与客观世界平行的艺术世界

## [2026-05-13] merge | batch-050-053 后处理

- 4 个 lecture 并行 ingest（agents 050 / 051 / 052 / 053）→ main agent merge
- ✅ 0 路径漂移, 0 wikilink 错位
- PENDING 处理：7 个总数中 5 dedup (俄狄浦斯/希望/草地上的午餐 Manet ×2/奥林匹亚) + 2 真新角度图 (草地上的午餐(塞尚)/02 + 萨尔丹纳帕拉/04)
- 跨 agent race-condition 解决：
  - **兰波/于斯曼/逆流 (于斯曼) À rebours**: 051 owns; 050 仅 backlink
  - **草地上的午餐 (塞尚) Luncheon on the Grass (Cézanne)**: 052 创建（标 1869），053 撤回自己写的同名 folder 并复用 052 命名 + PENDING_02 加新角度图
  - **人物/塞尚**: 042 stub → 052 extends（052 EXCEPTION）→ 053 defers（053 全部增量留 lint 合并）
  - **人物/罗杰·弗莱**: 052 创建; 053 仅 backlink + 分节内容延 lint
- Backlog（留 lint）：
  - ~80 既有人物/流派/技法/作品页的 `## 出现在` 反向链接 + 各作品页 `图片清单` 表格新行
  - 人物/塞尚 053 内容合并（早期激进期 + 与毕沙罗写生 + 艺术观三大支柱 + 弗莱判断）
  - 人物/罗杰·弗莱 053 内容合并（分节论 + 塞尚知性判断）
  - 流派/象征主义 050-051 内容合并（繁复路径 + 怪诞路径 + 三部曲框架）
  - 莫罗 + 雷东 stub 已升级（050/051 EXCEPTION）— 但与 048 创建的 stub 内容需 lint 时统一

## [2026-05-13] ingest | 054｜塞尚3：为什么理解塞尚那么困难？

- 新建：来源(1) 作品(6) 概念(1)
- 更新：人物/塞尚 (扩展到 ~170 行；三阶段方法论 + 7 件 054 代表作); 既有作品 3 个：草地上的午餐 (塞尚)/02 dedup、蓬图瓦兹的道路 (塞尚)/01 dedup、圣维多利亚山 +5 新版本 (02-06)
- 图片：下载 14, 1 dedup (圣维多利亚山 PENDING_07 = existing 01) + 2 PENDING dedup (草地上的午餐塞尚 PENDING_03 = existing 02; 蓬图瓦兹道路塞尚 PENDING_02 = existing 01), 5 真新角度图 (圣维多利亚山 02/03/04/05/06), 复用 1 course-footer, 失败 0
- 备注：塞尚生涯三阶段终章；新概念 [[结晶 (塞尚) Crystallization]] (Roger Fry 命名); 圣维多利亚山系列 6 版完整呈现 (1885/1887/1895/1902/1905/1906); 塞尚 stub→主页累积扩到 170 行

## [2026-05-13] ingest | 055｜高更1：为什么从印象派走向象征主义？

- 新建：来源(1) 人物(1) 作品(11) 概念(2)
- 更新：人物/高更 (044 stub → 完整传记 1848-1888 印象派→象征主义过渡期); 黄色的基督 stub 扩展
- 图片：下载 11 新作品首图, 复用 1 course-footer, 失败 0
- 备注：
  - 本批次 `batch-054-057` 并行处理
  - 1 新人物 [[安奎丹 Louis Anquetin]]（与贝尔纳共创景泰蓝派）
  - 2 新概念 [[景泰蓝派 Cloisonnism]] / [[阿旺桥 Pont-Aven]]
  - 11 新作品（高更 10 + 贝尔纳 1）：花园里的人物 / 比霍雷尔教堂下的果园 / 树下的小屋 / 有三条小狗的静物 / 打干草(高更) / 三个跳舞的布列塔尼女孩儿 / 布列塔尼的鹅 / 布列塔尼的干草堆 / 头形花瓶和日本木刻静物 / 布列塔尼农妇(贝尔纳) / 雅各与天使搏斗
  - 高更阿旺桥时期完整呈现；下一课 056 接塔希提期

## [2026-05-13] ingest | 056｜高更2：象征主义还能走多远？

- 新建：来源(1) 流派(1: 综合主义) 人物(2) 作品(8)
- 更新（待 lint）：人物/高更 (055 已主创建; 056 内容延 lint) / 流派/象征主义 / 流派/后印象派 / 多个 人物/作品 backlinks
- 图片：下载 9 新作品首图, 2 PENDING dedup (黄色的基督 + 雅各与天使搏斗 均与既有 01.jpg MD5 同), 失败 0
- 备注：
  - 本批次 `batch-054-057` 并行处理
  - 新流派 [[综合主义 Synthetism]]——1888 高更+贝尔纳共创
  - 2 新人物 [[奥里耶 Albert Aurier]]（1890 高更象征主义旗手命名人）[[米尔博 Octave Mirbeau]]
  - 8 新作品：失贞 / 阿尔附近的风景 / 阿尔的风景 / 黑猪 / 海边 Fatata te Miti / 神的日子 Mahana no atua / 死人的注视 Manao Tupapau / 我们从哪里来,我们是谁,我们要往哪里去
  - ⚠️ 跨 agent race-condition resolved：055 创建 [[景泰蓝派 Cloisonnism]] / [[阿旺桥 Pont-Aven]]；056 撤回自写 dup（阿旺桥画派 / 景泰蓝主义），wikilinks 全部指 055 命名

## [2026-05-13] ingest | 057｜凡·高1：为什么说他"性格决定命运"？

- 新建：来源(1) 人物(4) 作品(9) 概念(1)
- 更新：人物/凡·高 (045 stub → 完整传记 1853-1886 荷兰时期)
- 图片：下载 11 新作品+人物首图, 复用 1 course-footer, 失败 0; 0 PENDING
- 备注：
  - 本批次 `batch-054-057` 并行处理
  - 4 新人物：[[提奥 Theo van Gogh]]（终身资助者）[[尤金妮娅·洛耶 Eugénie Loyer]] [[凯·沃斯 Kee Vos]] [[西恩·霍尼克 Sien Hoornik]]（folder-per-person mode for 2 of them since 肖像照 not artwork）
  - 1 新概念 [[古比尔画廊 Goupil & Cie]]（凡·高家族产业）
  - 9 新作品 (1879-1885 荷兰时期素描+油画)：铲煤工 / 壁炉边 / 在路上 / 花田 / 织工 / 悲伤 / 西恩母亲的后花园 / 停尸床上的女人 / 吃土豆的人（凡·高荷兰时期顶峰）
  - 058/059+ 凡·高 2/3 待续

## [2026-05-13] merge | batch-054-057 后处理

- 4 个 lecture 并行 ingest（agents 054 / 055 / 056 / 057）→ main agent merge
- ✅ 0 路径漂移, 0 wikilink 错位
- PENDING 处理：10 个总数中 5 dedup + 5 真新角度图 (全部 054 的圣维多利亚山 02-06)
- 跨 agent race-condition 解决：
  - **景泰蓝派 / 阿旺桥**: 055 owns; 056 撤回 dup pages
  - **雅各与天使搏斗**: 055 创建 + 01.jpg; 056 staged dup clipping, MD5-confirmed → dedup
  - **黄色的基督**: stub by 046 batch merger, 055 期望扩展; 056 staged dup → dedup
  - **人物/高更**: 044 stub → 055 EXCEPTION 扩展为完整传记; 056 defer lint
  - **人物/塞尚**: 052/053/054 三次扩展，054 把页累积到 ~170 行（仍可控）
  - **人物/凡·高**: 045 stub → 057 EXCEPTION 扩展为完整传记 1853-1886（058+ 续）
- Backlog（留 lint）：
  - ~100 既有人物/流派/技法/作品页的 `## 出现在` 反向链接
  - 综合主义 vs 景泰蓝派 vs 阿旺桥 之间的概念层级关系（lint 期梳理）
  - 人物/高更 056 塔希提期内容合并
  - 人物/塞尚 后续 lint 期切分子章节（避免超 200 行）
  - [[日本浮世绘 Ukiyo-e]] 在 055 三处被 wiki-linked 但未建页（gap）

## [2026-05-13] ingest | 058｜凡·高2：为什么他的风格难以界定？

- 新建：来源(1) 人物(2) 作品(8)
- 更新：人物/凡·高 (057 → 058 巴黎期 1886-1888 大段)
- 图片：下载 8 新作品首图, 3 PENDING 全部 MD5 dedup (吃土豆的人/睡莲系列/弹钢琴的女人), 复用 1 course-footer
- 备注：本批次 `batch-058-061`; 蒙蒂切利+亚历山大·里德 新建; 风景 (凡·高 1888) 是暂用名待 disambig

## [2026-05-13] ingest | 059｜凡·高3：他为什么走向毁灭？

- 新建：来源(1) 人物(3) 作品(11)
- 更新：人物/凡·高 (058 → 059 病理生理 + 阿尔/Saint-Rémy/Auvers + 提奥心理; sources 3→4)
- 图片：下载 12 新作品首图, 1 PENDING dedup (吃土豆的人 同 057), 复用 1 course-footer
- 备注：
  - 本批次 `batch-058-061`
  - 3 新人物: [[颜料商唐吉老爹 Père Tanguy]] [[舒菲奈克 Émile Schuffenecker]] [[毛姆 Somerset Maugham]]
  - 11 新作品 (Arles/Saint-Rémy/Auvers): 丰收(凡高) / 15朵向日葵 / 黄房子 / 卧室(凡高) / 阿尔咖啡馆露台 / 耳朵打绷带的自画像 / 奥维尔小教堂 / 丝柏 / 星月夜 / 自画像 1889 / 麦田群鸦 (Auvers 遗作)
  - ⚠️ 路径冲突已 merger 解决：059 pre-created 红色葡萄园 (无 的) vs 058 canonical 红色的葡萄园——dup 文件已删除, 059 source page wikilink 修正

## [2026-05-13] ingest | 060｜马蒂斯1：野兽派从何而来？

- 新建：来源(1) 流派(1: 野兽派) 人物(7) 作品(11) 概念(1)
- 更新：（parallel-safe, 既有页留 lint）
- 图片：下载 12 新作品首图 (含 与 061 byte-identical 戴帽子的女人/01.jpg), 2 PENDING 真新角度图 (三个浴女/02 + 草地上的午餐/02), 复用 1 course-footer
- 备注：
  - 本批次 `batch-058-061`
  - 新流派 [[野兽派 Fauvism]]——060 owns 导论
  - 7 新人物：[[马蒂斯 Henri Matisse]] [[德朗 André Derain]] [[弗拉芒克 Maurice de Vlaminck]] [[马尔凯 Albert Marquet]] [[多纳泰罗 Donatello]] [[瓦克塞尔 Louis Vauxcelles]] (1905 反向命名野兽派+1908 立体主义) [[布格罗 William-Adolphe Bouguereau]]
  - 11 新作品（马蒂斯 9 早期+中期 + 多纳泰罗大卫 + 塞尚浴女们 1874）
  - 1 新概念 [[秋季沙龙展 Salon d'Automne]]（1903 创立）
  - ⚠️ 跨 agent race: 戴帽子的女人 race-condition with 061; 061 owns .md; 060 仅下载 01.jpg

## [2026-05-13] ingest | 061｜马蒂斯2：为什么说野兽派不"野兽"？

- 新建：来源(1) 人物(6) 作品(4) 概念(3) 技法(1)
- 更新：（parallel-safe, 既有页留 lint）
- 图片：下载 6 (4 新作品+2 PENDING 真新+假新), 1 真新角度图 (希望(夏凡纳)/02), 1 PENDING dedup (黄色的基督/01), 复用 1 course-footer
- 备注：
  - 本批次 `batch-058-061`
  - 6 新人物：[[蒙弗雷德 Georges-Daniel de Monfreid]] [[卢奥 Georges Rouault]] [[勃拉克 Georges Braque]] [[杜菲 Raoul Dufy]] [[弗里兹 Othon Friesz]] [[普雷齐奥西 Donald Preziosi]]
  - 4 新作品 (马蒂斯 1905-1906 野兽派核心)：戴帽子的女人 / 绿线 / 开着的窗户 / 生活的欢乐
  - 3 新概念：[[为色彩而色彩 Colour for Colour's Sake]] / [[安乐椅 (马蒂斯) Armchair Art]] / [[分节 (塞尚) Passage]]
  - 1 新技法 [[平涂 Flat Colour]]
  - ⚠️ 同名概念 [[分节 (塞尚) Passage]] (061) vs [[分节 Articulation]] (053)——同概念不同术语, lint 时合并

## [2026-05-13] merge | batch-058-061 后处理

- 4 个 lecture 并行 ingest → main agent merge
- ✅ 0 路径漂移, 0 wikilink 错位
- PENDING 处理: 9 个 — 6 dedup (吃土豆的人 ×2 / 睡莲系列 / 弹钢琴的女人 / 黄色的基督) + 3 真新角度图 (060: 三个浴女/02 + 草地上的午餐/02; 061: 希望(夏凡纳)/02)
- 跨 agent race-condition 解决：
  - **红色葡萄园 vs 红色的葡萄园**: 058 wrote canonical (with 的); 059 pre-created dup (without 的); merger deletes dup folder contents, 059 source wikilink fixed
  - **戴帽子的女人**: 060 vs 061 both wanted; 061 owns .md (with 060 wrote 01.jpg); 060 references via wikilink
  - **野兽派/马蒂斯/德朗/马尔凯/弗拉芒克**: 060 owns; 061 defers
  - **人物/凡·高**: 057 stub → 058 巴黎期 → 059 Saint-Rémy/Auvers (sources 1→2→3→4); 多次扩展安全
- Backlog（留 lint）：
  - ~100+ 既有人物/流派/作品页的 `## 出现在` 反向链接
  - [[分节 Articulation]] (053) + [[分节 (塞尚) Passage]] (061) 概念合并
  - 红色葡萄园 dup 空文件夹 rmdir（sandbox 默认拒绝）
  - 风景 (凡·高 1888) 暂用名待 disambig 到具体画作
  - [[19世纪 19th Century]] / [[20世纪 20th Century]] / [[立体主义 Cubism]] / [[表现主义 Expressionism]] / [[亚维农的少女 Les Demoiselles d'Avignon]] / [[舞蹈 La Danse]] / [[斯泰因兄妹]] / [[日本浮世绘 Ukiyo-e]] 等多个 forward wikilink gap

## [2026-05-13] ingest | 062｜马蒂斯3：如何理解他一生的创作？

- 新建：来源(1) 流派(2: 立体主义+表现主义 stubs) 人物(3) 技法(1: 剪纸) 作品(9) 概念(4)
- 更新：人物/马蒂斯 (sources 1→3 — 中后期 + 柏格森转向 + 剪纸升格)
- 图片：下载 10, 复用 1 course-footer, 失败 0; 0 PENDING
- 备注：
  - 本批次 `batch-062-065` 并行处理
  - 3 新人物：[[贝伦森 Bernard Berenson]] [[柏格森 Henri Bergson]] [[史楚金 Sergei Shchukin]]
  - 4 新概念（柏格森体系）：生命哲学 / 直觉 (Bergson) / 绵延 / 准确不等于真实
  - 1 新技法 [[剪纸 Cut-outs]]（马蒂斯晚年）
  - 9 新作品：有雕像的静物 / 红色的和谐 / 舞蹈(马蒂斯) / 音乐(马蒂斯) / 西班牙静物(马蒂斯) / 伊西的花园 / 粉色的裸女 / 伊卡洛斯(马蒂斯) / 蓝色裸女系列剪纸
  - 立体主义+表现主义 stubs 提前建（062 引用，064/065/后续完整建）—— 解决多 lecture 的 forward wikilink gap

## [2026-05-13] ingest | 063｜野兽派，除了马蒂斯还能谈什么？

- 新建：来源(1) 人物(1: 米罗) 作品(18)
- 更新：人物/德朗 + 弗拉芒克 + 杜菲 (sources 1→2; 提供详细传记)
- 图片：下载 19, 8 PENDING 全部 MD5 dedup → 既有 01.jpg (含修正 亚维农的少女→亚威农少女 命名)
- 备注：
  - 本批次 `batch-062-065` 并行处理
  - 1 新人物 [[米罗 Joan Miró]]（虽超前但 063 引《丑角狂欢节》）
  - 18 新作品（野兽派 17 + 米罗 1）：
    - 德朗 6: 老树 / 滑铁卢大桥 / 海德公园 / 威斯敏斯特大桥 / 科利乌尔的山 / 两只小船
    - 弗拉芒克 3: 红树 / 布吉瓦尔帆船赛 / 水边风景
    - 杜菲 9: 有干草垛的立体主义风景 / 地中海居民 / 考斯的帆船比赛 / 阿拉伯骑士 / 帆船赛的回归 / 威尼斯拉多加纳 / 海葵 / 橙色音乐会
    - 米罗 1: 丑角狂欢节
  - ⚠️ 跨 agent: 亚维农的少女 wikilink → 亚威农少女 (065 canonical) — merger 全文 rename

## [2026-05-13] ingest | 064｜毕加索1：如何理解"蓝色时期"和"玫瑰红时期"？

- 新建：来源(1) 人物(6) 作品(19) 概念(2)
- 更新：（parallel-safe, 既有页留 lint）
- 图片：下载 19, 1 PENDING dedup (戴帽子的女人/01.jpg 与 061 同 MD5), 失败 0
- 备注：
  - 本批次 `batch-062-065` 并行处理
  - 6 新人物：[[毕加索 Pablo Picasso]] [[曼雅克 Pere Mañach]] [[沃拉尔 Ambroise Vollard]] [[费尔南德 Fernande Olivier]] [[埃尔·格列柯 El Greco]] [[劳特累克 Henri de Toulouse-Lautrec]]
  - 2 新概念：[[蓝色时期 Blue Period]] / [[玫瑰红时期 Rose Period]]
  - 19 新作品（毕加索早期 1895–1905）：含蓝色时期代表 [[老吉他手 The Old Guitarist]] / [[人生 (毕加索) La Vie]] + 玫瑰红时期 [[拿烟斗的男孩 Boy with a Pipe]]（1.04 亿拍卖）

## [2026-05-13] ingest | 065｜毕加索2：如何理解"黑人时期"？

- 新建：来源(1) 人物(5) 作品(10) 概念(1)
- 更新：（parallel-safe, 既有页留 lint）
- 图片：下载 11, 3 PENDING 全部 MD5 dedup (圣维多利亚山/生活的欢乐/蒙娜丽莎), 失败 0
- 备注：
  - 本批次 `batch-062-065` 并行处理
  - 5 新人物：[[格特鲁德·斯坦因 Gertrude Stein]] [[阿波利奈尔 Guillaume Apollinaire]] [[马科斯·耶科 Max Jacob]] [[卡恩韦勒 Daniel-Henry Kahnweiler]] [[海明威 Ernest Hemingway]]
  - 10 新作品：含 [[亚威农少女 Les Demoiselles d'Avignon]]（1907；20 世纪艺术最重要转折点）+ [[揭开第五封印 The Opening of the Fifth Seal]]（构图蓝本）+ [[格特鲁德·斯坦因肖像]]（黑人时期试水 / 90 次坐画）
  - 1 新概念 [[黑人时期 African Period (Picasso)]]
  - 顾衡反命题：黑人时期不是"前立体主义"，本质是"打着塞尚旗号画非洲木雕"

## [2026-05-13] merge | batch-062-065 后处理

- 4 个 lecture 并行 ingest → main agent merge
- ✅ 0 路径漂移, 0 wikilink 错位 (refined prompt 持续显效)
- 🆕 100% PENDING dedup 率 (12/12) — agents 重复下载已存图
- 跨 agent race-condition 解决：
  - **戴帽子的女人**: 061 owns, 063+064 PENDING 同 MD5, dedup
  - **亚维农的少女 → 亚威农少女**: 063 用旧拼写, 065 创建 canonical (亚威农少女, 无的); merger 修正 063 共 5 处 wikilink + 1 image path
  - **立体主义/表现主义 stubs**: 062 提前建以解决多课 forward gap; 064/065 仅 wikilink
  - **毕加索 stub → 主页**: 064 创建 main page; 065 仅 reference
- 旧 bug 发现（留 lint）：
  - 蒙娜丽莎/01.jpg == 02.jpg, 03.jpg == 04.jpg byte-identical (pre-existing duplicates)
- Backlog（留 lint）：
  - ~100+ 既有人物/流派/技法/作品页的 `## 出现在` 反向链接
  - 亚维农 vs 亚威农 命名统一（065 canonical 是亚威农, 但标准中文文献多用亚维农）
  - 蒙娜丽莎/01 == 02 + 03 == 04 dup cleanup
  - 立体主义/表现主义 stubs 待 后续 lecture (066+) 完整建

## [2026-05-13] ingest | 066｜毕加索3：什么是分析立体主义？

- 新建：来源(1) 人物(2) 作品(8) 概念(1: 分析立体主义 folder-mode 含玻尔原子模型图)
- 更新：流派/立体主义 (062 stub → 分析/综合阶段框架), 人物/毕加索 (066 出现在)
- 图片：下载 15, 1 真新角度图 (弹曼陀铃 02), 4 PENDING dedup (弹曼陀铃 01 / 伊娃在扶手椅 / 卡恩韦勒 / 亚威农少女), 失败 0
- 备注：本批次 `batch-066-069`; 2 新人物 [[普朗塞 Maurice Princet]]（数学家几何顾问）[[伊娃 Eva Gouel]]

## [2026-05-13] ingest | 067｜毕加索4：什么是综合立体主义？

- 新建：来源(1) 流派(1: 超现实主义) 人物(9) 作品(14) 概念(3)
- 更新：人物/毕加索 (067 出现在); 作品/藤椅上的静物 +02
- 图片：下载 16, 复用 1 course-footer, 失败 0
- 备注：
  - 9 新人物（毕加索一生 4 任妻女 + 配套圈子）：[[佳吉列夫 Sergei Diaghilev]] [[奥尔加 Olga Khokhlova]] [[朵拉·玛尔 Dora Maar]] [[玛丽·泰莱斯 Marie-Thérèse Walter]] [[弗朗索瓦斯·吉洛 Françoise Gilot]] [[杰奎琳·罗克 Jacqueline Roque]] [[佛朗哥 Francisco Franco]] [[罗兰特·潘罗斯 Roland Penrose]] [[斯特拉文斯基 Igor Stravinsky]]
  - 14 新作品（含格尔尼卡 / 哭泣的女人 / 三个音乐家等综合立体主义代表）
  - 3 新概念（删除 dup 后）：[[综合立体主义 Synthetic Cubism]] / [[拼贴 Collage]] / [[俄罗斯芭蕾舞团 Ballets Russes]]
  - ⚠️ 跨 agent dup resolved: 067 创建 分析立体主义 Analytic Cubism + 钢琴课/摩洛哥人 with (Matisse) 后缀 — merger 删除 067 重复版, wikilinks 重指 066/068 canonical

## [2026-05-13] ingest | 068｜立体主义，除了毕加索还值得了解什么？

- 新建：来源(1) 人物(2) 作品(23) 概念(3 after dedup: 俄耳浦斯立体主义 / 同时性绘画 / 管子主义)
- 更新（待 lint）：流派/立体主义 / 人物/勃拉克 / 毕加索 / 马蒂斯（多 agent 共写, 留 lint）; 作品/亚威农少女 +02 (但 MD5 dup of 01, lint cleanup); 作品/鲁昂大教堂系列 +03
- 图片：下载 26, 0 失败
- 备注：
  - 2 新人物：[[莱热 Fernand Léger]]（管子主义）[[德劳内 Robert Delaunay]]（俄耳浦斯）
  - 23 新作品（勃拉克 4 + 毕加索 1 + 马蒂斯 2 含 dedup + 莱热 6 + 德劳内 9 + 法国塞尚 1）
  - ⚠️ 跨 agent dup: 067 创建 钢琴课/摩洛哥人 with (Matisse) suffix vs 068 without — merger keep 068 versions (cleaner), delete 067's dups
  - ⚠️ 跨 agent dup: 067 创建 分析立体主义 Analytic Cubism + 068 单文件 Analytical Cubism vs 066 folder-mode Analytical Cubism — merger keep 066 folder version (richest 117 lines + diagram)

## [2026-05-13] ingest | 069｜什么是表现主义？

- 新建：来源(1) 人物(4) 概念(2)
- 更新：流派/表现主义 (062 stub → full 导论 sanctioned by orchestrator)
- 图片：下载 0, 复用 1 course-footer, 失败 0; 069 是纯思想史课，0 件 artwork
- 备注：
  - 4 新人物：[[歌德 Johann Wolfgang von Goethe]] [[费希特 Johann Gottlieb Fichte]] [[黑格尔 G.W.F. Hegel]] [[爱德华·蒙克 Edvard Munch]]（070 主角预告）
  - 2 新概念：[[新康德主义 Neo-Kantianism]] / [[刺猬与狐狸 Hedgehog and the Fox]]

## [2026-05-13] merge | batch-066-069 后处理

- 4 个 lecture 并行 ingest → main agent merge
- ✅ 0 路径漂移, 0 wikilink 错位
- 跨 agent dup 集中爆发 + 一次性解决：
  - **分析立体主义 (3-way)**: 066 创建 folder-mode (Analytical Cubism, 含图 + 117 行) + 067 创建 .md (Analytic Cubism, 55 行) + 068 创建 .md (Analytical Cubism, 44 行) → merger 删除 067 + 068 单文件, 保留 066 folder
  - **钢琴课 / 摩洛哥人 (马蒂斯)**: 067 用 (Matisse) 后缀, 068 不用 → merger 删除 067 版本, 保留 068; 067 source page 5 处 wikilink 修正
  - **综合立体主义**: 067 + 068 都创建 → 文件系统层只剩一份 (后写者覆盖), no action needed
- PENDING 处理: 5 个 (066) — 1 真新 (弹曼陀铃/02) + 4 dedup
- Backlog（留 lint）：
  - ~100 既有人物/流派/作品页的 `## 出现在` 反向链接
  - 流派/立体主义 大幅扩展（066/067/068 各自补充内容需合并）
  - 人物/毕加索 多课内容合并（066/067/068）
  - 人物/勃拉克 stub → 完整传记（068 提供大量素材）
  - 亚威农少女/02.jpg 与 01.jpg MD5 dup cleanup（pre-existing from 068）
  - 蒙克 stub 待 070 (蒙克专题) 完整建

## [2026-05-13] ingest | 070｜蒙克1：表现主义的先行者经历了什么？

- 新建：来源(1) 人物(5) 作品(15) 概念(5)
- 更新：人物/爱德华·蒙克 (069 stub → 完整传记 91 行), 作品/星月夜 +02 (+ Northern Gothic context)
- 图片：下载 18 (含 1 现有作品 append + 17 新), 失败 0
- 备注：本批次 batch-070-073; 5 新人物含克罗格/威廉二世/易卜生/沃林格/苏菲蒙克; 5 新概念含[[北方哥特风 Northern Gothic]]/[[爱组画 The Frieze of Life]]; 15 新作品 (蒙克 1880s-1890s); [[呐喊]] / [[焦虑]] / [[绝望]] (双版本) 等创立

## [2026-05-13] ingest | 071｜蒙克2：为什么他是表现主义之父？

- 新建：来源(1) 人物(6) 作品(7)
- 更新：作品/呐喊 +02, 焦虑 +02, 日出·印象 +03, 格尔尼卡 +02
- 图片：下载 13, 复用 1 (吸血鬼 070 同 MD5), 失败 0
- 备注：
  - 6 新人物 (蒙克柏林圈子): [[普茨比斯维斯基 Stanisław Przybyszewski]] [[斯特林堡 August Strindberg]] [[达格妮 Dagny Juel]] [[图拉·拉尔森 Tulla Larsen]] [[柯科施卡 Oskar Kokoschka]] [[拉特瑙 Walther Rathenau]]
  - 7 新作品 (含 [[圣母像 Madonna (Munch)]] [[女凶手 The Killer (Munch)]] [[马拉之死 The Death of Marat (Munch)]] disambig)
  - ⚠️ 跨 agent: 呐喊/焦虑/吸血鬼 race-condition with 070, 071 in-agent 已删除 dup 文件夹, 仅追加图

## [2026-05-13] ingest | 072｜桥社：什么是表现主义绘画的使命？

- 新建：来源(1) 流派(1: 桥社 Die Brücke) 人物(4) 作品(14)
- 图片：下载 15 (街景 2 版本), 失败 0
- 备注：
  - 新流派 [[桥社 Die Brücke]] (1905–1913 德累斯顿)
  - 4 新人物: [[基希纳 Ernst Ludwig Kirchner]] [[诺尔德 Emil Nolde]] [[施密特-罗特鲁夫 Karl Schmidt-Rottluff]] [[赫尔曼·巴尔 Hermann Bahr]]
  - 14 作品 (基希纳 6 + 诺尔德 8)

## [2026-05-13] ingest | 073｜克里姆特：什么是维也纳分离派？

- 新建：来源(1) 流派(5: 维也纳分离派+新艺术运动+青年风格+包豪斯+巴黎画派) 人物(3) 作品(13) 概念(1)
- 图片：下载 13 + 1 装饰图 (笛卡尔象限) + footer 复用, 失败 0
- 备注：
  - 5 新流派 (含 4 个相关 stub 解决多课 forward-link gap)
  - 3 新人物: [[克里姆特 Gustav Klimt]] [[惠斯勒 James Whistler]] [[艾米莉·弗洛奇 Emilie Flöge]]
  - 13 作品 (含 [[吻 The Kiss (克里姆特)]] / [[阿黛尔夫人像]] / [[医学]]/[[法学]]/[[哲学]] 维也纳大学三联画)
  - 新概念 [[维也纳工坊 Wiener Werkstätte]]
  - ⚠️ 预告 forward wikilink: [[席勒 Egon Schiele]] in 维也纳分离派 / 克里姆特 / 来源 pages — 074 将创建

## [2026-05-13] merge | batch-070-073 后处理

- 4 个 lecture 并行 ingest → main agent merge
- ✅ 0 路径漂移, 0 wikilink 错位, 0 PENDINGs (071 自行 in-agent 处理 race)
- 跨 agent race-condition 解决：
  - **呐喊 / 焦虑 / 吸血鬼**: 070 + 071 都引用, 071 in-agent 删除 dup 文件夹, 仅 append image
  - **蒙克 page**: 069 stub → 070 EXCEPTION 扩展完整传记 91 行; 071 defer to lint
- Backlog（留 lint）:
  - 蒙克 page 071 内容合并 (柏林时期 / 图拉事件 / 危机后期)
  - 流派/表现主义 持续扩充 (070-072 内容)
  - 流派/桥社 + 流派/维也纳分离派 + 新艺术运动 / 青年风格 / 包豪斯 / 巴黎画派 关系梳理
  - 席勒 Egon Schiele forward wikilink wait for 074

## [2026-05-13] ingest | 074｜席勒1：他为什么走向表现主义？

- 新建：来源(1) 人物(3) 概念(2) 作品(9)
- 更新：人物/弗洛伊德 (与 075/076 并发创建+扩展)
- 图片：下载 9 新作品首图 + 1 PENDING dedup (吻/01 MD5 同 073), 失败 0
- 备注：本批次 batch-074-077; 主角 [[席勒 Egon Schiele]] 严格区分诗人 [[席勒 Friedrich Schiller]]; 2 概念 [[精神分析 Psychoanalysis]] [[神经官能症 Neurosis]] 解释席勒"残缺"画法

## [2026-05-13] ingest | 075｜席勒2：为什么他是"最表现主义"的画家？

- 新建：来源(1) 人物(1: 巴尔蒂斯) 作品(16)
- 更新：人物/席勒 (074 → 075 增补), 人物/弗洛伊德 (并发追加)
- 图片：下载 15 新作品首图, 失败 0
- 备注：16 新作品 (席勒 15 + 巴尔蒂斯 1); 含 [[一家人 (席勒) The Family (Schiele)]] 遗作, [[少女与死神 (席勒)]] 双 Wally + 双 Edith 系列, [[世界的起源 (库尔贝) L'Origine du monde]] 库尔贝 stub

## [2026-05-13] ingest | 076｜表现主义到底要表现什么？

- 新建：来源(1) 人物(8) 概念(4) 作品(1: 风中新娘)
- 更新：流派/表现主义 (069/072 → 076 综合段落); 人物/柯科施卡 (风中新娘 案例); 人物/沃林格 (集中讲述)
- 图片：下载 1 新作品 + 2 PENDING MD5 dedup (星月夜/疯狂跳舞的孩子), 失败 0
- 备注：表现主义板块收束; 8 新人物（叔本华→立普斯→波普尔思想链 + 马勒-艾尔玛-格罗庇乌斯-杰林斯基《风中新娘》情史圈）; 4 新概念建构 Kunstwollen→Worringer 理论闭环

## [2026-05-13] ingest | 077｜夏加尔：俄国人在巴黎

- 新建：来源(1) 人物(2) 作品(9) 概念(2)
- 图片：下载 9 新作品首图, 失败 0
- 备注：[[夏加尔 Marc Chagall]] 俄国-法国巴黎画派; 9 新作品 (含 [[我和我的村庄]] [[飞翔的马车]] [[生日 (夏加尔)]] 等魔幻飞翔母题); 新概念 [[超自然主义 Surnaturalisme]] / [[魔幻现实主义 Magic Realism]]

## [2026-05-13] merge | batch-074-077 后处理

- 4 个 lecture 并行 ingest → main agent merge
- ✅ 0 路径漂移, 0 wikilink 错位
- 跨 agent 协作:
  - **人物/弗洛伊德** 三 agent 并发: 076 创建 stub → 074 替换为完整内容 → 075 追加；最终内容已合并 (sources 列出 074/075/076)
  - **人物/席勒 Egon Schiele** 074 创建 → 075 扩展 (075 在 sources 标 074+075)
- PENDING/dedup 处理: 3 个 (074 吻 + 076 星月夜 + 076 疯狂跳舞) 全部 MD5 dedup
- Backlog（留 lint）:
  - 流派/表现主义 多 lecture 内容继续合并 (069-076)
  - 巴黎画派 stub → 077 内容
  - 弗洛伊德 / 席勒 多版本 sections 合并
  - 星月夜/01==02 dup (070 留下)

## [2026-05-13] ingest | 078｜莫迪里阿尼：画中女子为什么让人一眼难忘？

- 新建：来源(1) 流派(1: 马基亚伊奥利画派) 人物(9) 作品(24) 概念(2)
- 更新（图片层面）：作品/圣母领报 (马丁尼·梅米) +04, 作品/呐喊 +03, 作品/春/圣母像(Munch)/蓬巴杜夫人的肖像 dedup 到 01
- 图片：下载 30, 3 真新角度图 + 3 dedup, 失败 0
- 备注：本批次 batch-078-081; 9 新人物（莫迪里阿尼 + 布朗库西 + 7 配角）; 24 新作品；2 新概念 [[原型 (柏拉图) Archetype]] [[波希米亚风 Bohemian Style]]; 作品 disambig (毕加索)/(莫迪里阿尼)/(达·芬奇) 解决多重同名

## [2026-05-13] ingest | 079｜亨利·卢梭：毕加索对他的吹捧是真心的吗？

- 新建：来源(1) 人物(1: 亨利·卢梭) 作品(5) 概念(4)
- 图片：下载 5, 失败 0; 1 uncaptioned 清理
- 备注：[[亨利·卢梭 Henri Rousseau]] 画家 disambig from [[卢梭 Jean-Jacques Rousseau]] 哲学家; 4 新概念 [[原始主义 Primitivism]] / [[卢梭之夜 Rousseau Banquet]] / [[偏爱原始性 The Preference for the Primitive]] / [[欧洲黄金年代 Belle Époque]]

## [2026-05-13] ingest | 080｜什么是未来主义？

- 新建：来源(1) 流派(1: 未来主义) 人物(3) 作品(10)
- 更新（图片层面）：作品/纳税银 +02 (真新), 作品/沃拉尔肖像 dedup 到 01
- 图片：下载 10 新作品首图 + 2 PENDING (1 真新 + 1 dedup), 失败 0
- 备注：新流派 [[未来主义 Futurism]]——1909 马里内蒂宣言; 3 新人物 [[马里内蒂]] [[波丘尼]] [[巴拉]]; 10 作品含杜尚《下楼梯的裸女》

## [2026-05-13] ingest | 081｜康定斯基1：什么是抽象绘画？

- 新建：来源(1) 流派(2: 青骑士 + 抽象绘画) 人物(9) 作品(6) 概念(2)
- 更新（图片层面）：4 PENDING 全部 MD5 dedup (亚威农少女/小提琴(毕加索 1910)/音乐(马蒂斯)/舞蹈(马蒂斯))
- 图片：下载 11, 4 dedup, 失败 0
- 备注：
  - 新流派 [[青骑士 Der Blaue Reiter]] + [[抽象绘画 Abstract Painting]]
  - 9 新人物含 [[康定斯基 Wassily Kandinsky]] [[库普卡 František Kupka]] [[马尔克 Franz Marc]] [[马克 August Macke]] [[克利 Paul Klee]] 等青骑士全班 + [[瓦格纳 Richard Wagner]] (音乐影响)
  - 6 新作品含 [[多个圆 Several Circles]] 抽象画代表 + [[蓝色的马一号 Blue Horse I]] (马尔克 1911)
  - 2 新概念 [[反具象 Non-Representational]] / [[三根线 (绘画道统) Three Strings]]

## [2026-05-13] merge | batch-078-081 后处理

- 4 个 lecture 并行 ingest → main agent merge
- ✅ 0 路径漂移, 0 wikilink 错位
- PENDING 处理: 11 个 existing-artwork clippings (5 dedup + 3 真新 + 3 uncaptioned/closing)
- 跨 agent 协作: 大量既有作品引用通过 wikilink 解决, 0 重大冲突
- Backlog（留 lint）:
  - 各既有人物/流派/作品页的 `## 出现在` 反向链接
  - 流派/巴黎画派 stub → 077-079 内容
  - 勃拉克 Georges Braque 页面是否已存在 (081 标识 gap)
  - 081 提及的 080 杜尚《下楼梯的裸女》是否与未来主义/立体主义存在归类争议

## [2026-05-13] ingest | 082｜康定斯基2：他为什么走向抽象？

- 新建：来源(1) 人物(1: 威尔·贡培兹) 作品(14) 概念(2: 总体艺术/论艺术的精神)
- 更新：人物/康定斯基 (081 → 082 走向抽象过程 + 实践/理论双重不彻底论 + 三大影响源)
- 图片：下载 14 新作品首图, 1 真新角度图 (干草垛系列/04), 失败 0
- 备注：本批次 batch-082-085; 康定斯基 1909–1936 14 件作品 (即兴/构图/抒情诗 等); 瓦格纳总体艺术 + 论艺术的精神 (1911 著作)

## [2026-05-13] ingest | 083｜马列维奇：什么是至上主义？

- 新建：来源(1) 流派(3: 至上主义+巡回画派+辐射主义) 人物(5) 作品(18) 概念(4)
- 图片：下载 19, 3 PENDING dedup (绿线/下楼梯的裸女/第一盘均 MD5 同既有 01.jpg), 失败 0
- 备注：
  - 主创建 [[至上主义 Suprematism]]——抽象画逻辑终点
  - 5 新人物 ([[马列维奇 Kazimir Malevich]] + [[列宾 Ilya Repin]]《伏尔加纤夫》+ [[施希金 Ivan Shishkin]] + [[冈察洛娃 Natalia Goncharova]] + [[莫洛索夫 Ivan Morozov]] 收藏家)
  - 18 新作品 (马列维奇全生涯 + 列宾 + 施希金 + 冈察洛娃)
  - 4 新概念: [[征服太阳 Victory over the Sun]] (黑方块源头) / [[斯托雷平改革]] / [[驴尾社 Donkey's Tail]] / [[至上主义绘画宣言]]
  - ⚠️ 跨 agent 命名冲突: 084 引 黑方块/红方块 with `(马列维奇 1915)` suffix; merger 改为 083 canonical `黑方块 Black Square` / `红色方块 Red Square (Malevich)`

## [2026-05-13] ingest | 084｜蒙德里安：他为什么要画那么多格子？

- 新建：来源(1) 流派(2: 风格派+新造型主义) 人物(3) 作品(9) 概念(1: 神智学)
- 更新（图片层面）：作品/多个圆 +02 (真新)
- 图片：下载 9 新作品 + 2 PENDING (1 真新 多个圆/02 + 黑方块/红色方块 MD5 dedup), 失败 0
- 备注：
  - 2 新流派 [[风格派 De Stijl]] + [[新造型主义 Neo-Plasticism]] (同指一物)
  - [[蒙德里安 Piet Mondrian]] + [[杜斯堡 Theo van Doesburg]] + [[布拉瓦茨卡娅 Helena Blavatsky]] (神智学创立)
  - 9 作品 (含 [[百老汇的爵士乐 (蒙德里安) Broadway Boogie Woogie]] 1942-43 + 红树→灰树→构图三 系列)
  - 1 新概念 [[神智学 Theosophy]] (抽象画三人组思想背景)
  - ⚠️ 跨 agent 命名修正: 黑方块/红色方块 wikilinks 改用 083 canonical (无 (马列维奇 1915) suffix)

## [2026-05-13] ingest | 085｜克利：他为什么模仿小孩子画画？

- 新建：来源(1) 人物(3: 赫伯特·里德/老子/勋伯格) 作品(13) 概念(3: 婴儿视角/自动写作/颓废艺术)
- 更新：人物/克利 (081 stub → 完整 + 方法-vs-康定斯基对照表 + 13 代表作品)
- 图片：下载 14, 失败 0; 1 uncaptioned 清理
- 备注：13 作品 (克利 12 + 马克《树下的女孩》《永别》+ 马尔克《战争中的形》)

## [2026-05-13] merge | batch-082-085 后处理

- 4 个 lecture 并行 ingest → main agent merge
- ✅ 0 路径漂移
- PENDING 处理: 9 个 — 2 真新 (干草垛系列/04 + 多个圆/02) + 5 dedup + 2 uncaptioned cleanup
- 跨 agent 命名冲突解决:
  - **黑方块/红方块**: 083 创建 `黑方块 Black Square` / `红色方块 Red Square (Malevich)`; 084 用了 `(马列维奇 1915)` suffix → merger rename 084's wikilinks 共 8 处
- Backlog（留 lint）:
  - 各既有人物/流派/作品页的 `## 出现在` 反向链接
  - 080 杜尚《下楼梯的裸女》是未来主义还是立体主义 (083 引用)
  - 抽象绘画 流派页 整合 081/082/083/084/085 内容

## [2026-05-13] ingest | 086｜塔特林：什么是构成主义？

- 新建：来源(1) 流派(1: 构成主义) 人物(3: 塔特林/利西茨基/罗琴科) 作品(6) 概念(3)
- 图片：下载 9, 2 PENDING dedup (收割者/黑方块), 失败 0
- 备注：本批次 batch-086-089; 构成主义流派 + 反浮雕/生产主义概念; 塔特林塔设计稿

## [2026-05-13] ingest | 087｜什么是达达主义？

- 新建：来源(1) 流派(1: 达达主义) 人物(4) 作品(1) 概念(2: 伏尔泰酒吧/达达主义宣言)
- 图片：下载 1 新作品 + 1 closing 清理, 失败 0
- 备注：1916 苏黎世起源; 雨果·鲍尔/查拉/胡森贝克/让·阿尔普 (反艺术核心圈)

## [2026-05-13] ingest | 088｜杜尚1：他"好好画画"是什么样子的？

- 新建：来源(1) 流派(1: 皮托集团) 人物(4) 作品(14) 概念(1: X 射线)
- 更新：人物/杜尚 (008 stub → 完整传记 sources 2→3)
- 图片：下载 14 新作品首图 + 2 真新角度图 (下楼梯的裸女/02 + 被拴住的狗的动态/02), 失败 0
- 备注：杜尚早期"好好画画"期 (1902-1911); 4 人物 (杜尚兄弟+尼科尔+邓肯)

## [2026-05-13] ingest | 089｜杜尚2：什么是他人生的转折点？

- 新建：来源(1) 人物(1: 雅里) 作品(4) 概念(2: 啪嗒学/Apollonian)
- 更新：人物/杜尚 (088 → 089 转折点)
- 图片：下载 4 新作品首图 + 1 真新角度图 (从处女到已婚妇女/02), 失败 0
- 备注：杜尚 1912 慕尼黑转折期 (作品被皮托集团劝退 → 解构路线); 4 作品 (新娘/被撕成碎片的伊芳/杜尔西尼亚等)

## [2026-05-13] merge | batch-086-089 后处理

- 4 个 lecture 并行 ingest → main agent merge
- ✅ 0 路径漂移, 0 wikilink 错位
- PENDING + 真新图片处理:
  - 086: 2 PENDING (收割者/黑方块) — 全部 MD5 dedup
  - 088: 2 PENDING (下楼梯的裸女 + 被拴住的狗的动态) — 2 真新角度图 → 02.jpg
  - 089: 4 PENDING (下楼梯 ×2 + 被拴住 + 从处女到已婚) — 3 与 088 同 MD5 dedup, 1 真新 (从处女到已婚/02)
- 跨 agent 协作:
  - **杜尚 page 3-way write**: 008 stub → 088 EXCEPTION 扩展 → 089 EXCEPTION 进一步扩展 (sources 1→2→3)
  - **皮托集团**: 088 owns; 089 references via wikilink
  - **下楼梯的裸女 02**: 088 + 089 同时引同一URL/MD5 → 单一文件, 两 source 共享路径
- Backlog（留 lint）:
  - ~30 既有人物/流派/作品页 `## 出现在` 反向链接
  - 流派/超现实主义 完整建（087 引用，待 092）
  - 杜尚 stub vs canonical 进一步整理

## [2026-05-13] ingest | 090｜杜尚3：他为什么要送一个小便器去参展？

- 新建：来源(1) 作品(5: 巧克力研磨机/三个标准的终止/自行车轮/瓶架/提前断臂) 概念(7)
- 更新：人物/杜尚 (089 → 090 反艺术阶段); 作品/泉 (杜尚) (stub → full)
- 图片：下载 6 新作品 + 4 PENDING dedup, 失败 0
- 备注：本批次 batch-090-093; 7 新概念含 [[现成品 Readymade]] 立体主义之后的核心革命 + 军械库展/独立艺术家协会展; ⚠️ 090 创建 大玻璃 (大玻璃) suffix dup 文件夹, 091 owns canonical, merger 删除 090 dup

## [2026-05-13] ingest | 091｜毕卡比亚：如何用绘画表现达达主义？

- 新建：来源(1) 流派(1: 毕卡比亚画派) 人物(1: 毕卡比亚) 作品(23)
- 图片：下载 23 新作品 + 4 PENDING dedup (穿黑丝袜/下楼梯/第一盘/从处女到已婚), 失败 0
- 备注：23 作品 (毕卡比亚 22 + 杜尚大玻璃 1); 创建 [[新娘甚至被单身汉剥光了衣服 The Bride Stripped Bare by Her Bachelors]] = 杜尚大玻璃

## [2026-05-13] ingest | 092｜超现实主义为什么会诞生？

- 新建：来源(1) 作品(3: 乌比王/恋人/记忆的永恒) 概念(4)
- 更新（待 lint）：流派/超现实主义 (067 stub → 092 诞生导论 待 lint)
- 图片：下载 7 新作品 + 4 PENDING dedup (美惠三女神/三个浴女/百老汇/泉杜尚), 失败 0
- 备注：4 新概念 [[第一次超现实主义宣言]] / [[无意识 Unconscious]] / [[巫师与祭司之战]] / [[词语联想法则 Word Association]]; ⚠️ 与 093 race: 词语联想法则 命名冲突, 092 命名 canonical (Word Association), merger 删 093 dup (Word-Association Rules)

## [2026-05-13] ingest | 093｜契里柯与恩斯特：如何用绘画表现超现实主义？

- 新建：来源(1) 流派(1: 形而上画派) 人物(5) 技法(2) 作品(14)
- 图片：下载 14 新作品 + 1 真新角度图 (乌比王/02 — 与 092 同作品不同图), 失败 0
- 备注：
  - 新流派 [[形而上画派 Metaphysical Painting]] (契里柯创立, 超现实直接前身)
  - 5 新人物: [[契里柯 Giorgio de Chirico]] [[恩斯特 Max Ernst]] [[布勒东 André Breton]] [[艾吕雅 Paul Éluard]] [[洛特雷阿蒙 Comte de Lautréamont]]
  - 2 新技法: [[摩擦法 Frottage]] / [[拓印法 Decalcomania]]
  - 14 作品 (契里柯 3 + 恩斯特 11)
  - ⚠️ 跨 agent: 词语联想法则 命名 dedup; 布勒东 race-condition (087/092/093 三方期望创建, 093 实际写入)

## [2026-05-13] merge | batch-090-093 后处理

- 4 个 lecture 并行 ingest → main agent merge
- ✅ 0 路径漂移 (091 用了 `PENDING-EXISTING-...` 自定义占位符, 已 merger 改回 vault path)
- PENDING + 真新图片处理:
  - 090: 4 PENDING 全 dedup (下楼梯/国王王后/L.H.O.O.Q./泉杜尚)
  - 091: 4 PENDING 全 dedup (穿黑丝袜/下楼梯/第一盘/从处女到已婚)
  - 092: 4 PENDING 全 dedup (美惠三女神/三个浴女/百老汇/泉杜尚)
  - 093: 1 真新 (乌比王/02 — 与 092 同作品不同图), 已 move
- 跨 agent 重大 race-condition 解决:
  - **大玻璃 (杜尚)**: 090 创建 `新娘甚至被单身汉剥光了衣服 (大玻璃)... Even` 后缀; 091 创建 canonical `新娘甚至被单身汉剥光了衣服 The Bride Stripped Bare by Her Bachelors`; merger 删除 090 dup folder
  - **词语联想法则**: 092 创建 `Word Association`; 093 创建 `Word-Association Rules`; merger 删除 093 dup, 093 wikilinks 重指 092 canonical
  - **乌比王 (恩斯特)**: 092 创建 + 01.jpg (MD5 3f4643c); 093 不同 URL → 不同图; merger move 093 → 02.jpg
  - **布勒东 André Breton**: 087/092/093 三方期望创建; 实际 093 写入了 (092 撞期间检测到已存在)
- Backlog（留 lint）:
  - ~30 既有人物/流派/作品页 `## 出现在` 反向链接
  - 流派/超现实主义 092 内容合并 (诞生导论)
  - 布勒东 page 待 092 补充 (化解达达悖论 + 托洛茨基迷弟 + 阿波利奈尔词源)
  - 美惠三女神 01==02 byte-identical (pre-existing 030 留下) dup cleanup
  - 大玻璃 dup folder rmdir (sandbox 拒绝, 留空文件夹)

## [2026-05-13] ingest | 094-097 (batch, 4 lectures)

- 094 达利: +2 人物 (加拉, 布纽尔) + 10 作品 + 1 概念 (一条安达鲁狗); extended 达利 stub
- 095 当代艺术导论: +1 时代 (当代) + 1 人物 (玛丽·卡萨特) + 2 作品 + 2 概念 (MoMA, 联邦艺术计划)
- 096 波洛克: +1 流派 (抽象表现主义) + 6 人物 + 1 技法 (滴画法) + 11 作品 + 3 概念 (集体无意识/本世纪画廊/当代艺术)
- 097 德·库宁: +2 人物 + 6 作品

- 跨 agent race 解决:
  - **WPA**: 095 详细版 (联邦艺术计划) vs 096 短版 (WPA.md) → merger 删 096 dup
  - **秋韵**: 096 创建空 folder `秋韵 (波洛克) Autumn Rhythm No. 30` + 实际内容在 `秋韵 Autumn Rhythm` → merger keep latter, 097 wikilink 重指
  - **4 Pollock missing artworks**: 097 引用 4 个 Pollock 作品但 096 仅创建 11 个; merger 创建 [[薰衣草雾气]] / [[黑与白(20号)]] / [[海神的召唤]] / [[七号(网络之外)]] stubs + move 097 clippings 落地

- Backlog (lint):
  - 秋韵 命名一致性
  - 4 merger-created Pollock stubs 待充实
  - ~30 既有页 `## 出现在` 反向链接

## [2026-05-13] ingest | 098–100 (FINAL batch, 3 lectures)

- 098 波普艺术: +1 流派 (波普艺术) + 7 人物 (沃霍尔/利希滕斯坦/劳森伯格/约翰斯/汉密尔顿/鲍德里亚/王尔德) + 1 技法 (丝网印刷) + 11 作品 + 2 概念 (拟真/机械复制时代)
- 099 大便罐头到NFT: +4 人物 (曼佐尼/卡特兰/Beeple/库布勒) + 3 作品 (艺术家的粪便/丑角/希阿岛屠杀) + 4 概念 (NFT/幂律/布雷顿森林/先锋性=平面性); +1 真新角度图 (吉内薇拉/02)
- 100 结语: +5 人物 (约瑟夫·赖特/老普林尼/柏拉图/弗雷泽/特蕾西·艾敏) + 2 作品 (科林斯少女/公牛走廊拉斯科) + 8 概念 (交感巫术/金枝/洞穴寓言/灵韵/机械复制时代/判断力批判/当代艺术之争/画出来的箴言)

## [2026-05-13] 全部 100 讲 ingest 完成 🎉

- 课程：[[顾衡·西方美术100讲]] sources 1→101 (发刊词 + 001-100 = 101 来源页)
- 18 轮 batch (034-037 → 098-100); 每 batch 3-4 parallel agents + main agent merge
- 总体 wiki 统计 (粗估): ~30 流派 / 5 时代 / ~250 人物 / ~28 技法 / ~600 作品 / ~120 概念 / 101 来源
- 待 lint 处理：~200+ 既有页 `## 出现在` 反向链接、若干 stub 待充实、若干 dup 命名待统一
- 此次大规模批量是用户预授权的 batch-unattended 模式 (memory feedback_batch_unattended.md)，跳过 per-file Step 4 Checkpoint

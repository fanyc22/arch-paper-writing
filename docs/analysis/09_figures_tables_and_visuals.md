# 维度 9：计算机体系结构顶会论文的绘图、表格与视觉设计深度分析

> **研究范围与方法论声明**
> - **阶段 A（像素级视觉精审）**：基于 `corpus/manifest.json` 指定的全部 **20 篇公开 OA 论文**（`visual_oa_ids`：14 篇获奖/权威标杆 `exemplar` + 3 篇普通录用对比 `contrast_ordinary` + 3 篇 2023 年后对比 `contrast_post2023`，横跨 2012–2026 年 ISCA / MICRO / HPCA / ASPLOS），通过 `scripts/render_oa_pdfs.py` 全部成功下载并渲染 **118 张 150 DPI PNG 页面**（20/20 成功率），人工逐页视觉审查其中 **92 张核心图文页**（覆盖全部 20 篇，每篇精审 4–6 页：首页/Teaser、微架构框图/演进图、实验结果图与表格）。
> - **阶段 B（全样本图注、预算与图文耦合量化分析）**：基于 `corpus/macro_cache/` 全部 **48 篇 `deep_read` 论文**（提取 **671/686 个图注 [97.8% 召回]** 与 **164/167 个表注 [98.2% 召回]**，并用 20 篇 OA PDF 的 PyMuPDF 精确排版块提取 **261 个图注与 63 个表注**作词数真值校验），同时用 152 篇 `macro_pool` 交叉验证图表预算的年代/会议稳定性。全程严格隔离 `held_out_test`（零读取、零引用）。
> - **批判原则**：既提炼标杆论文的视觉工艺，也毫不留情地指出**最佳论文/Top Picks 中的真实视觉瑕疵**，并与普通论文、近年论文的典型退化做对照。本文聚焦视觉设计、排版与图注原则，不提供任何绘图脚本。

---

## 目录

1. [阶段 A：20 篇 OA 论文（92 页 PNG）像素级视觉设计剖析](#1-阶段-a20-篇-oa-论文92-页-png像素级视觉设计剖析)
   - [1.1 全部 20 篇视觉样本清单与总评索引](#11-全部-20-篇视觉样本清单与总评索引)
   - [1.2 色彩体系、语义一致性与黑白打印安全](#12-色彩体系语义一致性与黑白打印安全)
   - [1.3 字体、字号、比例尺与零重叠纪律](#13-字体字号比例尺与零重叠纪律)
   - [1.4 微架构框图、机制演进图与真实工程证据语法](#14-微架构框图机制演进图与真实工程证据语法)
   - [1.5 实验图表人体工学：选型、标注、截断诚实性与反模式](#15-实验图表人体工学选型标注截断诚实性与反模式)
   - [1.6 表格视觉工艺：Booktabs、层级对齐与信息密度](#16-表格视觉工艺booktabs层级对齐与信息密度)
   - [1.7 15 年视觉演化轨迹（2011–2015 vs 2016–2022 vs 2023–2026）](#17-15-年视觉演化轨迹20112015-vs-20162022-vs-20232026)
2. [阶段 B：48 篇 `deep_read` 论文的图表预算、图注解剖与图文耦合](#2-阶段-b48-篇-deep_read-论文的图表预算图注解剖与图文耦合)
   - [2.1 图表数量预算（按会议、年代、分层与章节分布）](#21-图表数量预算按会议年代分层与章节分布)
   - [2.2 规范图表分类体系与 Figure 1 定位策略](#22-规范图表分类体系与-figure-1-定位策略)
   - [2.3 Caption 解剖学：词数分布、结论前置与 15 年演化](#23-caption-解剖学词数分布结论前置与-15-年演化)
   - [2.4 图文耦合机制：引入动词、编号同步与“趋势综合 vs 念柱子”](#24-图文耦合机制引入动词编号同步与趋势综合-vs-念柱子)
   - [2.5 Table vs Figure vs Prose 决策边界](#25-table-vs-figure-vs-prose-决策边界)
3. [面向 Phase 2 Skill 蒸馏的可执行视觉设计准则与提交前核查清单](#3-面向-phase-2-skill-蒸馏的可执行视觉设计准则与提交前核查清单)

---

## 1. 阶段 A：20 篇 OA 论文（92 页 PNG）像素级视觉设计剖析

### 1.1 全部 20 篇视觉样本清单与总评索引

下表汇总全部 20 篇公开 OA 论文的视觉审查记录（每篇列出已人工审阅的代表性 PNG 链接、核心亮点与**必须指出的真实缺陷**）：

| # | `paper_id` | 会议/年份 | 分层 | 已审核心 PNG 页 | 突出视觉亮点 | 发现的真实视觉缺陷（含获奖论文） |
|---|---|---|---|---|---|---|
| 1 | `conf__isca__KimSLLM12` (SALP) | ISCA 2012 | `exemplar` | p3, p4, p5, p6, p10, p11 | 100% 纯灰度印刷安全；正文内嵌黑底白字圆圈编号 `❶→❺` 与图严格同步（Fig 4/7）；升序排序柱状图（Fig 13）；教科书级 booktabs 表（Table 1） | Fig 15（p11）2×2 子图**重复 4 遍相同图例**挤占 45% 宽度；Fig 13/14/15/17 用 4–5 阶相近灰度且**无纹理（hatch）**；Fig 13 的 `gmean` 未与个体测试集分隔 |
| 2 | `conf__isca__KimDKFLLWLM14` (RowHammer) | ISCA 2014 | `exemplar` | p2, p3, p7, p8, p10, p11 | 全文 6 图（Fig 4–9）三组模组**色彩+形状双冗余锁定**（藏青圆/砖红方/灰绿菱）；实心/空心叠加双变量（Fig 6）；左右对齐汇编对比（Code 1）；问句式图注（Fig 7–9）；极简 booktabs 表（Table 1/4/5/6/7） | Fig 4/5/6/7 纵轴在 `10^0` 下方直接拼 `0` 刻度但无断轴标记 `//`；Fig 2 中 `Chip0/Chip7` 竖排文字略微贴边 |
| 3 | `conf__isca__ChenES16` (Eyeriss) | ISCA 2016 | `exemplar` | p2, p3, p5, p8, p11 | 单强调色（红）点亮灰度数据流对比（Fig 3）；真实 65nm 流片 Die Photo + 规格简表（Fig 4）；经典 2 行能耗层级表（Table IV：`200× / 6× / 2× / 1×`）；Fig 12 图注尾句直给结论 | Table I/III/IV 采用陈旧全边框网格线；Fig 11/12（p11）每幅子图**重复 3 遍相同 5 项图例**；Fig 11 三子图纵轴上限不一致（`0.025 / 0.03 / 0.015`）；Fig 12 四图并排导致 5 阶纯灰堆叠柱极细难辨 |
| 4 | `conf__isca__KarandikarMKBAL18` (FireSim) | ISCA 2018 | `exemplar` | p3, p7, p9, p11 | 逻辑拓扑→物理宿主机映射双图配对（Fig 1+2）；3D 叠层优雅压缩 1024 节点拓扑（Fig 10）；线型+灰度+点型三冗余折线图（Fig 5/8/9） | Table I/II/III 全竖线格子笼；Fig 11（p11）短数字横轴 `75.0 / 50.0 / 25.0` 强行竖排 90° 且降序、粗交叉阴影产生视觉摩尔纹且柱内出现白缝；正文 p11 误将 Fig 11 写成 `"Figure VI"` |
| 5 | `conf__isca__BeraRRMNGOKSSM24` (Constable) | ISCA 2024 | `exemplar` | p3, p6, p9, p11, p12 | SAFARI 实验室 12 年进化典范：Fig 8 三路径色彩+实虚线+编号分离（黑查/蓝学/红虚线失效）；Fig 10 全宽分镜 `(A)→(G)` 实时标红表项变更；Fig 11/13/14/16 灰底 `GEOMEAN` 区+直标精确数值+跨图色调锁定；Fig 12 红绿底纹分区+直标异常测试集 | Fig 11/13/14 纵轴从 `1.00` 截断放大视觉差异；Fig 2 周期刻度（`1..19`）与 Fig 12 单栏 90 点折线内标注字号过小（~4.5pt）；p11 第 9.1.1 节正文将 Fig 11 误引为 `"Fig. 14"` |
| 6 | `conf__micro__JeffreySYES15` (Swarm) | MICRO 2015 | `exemplar` | p2, p5, p9, p10 | **全场视觉综合标杆**：Fig 1 代码-图-依赖-并行调度四联跨图色彩联动；低饱和度高级配色（灰蓝/陶橙/橄榄绿）；全宽 6 面板小倍数共享纵轴+右侧单图例（Fig 12）；超线性出界曲线优雅直标 `122×/117×`（Fig 11/12）；结论前置粗体图注；完美 booktabs 表（Table 3/4） | Fig 12 使用绿（实线）vs 红（虚线）存在轻微红绿色盲对，但被实/虚线型冗余有效补救 |
| 7 | `conf__micro__YanCS0FT18` (InvisiSpec) | MICRO 2018 | `exemplar` | p1, p5, p8, p11 | 首页紧凑“左代码+右图注”并排（Fig 1）；极简安全侧信道尖峰直标 `Secret value is 84.`（Fig 5）；清爽单栏时间线（Fig 2） | Fig 4（p11）**横轴标签 `libquantum` 直接与下方图注文字重叠碰撞**、`Average` 未分隔、5 阶灰度含极扁斜线极难区分；Table III 粗双横线+全竖线网格且表头强行断词 `Comple-xity?` |
| 8 | `conf__micro__XuW0CLZW25` (LLM.265 / 预印本 VcLLM) | MICRO 2025 | `exemplar` | p1, p4, p5, p7, p10 | 首页右栏覆盖范围对比 Teaser 色彩精确联动（Fig 1）；H.265 流水线+逐级消融瀑布图直击负收益 `+0.5 bit / Not Working!`（Fig 2）；DCT 异常值平滑数值热图（Fig 3）；真实等比例芯片面积对比+EDA 布局图（Fig 9） | **矢量图与图注多处拼写错误**（Fig 2 `"Armortize"`, `"Explot"`；Fig 9 `"Comparision"`；Fig 5 `"bid-width"`；Fig 6 `"pipline"`）；Fig 5/6 红色虚线基线**缺失于图例**；Fig 6 右子图纵轴从 ~55 截断；Fig 4(b) 红字叠深蓝背景对比度极低 |
| 9 | `conf__hpca__ZhangBES14` (PVCoherence) | HPCA 2014 | `exemplar` | p3, p6, p9, p11 | 整页协议规范差异对照表仅加粗变动条款（Table 1）；Fig 6–8 全文统一“深红实心 vs 蓝斜纹”+误差棒+诚实零点基线 | Fig 2 PowerPoint 默认云朵+刺眼亮黄圆；Fig 5 黑框直贴图注无留白；Fig 6/7/8 原生 Excel 默认图表（Calibri 与 Times 冲突、**连续三图重复相同图例**、Fig 6 与 Fig 7 宽度不一） |
| 10 | `conf__hpca__QinSKNS0KK20` (SIGMA) | HPCA 2020 | `exemplar` | p3, p6, p10, p11 | Fig 5 极详尽 7 步 `(i)→(vii)` 实例推演（具体矩阵元素贯穿位图→Benes→多播）；Table II 清爽 booktabs 指标表 | **获奖论文中最典型的反面教材集合**：Fig 2 使用**饼图**且小切片标签碰撞；Fig 3b/10/11/12/13/14 全是**默认 Excel 双轴柱线混叠**且**用连续折线连接离散矩阵类别**；Fig 12(b) 纵轴拼错 `"Efficiecny"`；Fig 5 开关子图字号 ~3.5pt 不可读；p10 节标题 `VI. EVALUATION` 与正文上下碰撞 |
| 11 | `conf__hpca__WooSN23` (SRS) | HPCA 2023 | `exemplar` | p1, p4, p7, p10, p11 | 教科书级首页双目标 Teaser（Fig 1 红柱/绿箭直标 `GOAL`）；层次化编号 `❶→1.1→1.4` 同步正文与 4 帧状态演进图（Fig 8）；橙阶 vs 灰阶双家族明度渐变（Fig 4/15/16）；Fig 14 红虚线清晰隔离 `GMEAN` 区+双括号标注 | Fig 4/14/15/16 均截断纵轴（`0.70/0.80/0.90` 起）；Fig 14 矢量标注拼错 `"atleast"`；Table III/IV/V 全竖线格子笼且 Table IV 单位空格不一致（`35 KB` vs `9.4KB`） |
| 12 | `conf__asplos__FerdmanAKVAJKPAF12` (CloudSuite) | ASPLOS 2012 | `exemplar` | p3, p5, p7, p9 | 极简纯灰度+斜纹设计；全文统一留白沟壑分隔“Scale-out（左）vs 传统负载（右）”；Fig 3 清晰给出组内极值范围须（Range bars）并写明于图注；诚实零点基线 | Table 1 全网格居中排版；Fig 1 纵轴拼错 `"Total exeution cycles"` 且相邻并置堆叠柱+重叠 `Memory` 柱需读正文方解 |
| 13 | `conf__asplos__SkarlatosKXT20` (Elastic Cuckoo) | ASPLOS 2020 | `exemplar` | p4, p5, p11, p13 | 极简算法演进图仅用单一红色斜线标示 `Migrated Region`（Fig 5/6）；Fig 16 延迟直方图顶部标出存储层级区间（`Cache Hit / 1st–3rd DRAM`）直观揭示长尾消除 | Fig 15（p13）**三连重复图例** + 4 阶无纹理近色灰柱（`Baseline 4KB` 与 `Cuckoo 4KB` 几乎同灰）+ 截断纵轴；Fig 4 缺 `(a)(b)` 标号但正文引用 `Figure 4(a)/(b)`；Table 2 面积漏写平方 `1.9*10^-3 mm` |
| 14 | `conf__asplos__LiBHEZNSRLAHFB23` (Pond) | ASPLOS 2023 | `exemplar` | p4, p5, p6, p7, p12, p13 | **2023+ 现代数据可视化最高标杆**：曲线直标取代远距图例（Fig 8/18/21）；直接标出 `-36% ↓` 与缺失/离群诚实说明框（Fig 4/5/8）；逐跳延迟预算框图+内嵌假设简表（Fig 7）；真实 Linux `numactl` 终端截图（Fig 10）；`粗体标题 + (§X.Y) 章节回链 + 斜体结论` 图注范式 | **同页严重色彩反转失误**：Fig 4/5/21 中红=`222% (255ns)`、蓝=`182% (142ns)`，但**同一页（p13）左侧 Fig 20 竟反转为蓝=`222%`、红=`182%`**；Fig 9 浅灰标注字对比度过低；Fig 21 纵轴从 85% 无断轴截断 |
| 15 | `conf__micro__ZengKLJ21` (Turnpike) | MICRO 2021 | `contrast_ordinary` | p3, p5, p10, p11 | Fig 9/10 编译器基本块内用红删除线标示被消除的 checkpoint 较直观 | **图表膨胀与微观拥挤反面教材（13 页塞 26 图）**：p3 单栏硬塞 Fig 3+Fig 4 导致图注左右相撞；`wrapfigure` 配业余 STOP/GO 路牌挤压出窄列正文；Fig 21–26 反复塞入 42 测试集微缩彩条（Fig 23–26 在单栏挤 42 根 4pt 竖字条形码，Fig 24 图例压在亮黄柱上）；Table 1 网格笼且小数位数混乱（5 位小数 `0.43099`） |
| 16 | `conf__hpca__LazoRMBVSCUC22` (AVA) | HPCA 2022 | `contrast_ordinary` | p4, p7, p9, p12 | Fig 1 绿色高亮新增微架构模块+正文编号联动；Fig 5 真实 22nm PnR 版图等比例展示 53% 面积缩减 | **全场最极端“图表墙”灾难（Fig 3, p9）**：单张图硬塞 **6×4=24 个子图**，重复 `24×15=360` 个 4pt 竖排横轴标签、第 3 列双轴缺图例、无任何汇总均值图；Fig 1 编号 `❹` 误标两处；Fig 2 寄存器表刺眼彩虹色 |
| 17 | `conf__asplos__MiaoJPML19` (StreamBox-HBM) | ASPLOS 2019 | `contrast_ordinary` | p3, p5, p11, p12 | **高阶技巧**：Fig 10（p12）在数据折线图上直接标出圆圈步序 `①–⑦` 与正文联动讲解；Table 1 紧凑斜表头+圆点能力矩阵 | Fig 8（p11）3×3 双轴图使用刺眼纯黄柱、9 次重复全部坐标轴标题导致列间 `HBM BW Use GB/s` 与 `Throughput MRec/s` 贴脸碰撞、且无图例；Fig 9 图例文字撞入纵轴 `30` 刻度 |
| 18 | `conf__micro__ChenTTLZQ25` ($\rho$Hammer) | MICRO 2025 | `contrast_post2023` | p3, p5, p8, p11 | 感知均匀 `viridis` 色图呈现 2D 密度与 32×32 地址异或热图（Fig 3/4）；青/橙语义配色统一；Table 1/2 清爽淡灰斑马纹 booktabs；Fig 11 内嵌量化汇总框 | Table 6（p11）“糖果彩虹”四色斑马底纹（粉/青/紫/桃）喧宾夺主且大数无千分位；Fig 8（p8）**左右双纵轴全部缺失轴标题与单位**、柱顶数值 `224/170` 重叠；Fig 11 横轴 `60` 与右图 `0` 相碰 |
| 19 | `conf__hpca__HuZ00GH00GL25` (M-ANT) | HPCA 2025 | `contrast_post2023` | p3, p5, p6, p9, p12 | Fig 4 柔和粉彩+纹理+对勾/问号直观对比 K vs V 实时量化难点；Fig 13/14 色彩+纹理双编码 | Fig 15（p12）**16 色彩虹堆叠柱状图**彻底不可辨识；Fig 13 横轴 8 次拼错 `"Bit Fsuion"` 且上下重复图例；Fig 11 标题拼错 `"Quantization Lantecy"`；p3 单栏硬塞 Fig 1+2 过于局促 |
| 20 | `conf__asplos__ChenML0MLF26` (FastTTS) | ASPLOS 2026 | `contrast_post2023` | p2, p4, p8, p10, p11 | Fig 1（p2）显式断轴 `//` 的 Pareto 前沿 Teaser；Fig 4/17 真实 NVIDIA Nsight 硬件算力利用率曲线；Fig 9 清爽浅蓝架构图 | Fig 16（p11）横轴 `128256512` 彻底挤撞成一团、`n` 轴标砸在图例 `M` 上；Fig 13（p10）出现**图例完全未解释的亮绿柱**；Fig 15（p11）单栏内嵌悬浮柱折线混杂费解；Fig 4/17(左) 一维曲线配多余 `viridis` 重复色条；Fig 14 单栏硬塞 4 子图致轴标撞数字 |

---

### 1.2 色彩体系、语义一致性与黑白打印安全

#### (1) 顶级论文的四大色彩黄金范式

1. **纯灰度 + 纹理（Monochrome Print-Safe）—— 经典永不过时**
   - `conf__isca__KimSLLM12`（SALP, ISCA 2012）全篇仅用黑/深灰/中灰/浅灰/白 5 阶（p3, p5）；`conf__asplos__FerdmanAKVAJKPAF12`（CloudSuite, ASPLOS 2012, p9 Fig 6–7）用“深灰实心 `Application` vs 斜条纹 `OS`”；`conf__isca__KarandikarMKBAL18`（FireSim, ISCA 2018, p7 Fig 5, p9 Fig 8–9）用“黑色虚线+三角 vs 中灰实线+圆点”。**但纯灰度的死穴在于：一旦序列超过 3 组且不加纹理（hatch），相近灰度就会糊成一片**——哪怕是 SALP（p10 Fig 13–14）和 Elastic Cuckoo（p13 Fig 15）也因此中招。
2. **灰底 + 单强调色（Grayscale + Single Semantic Accent）—— 最高效的注意力引导**
   - `conf__isca__ChenES16`（Eyeriss, ISCA 2016, p5 Fig 3）用纯黑灰画 3D 特征图张量，仅用一抹正红标出当前并发处理区域，3 秒看懂三种 Output-Stationary 数据流差异。
   - `conf__asplos__SkarlatosKXT20`（ASPLOS 2020, p5 Fig 5–6 & p13 Fig 16）在黑白哈希表中仅用红色斜线标示 `Migrated Region`，在延迟直方图中仅用纯蓝标示 `Cuckoo THP`、浅灰退后作 `Baseline THP`。
   - `conf__hpca__LazoRMBVSCUC22`（HPCA 2022, p4 Fig 1）在黑白矢量微架构图中仅将本文新增硬件（`VRF MAPPING` 与 `SWAP MECHANISM`）填绿，评审一眼定位硬件改动边界。
3. **低饱和度语义调色板 + 形状/线型/明度双重冗余（Muted Colorblind-Safe + Redundant Encoding）**
   - `conf__isca__KimDKFLLWLM14`（RowHammer, ISCA 2014, p7 Fig 4–5 & p8 Fig 6–9）：三个 DRAM 模组横跨全文 6 幅图严格锁定 **藏青圆 (`A_23^1240`) / 砖红方 (`B_11^1146`) / 灰绿菱 (`C_19^1223`)**，明度递增且形状各异，彩色、色盲与黑白打印全场景无损。
   - `conf__micro__JeffreySYES15`（Swarm, MICRO 2015, p2 Fig 1, p5 Fig 3–5）：柔和莫兰迪系灰蓝/陶橙/橄榄绿，视觉疲劳度极低。
   - `conf__hpca__WooSN23`（SRS, HPCA 2023, p4 Fig 4, p10 Fig 15, p11 Fig 16）：用**双色相×明度梯度矩阵**编码二维变量——对比基线 `RRS` 走浅橙→深棕，本文 `Scale-SRS` 走浅灰→纯黑，参数 $T_{RH}$ 从 512→4800 单调变深，直觉极强。
   - `conf__isca__BeraRRMNGOKSSM24`（Constable, ISCA 2024, p11 Fig 11, p12 Fig 14 & 16）：全文实验柱状图严格保持 `EVES`（白/浅灰）→ `Constable`（中钢灰）→ `EVES+Constable`（深炭黑）→ `EVES+Ideal Constable`（深藏青）的语义恒定。
4. **感知均匀色图（Perceptually Uniform Colormap）用于二维矩阵/热图**
   - `conf__micro__ChenTTLZQ25`（MICRO 2025, p5 Fig 3–4）与 `conf__micro__XuW0CLZW25`（MICRO 2025, p5 Fig 4）均选用 `viridis`（深紫→青绿→明黄），灰度转换后明度严格单调，远胜传统 `jet` 彩虹色图。

#### (2) 跨图语义色彩破坏与典型色彩反模式

- **警世案例——同页色彩反转（Semantic Color Inversion）**：在视觉整体堪称 2023 年标杆的 `conf__asplos__LiBHEZNSRLAHFB23`（Pond, ASPLOS 2023）中，Fig 4/5（p4）和 Fig 21（p13 右）全部设定 **红 = 222% (255ns)**、**蓝 = 182% (142ns)**；但就在 **p13 左侧的 Fig 20**（p13 左），图例竟毫无征兆地反转成 **蓝 = `At 222% (255ns)`**、**红 = `At 182% (142ns)`**！同一页左右两张相邻图红蓝互换，极易误导审稿人读反结论。
- **高饱和度彩虹与 Excel 默认色污染**：`conf__hpca__QinSKNS0KK20`（SIGMA, HPCA 2020, p11 Fig 12–14）、`conf__micro__ZengKLJ21`（Turnpike, MICRO 2021, p10 Fig 21–23）、`conf__hpca__LazoRMBVSCUC22`（AVA, HPCA 2022, p7 Fig 2 & p9 Fig 3）与 `conf__hpca__HuZ00GH00GL25`（M-ANT, HPCA 2025, p12 Fig 15 16 色堆叠柱）将过多高饱和原色混排，既伤眼又在灰度打印下完全失焦。
- **亮黄无对比度（Neon Yellow Trap）**：`conf__asplos__MiaoJPML19`（ASPLOS 2019, p11 Fig 8）与 `conf__micro__ZengKLJ21`（MICRO 2021, p11 Fig 24）用纯亮黄 `#FFFF00` 作柱体填充，白底对比度极差且打印近乎消失。
- **装饰性冗余色条（Decorative Redundant Colorbar，2025–2026 新兴坏习惯）**：`conf__asplos__ChenML0MLF26`（FastTTS, ASPLOS 2026, p4 Fig 4 & p11 Fig 17 左）给一维时间序列柱状图硬加了按纵轴高度着色的 `viridis` 渐变与右侧色条（`0–60` 与左纵轴 `GPU Compute Util. (%)` 100% 重复），纯属零信息增量的视觉噪音。

---

### 1.3 字体、字号、比例尺与零重叠纪律

1. **字体和谐与字号底线（印刷可读性法则）**
   - 顶会双栏排版下，正文通常为 9–10pt Times/Linux Libertine 衬线体；图内坐标轴标签与核心标注的最佳落地字号应不低于 **7–8pt（正文 75%–85%）**，框图可统一使用干净无衬线体（Helvetica / Arial / DejaVu Sans）以增强小字号辨识度，数据图数学符号（如 `RowHammer` p7 Fig 4–5 的回归方程 $y_A = 4.39\text{e-}6 \times x^{6.23}$）与正文同衬线体显得格外考究。
   - **高频字号塌陷案例**：`SIGMA`（p6 Fig 5 Benes 开关内部文字 ~3.5pt）、`Constable`（p3 Fig 2 顶部周期号 `1..19` 与 p11 Fig 12 底部标注 ~4.5pt）、`Turnpike`（p10 Fig 23 与 p11 Fig 24–26 单栏 42 个 4pt 竖排测试集名）、`AVA`（p9 Fig 3 24 子图内 ~4pt 轴标）。凡需审稿人放大至 250% 才能辨认的文字，本质上等于无效墨水。
2. **零碰撞铁律（在 20 篇中竟捕获 7 处真实排版碰撞！）**
   - **轴标撞图注**：`InvisiSpec`（MICRO 2018, p11 Fig 4）斜排的 `libquantum` 直接压在 `"Fig. 4: Normalized execution time..."` 上方。
   - **横轴刻度粘连 + 轴标砸图例**：`FastTTS`（ASPLOS 2026, p11 Fig 16）横轴 `128`、`256`、`512` 粘连成 `128256512`，中图 `n` 直接叠压在图例 `M` 上；p10 Fig 14 的 `pass@N Accuracy` 撞上左侧 `AMC` 柱图。
   - **相邻子图轴标题碰撞**：`StreamBox-HBM`（ASPLOS 2019, p11 Fig 8）中列左轴 `Throughput MRec/s` 与左列右轴 `HBM BW Use GB/s` 零间隙贴撞；p12 Fig 9 图例长名字撞进纵轴刻度 `30`。
   - **单栏硬塞两张独立图致图注相撞**：`Turnpike`（MICRO 2021, p3 Fig 3 & Fig 4）两段粗体图注在窄栏中间连成 `"Figure 3: Impact of region size inserted checkpoints"`。
   - **图例压柱体 / 数值重叠**：`Turnpike`（p11 Fig 24 `Average/Maximum` 图例压在黄柱顶）；`ρHammer`（MICRO 2025, p8 Fig 8 柱顶 `224` 与 `170` 重叠）。
3. **矢量图内文本必须单独做拼写检查（在 20 篇中捕获 6 处真实图内错词！）**
   - 因为 LaTeX 拼写检查器不会扫描嵌入的 PDF/SVG 图形，即便顶会最佳论文也屡屡中招：`CloudSuite`（p5 Fig 1）`"Total exeution cycles"`；`SIGMA`（p11 Fig 12b）`"Efficiecny"`；`SRS`（p10 Fig 14）`"atleast"`；`LLM.265/VcLLM`（p4 Fig 2b `"Armortize"`, `"Explot"`；p10 Fig 9 `"Comparision"`）；`M-ANT`（p9 Fig 11 `"Quantization Lantecy"`；p12 Fig 13 8 次 `"Bit Fsuion"`）。

---

### 1.4 微架构框图、机制演进图与真实工程证据语法

通过对 20 篇论文所有系统/微架构图的像素级拆解，顶级体系结构论文形成了 **6 种高度成熟的视觉文法**：

1. **双层局部放大法（Hierarchy + Zoom-in Callout）**：用虚线引导框从宏观阵列展开单个微观模块，拒绝把所有晶体管细节堆在同一层级。典型标杆：`SALP`（p4 Fig 5 Bank→Tile 展开）、`Eyeriss`（p2 Fig 1 PE Array→3 PE 内部 RF/pFIFO/ALU 展开）、`FireSim`（p3 Fig 1+2 逻辑集群拓扑→EC2 F1 多层嵌套宿主机映射）。
2. **流水线定位 + 路径分流双联图（Pipeline Anchor + Path-Typed Architecture）**：先用极简水平流水线标明“新增硬件插在哪一级”，再用不同颜色+线型区分控制流/数据流/失效路径。
   - **最佳典范**：`Constable`（ISCA 2024, p6 Fig 8）——(a) 仅占 0.6 英寸高，把 `SLD / RMT / AMT` 精准钉在 `Decode / Rename / Memory` 流水级；(b) 将全部操作严格分为三路：**黑实线 + 黑章 `❶❷❸`（查表消除数据通路）**、**蓝实线 + 蓝章 `❹❺❻`（置信度学习与注册通路）**、**红虚线 + 红章 `❼❽❾❿`（写寄存器/Store/Snoop 失效安全控制通路）**，彻底做到“虚线表控制/失效、实线表主数据流”。
3. **同视觉词汇的渐进式时间线对照（Progressive Timeline Comparison）**：用完全一致的色块图元从 Baseline 逐步演进到 Proposed，用双向括号箭头直标 `saved` 收益。
   - **最佳典范**：`SALP`（ISCA 2012, p5 Fig 7–8）从 `Same-bank (Baseline)` → `Diff-bank ("Ideal")` → `SALP-1` → `SALP-2` → `MASA` 复用完全相同的 `ACT / W / tWR / PRE / R` 图元，`saved` 箭头逐层拉长；`Constable`（ISCA 2024, p3 Fig 2）从 `(A) Without LVP` → `(B) With LVP`（绿字 `4 cycles saved`）→ `(C) With LVP + Load elimination`（绿字 `2 more cycles saved`）。
4. **分镜故事板状态演进图（Storyboard / Concrete-Example Walkthrough）**：拒绝抽象符号堆砌，用真实具体地址/指令/表项演示状态机如何逐拍变迁，并用红字或删除线高亮“本拍唯一变动处”。
   - **最佳典范**：`Swarm`（MICRO 2015, p2 Fig 1 与 p5 Fig 4）；`SRS`（HPCA 2023, p7 Fig 8 4 帧虚线分栏 + 删除线标示失效表项 + 层次编号 `❶→1.1→1.4, ❷→2.1→2.5`）；`Constable`（ISCA 2024, p9 Fig 10 全宽 7 步 `(A)→(G)` 时间轴 + 红字表项刷新 + 绿框正确消除 vs 红框错误恢复）；`LLM.265`（MICRO 2025, p4 Fig 2b 6 行累加消融瀑布图）。
5. **逐跳物理延迟预算图（Hop-by-Hop Latency Budget Diagram）**：将微架构拓扑与定量开销融合到一张图里。
   - **最佳典范**：`Pond`（ASPLOS 2023, p5 Fig 7）在每个物理跳模块下方直接标注 ns 延迟（`40ns | 25ns | 5+20+5ns | ...`），右上角嵌入紧凑 `Latency assumptions` 小表，右侧配服务器刀片物理线缆距离示意图（`<500mm` vs `>500mm`），一张图打通物理约束与系统性能建模。
6. **高可信度真实工程证据（Hardware / System Ground-Truth Visuals）**：胜过千言万语的说服力武器。
   - 真实流片显微照片 + 尺寸标注 + 规格简表：`Eyeriss`（ISCA 2016, p5 Fig 4）。
   - 真实 EDA 等比例面积对比 + PnR 版图着色：`LLM.265`（MICRO 2025, p10 Fig 9）与 `AVA`（HPCA 2022, p12 Fig 5）。
   - 真实 Linux 终端输出截图 + 红框标注：`Pond`（ASPLOS 2023, p7 Fig 10 `sudo numactl --hardware`）。
   - 真实硬件 Profiler 波形：`FastTTS`（ASPLOS 2026, p4 Fig 4 NVIDIA Nsight Systems 算力利用率采样）。

- **框图反模式警示**：
  - **盒内文字墙 / 微缩字**：`SIGMA` p6 Fig 5 试图在一张图内塞入 7 块电路+路由计算+完整开关内部逻辑，导致子模块文字缩至 3.5pt；
  - **业余剪贴画 + `wrapfigure` 挤文字**：`Turnpike` p3 Fig 5 用交通 `STOP/GO` 标志且窄栏环绕排版，严重破坏学术质感；
  - **编号错误**：`AVA` p4 Fig 1 两个不同位置都标了 `❹`。

---

### 1.5 实验图表人体工学：选型、标注、截断诚实性与反模式

#### (1) 体系结构实验图表选型与高阶人体工学语法

| 数据结构与论证目标 | 推荐图表形态 | 标杆实例（附 PNG 链接） | 严禁替代品 |
|---|---|---|---|
| 多测试集（10–35 个）性能加速/开销主结果 | **升序排序分组柱状图** + **独立视觉分隔的 `GEOMEAN/AVG` 阴影区或红虚线** + 均值直标数值 | `SALP` p10 Fig 13（按收益升序）；`SRS` p10 Fig 14（红虚线分隔 `GMEAN` + 双括号）；`Constable` p11 Fig 11（灰底 `GEOMEAN` + 竖排精确数字） | 无序字母排布且 `Geomean` 混在柱群里；单栏硬塞 40+ 根测试集条形码（`Turnpike` p10 Fig 23） |
| 大规模测试集（50–160 个）分布全貌 | **分组全宽概览柱图 + 紧邻 CDF 累积分布图**（或排序 S 曲线配优劣阴影区） | `Pond` p4 Fig 4 + Fig 5（158 负载分 9 套件 + CDF 直标离群）；`Constable` p11 Fig 12（90 负载升序折线 + 红绿胜负底纹） | 只给单点均值掩盖长尾，或硬塞 24 张分图（`AVA` p9 Fig 3） |
| 延迟/能耗/时间分解（$\le 5$ 类） | **100% 或绝对值堆叠柱状图**（颜色 + 纹理双冗余） | `CloudSuite` p5 Fig 1 & p9 Fig 6–7；`M-ANT` p12 Fig 13–14 | **饼图**（`SIGMA` p3 Fig 2）；**>6 类（如 16 色）堆叠柱**（`M-ANT` p12 Fig 15） |
| 连续参数敏感度 / 核数扩展性 | **折线图 / 水平共享轴小倍数（Small Multiples）** + 出界极值直标 + 曲线旁直标 | `Swarm` p9 Fig 11 & p10 Fig 12（6 子图共享纵轴+右侧单图例+出界标 `117×`）；`Pond` p6 Fig 8 & p12 Fig 18（曲线直标 + 误差棒） | 用连续折线串联无序离散测试集（`SIGMA` p11 Fig 12）；每个子图各复制一份相同图例 |
| 精度–延迟 / 性能–功耗权衡 | **Pareto 前沿散点/折线图** + 显式断轴 `//` + 目标方向箭头 | `FastTTS` p2 Fig 1b（阴影云端区 + 绿星 + 显式 `//` 断轴）；`RowHammer` p7 Fig 4–5（散点+拟合曲线+内嵌公式） | 隐瞒断轴或把两项权衡拆成两张不同纵轴范围的孤立柱图 |
| 二维位关系 / 密度 / 延迟分布 | **感知均匀热图 (`viridis`)** 或 **带硬件层级区间标注的直方图** | `ρHammer` p5 Fig 3–4；`Elastic Cuckoo` p13 Fig 16 | 16 色堆叠柱；`jet` 彩虹热图 |

#### (2) 直接标注（Direct Callouts）vs 远距图例搜寻

- **标杆级直标范式**：`Pond`（p6 Fig 8）完全取消传统图例框，直接在曲线旁用对应色文字标出 `Switches only`、`1 Switch`、`2 Switches`、`Pond with multi-headed design`，并用醒目红色双箭直标 `-36% ↓`，读者零眼跳即得核心结论。`StreamBox-HBM`（p12 Fig 10）甚至把带圈步序 `①–⑦` 直接标在双子图实验曲线的拐点上，使“先看图再对照段落解释动态均衡机制”丝般顺滑。
- **共享单图例铁律**：多子图共享同一套图例时，**必须且只能出现一次**（置于顶部居中或最右侧，如 `Swarm` p10 Fig 12、`LLM.265` p7 Fig 5）。**重复图例反模式**竟连标杆论文都高频犯错：`SALP`（p11 Fig 15 重复 4 次，吃掉近半画布）、`Eyeriss`（p11 Fig 11–12 重复 3 次）、`PVCoherence`（p11 Fig 6–8 竖排 3 重复）、`Elastic Cuckoo`（p13 Fig 15 竖排 3 重复）。

#### (3) 纵轴截断、断轴诚实性与离群值处理

- **核心伦理与视觉张力**：体系结构论文常见 1%–15% 的归一化加速（`1.00–1.15`）或低开销安全防护（`0.90–1.00`）。直接从 `0` 画起会让差异压缩成一条细缝，但**静默截断柱状图纵轴**（如 `Constable` p11 Fig 11 从 `1.00` 起、`SRS` p10 Fig 14 从 `0.70` 起、`LLM.265` p7 Fig 6 右 准确率柱图从 ~55 起、`FastTTS` p4 Fig 3 左 从 `100` 和 `45` 起）会在视觉面积上夸大 2×–4× 的比例差距！
- **三种诚实且优雅的解法**：
  1. **改画相对百分比增益/开销（从 `0%` 起）**：如 `SALP`（p10 Fig 13 `IPC Improvement 0%–80%`），零点真实且差异清晰。
  2. **若折线/Pareto 图必须跨大空白区间，强制加显式断轴符号 `//`**：如 `FastTTS`（p2 Fig 1b `45 // 85..90`）。
  3. **若归一化柱状图截断于 `0.95` 或 `1.00`，必须在 `1.00` 处画醒目基线虚线并在关键汇总柱顶直标真实数值**（如 `Constable` p12 Fig 15 的红色 `1.00` 虚线 + 精确数字 `1.047 / 1.051`）。
- **单一极端离群值处理（防压扁其余曲线/柱子）**：`Swarm`（p9 Fig 11 & p10 Fig 12）将纵轴定格在理想线性上限 `64×`，在冲破顶框的超线性曲线旁优雅斜标 `122× / 112× / 83× / 117×`；`Pond`（p4 Fig 5）在 CDF 截断处直写诚实说明 `"Three outliers under 255ns with >100% slowdowns (max 124%)"`，远胜强行拉高纵轴让 95% 数据贴地。

#### (4) 四大高危实验图反模式总结

1. **“24 宫格/42 条形码”原始数据倾倒症**：`AVA`（p9 Fig 3 24 子图无汇总）与 `Turnpike`（p10–11 Fig 21–26 单栏 42 根微缩彩柱 + 双轴 84 根黑白条形码）。评审看论文要的是洞察与总结，不是作者的原始 Excel 文件夹。
2. **双轴柱线大杂烩 + 离散类目连折线**：`SIGMA`（p10 Fig 10–11 & p11 Fig 12–14）把 6 组彩色柱和 2 条折线或散点黑斑压在同一双轴画布上，且用连续折线连接互不相关的离散矩阵尺寸。
3. **图例缺失 / 图例与图形元素不一致**：`LLM.265`（p7 Fig 5–6 红色水平虚线无图例）、`FastTTS`（p10 Fig 13 出现图例完全未提及的亮绿柱）、`AVA`（p9 Fig 3 第三列 蓝橙无图例）、`ρHammer`（p8 Fig 8 左右纵轴均无标题与单位）。
4. **并排子图纵轴比例尺暗中变化**：`Eyeriss`（p11 Fig 11 `0.025 / 0.03 / 0.015`）与 `FastTTS`（p11 Fig 16 `60% / 300% / 400%`），共享单一左侧纵轴标题却暗换三套标尺，极易引发横向高度误读。

---

### 1.6 表格视觉工艺：Booktabs、层级对齐与信息密度

20 篇视觉样本揭示了一条清晰的表格工艺分水岭：

- **黄金标杆（Clean Booktabs + 视觉分层 + 语义加粗）**：
  - `SALP` p3 Table 1：顶底粗线（`\toprule`/`\bottomrule`）、`\cmidrule` 分组表头、**零竖线**、仅对关键瓶颈值（`~50`, `15`）加框加粗、表底紧附紧凑符号脚注。
  - `RowHammer` p3 Table 1, p7 Table 4, p8 Table 5, p10 Table 6：全书统一无竖线 booktabs，整数统一右对齐加千分位逗号（`1,318,603`），**仅加粗每行最大值或不可纠正错误并在表注显式说明**（`"Uncorrectable multi-bit errors (in bold)"`）。
  - `Swarm` p9 Table 3–4：配置表用细横线（`\midrule`）逻辑分组（Cores / Caches / NoC / Swarm Queues），左列右对齐加粗键名、右列左对齐紧凑说明，零废话。
  - `StreamBox-HBM` p3 Table 1：90° 竖排表头 + 实心黑点 `•` 构成极省空间的算子能力矩阵。
  - `ρHammer` p3 Table 1–2：现代极淡灰斑马纹（`~5% gray`）配合 booktabs，兼顾长表行扫描与清爽观感。
  - `PVCoherence` p9 Table 1：协议规范对比表仅将新协议相对旧协议的**增量改动加粗**，极大降低评审核查协议正确性的认知负荷。
- **五大表格反模式**：
  1. **全竖线格子笼（Vertical-Line Prison）**：即便在获奖论文中也反复出现——`Eyeriss`（p5 Table III）、`FireSim`（p3 Table I–II）、`InvisiSpec`（p8 Table III）、`SRS`（p10–11 Table III–V）、`Turnpike`（p10 Table 1）。
  2. **糖果彩虹斑马纹（2024–2026 新通病）**：`ρHammer`（p11 Table 6）给 4 个测试平台分别铺上粉红/天蓝/淡紫/蜜桃四色斑马底纹，毫无定量语义却制造强烈视觉噪音。
  3. **过度小数精度与单位格式失范**：`Turnpike`（p10 Table 1）用 CACTI 仿真模型报出 5 位小数能耗 `0.43099 pJ`、`0.02518 pJ`（伪精确）；`SRS`（p11 Table IV）同行内混写 `35 KB` 与 `9.4KB`；`Elastic Cuckoo`（p11 Table 2）漏掉面积平方 `1.9*10^-3 mm`。
  4. **数字居中而非右对齐 + 缺千分位**：`CloudSuite`（p3 Table 1）大段文字居中；`ρHammer`（p11 Table 6）将 `257881, 13880` 无千分位逗号拼在同一格，扫读极易看错数量级。

---

### 1.7 15 年视觉演化轨迹（2011–2015 vs 2016–2022 vs 2023–2026）

把 20 篇视觉样本按年代排开——尤其是横向对照**同一权威课题组（Onur Mutlu / SAFARI）跨越 12 年的三篇代表作**（`SALP ISCA'12` → `RowHammer ISCA'14` → `Constable ISCA'24`）——能清晰看见体系结构顶会视觉范式的三代跃迁：

| 视觉维度 | 2011–2015（黑白印刷优先期） | 2016–2022（彩色工具过渡与两极分化期） | 2023–2026（数字优先高密度信息图期） |
|---|---|---|---|
| **典型样本** | `SALP'12`, `CloudSuite'12`, `RowHammer'14`, `PVCoherence'14`, `Swarm'15` | `Eyeriss'16`, `FireSim'18`, `InvisiSpec'18`, `StreamBox-HBM'19`, `SIGMA'20`, `Elastic Cuckoo'20`, `Turnpike'21`, `AVA'22` | `Pond'23`, `SRS'23`, `Constable'24`, `LLM.265'25`, `ρHammer'25`, `M-ANT'25`, `FastTTS'26` |
| **色彩策略** | 绝对主流为纯灰度+斜纹（SALP, CloudSuite），少数先锋用 3 色莫兰迪/双冗余（RowHammer, Swarm）；纸质黑白印刷兼容性摆在第一位 | 开始全面转彩但工具链割裂：顶级组用灰+单强调色（Eyeriss, Elastic Cuckoo），但大量论文直接导出**原生 Excel/PPT 默认彩图**（SIGMA, Turnpike, AVA）导致视觉灾难 | 全面进入 Python (`matplotlib/seaborn`) + 矢量图（Draw.io / Illustrator / Inkscape）时代：柔和色板、`viridis` 热图、语义路径配色成为标配；但涌现新通病（冗余 colorbar、16 色堆叠、糖果表） |
| **首页与框图范式** | Fig 1 极少上首页（仅 1/14 篇），多为第 2 页基础背景图；框图偏极简黑白电路/结构示意 | 首页 Teaser 开始兴起（4/18 篇），出现 Die Photo（Eyeriss）、代码+图注并排（InvisiSpec）、复杂 7 步推演（SIGMA） | **高信息密度故事板与系统全栈图成熟**：首页双目标 Teaser（SRS, LLM.265）、路径分色框图（Constable Fig 8）、7 步状态分镜（Constable Fig 10）、逐跳延迟预算（Pond Fig 7）、真实终端/Profiler/EDA 版图广泛入文 |
| **数据图人体工学** | 偏传统分组柱图/简单折线；`gmean` 常无分隔、子图偶现重复图例；**极少直接图内文字标注** | 开始广泛出现多子图网格、双轴图，但同时伴随最严重的图例重复、轴标碰撞和 24 宫格失控 | **图内直接标注（Direct Callouts）成为分水岭**：阴影 `GEOMEAN` 区+柱顶直标精确值（Constable）、红虚线分区（SRS）、曲线直标+`-36%↓` 箭头+诚实离群框（Pond）、显式 `//` 断轴（FastTTS） |
| **SAFARI 课题组 12 年纵向进化** | **2012 SALP**：纯灰度、黑圆标 `❶–❺`、升序柱图但无 `gmean` 分隔且 4 灰柱无纹理、Fig 15 重复 4 图例 → **2014 RowHammer**：引入 3 色+3 形状全篇锁定与内嵌回归公式 | （过渡期积累矢量配色与图内标注规范） | **2024 Constable**：完整继承 `❶–❿` 正文联动与升序全负载曲线，叠加红/蓝/黑三路径语义框图、全宽 `(A)→(G)` 分镜、灰底 `GEOMEAN` 数值直标与红绿胜负阴影区 |

---

## 2. 阶段 B：48 篇 `deep_read` 论文的图表预算、图注解剖与图文耦合

### 2.1 图表数量预算（按会议、年代、分层与章节分布）

对全部 **48 篇 `deep_read` 论文**（以及 152 篇 `macro_pool` 预算交叉核验）进行定量统计，得到以下稳定规律：

#### (1) 总体、分层、会议与年代预算表（48 篇 `deep_read` + 152 篇 `macro_pool` 对照）

| 维度分组 | 样本量 | 图数量中位数 / 均值 [范围] | 表数量中位数 / 均值 [范围] | 152 篇 `macro_pool` 图 / 表中位数验证 | 图注词数中位数 / 均值 | 多句图注占比 (≥2 句) | 含结论/主张图注占比 | Fig 1 页码分布 (p1 / p2 / p3+) |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| **全部 `deep_read`** | **48** | **15.0 / 14.3 [5–27]** | **3.0 / 3.5 [0–7]** | **13.0 / 3.0** | **17.0 / 21.2** | **45.8%** | **12.1%** | **8 / 25 / 15** |
| — `exemplar`（标杆） | 32 | 14.5 / 14.5 [7–27] | **3.0 / 3.7** [0–7] | — | **18.0 / 21.9** | **47.9%** | **13.2%** | 6 / 16 / 10 |
| — `contrast_ordinary` | 10 | 15.0 / 14.3 [5–26] | **2.0 / 2.4** [1–5] | — | **12.0 / 16.8** | **31.2%** | **6.5%** | 1 / 6 / 3 |
| — `contrast_post2023` | 6 | 13.0 / 13.2 [9–18] | **5.5 / 4.3** [0–7] | — | **21.0 / 24.6** | **59.0%** | **15.4%** | 1 / 3 / 2 |
| **ISCA** | 12 | 13.0 / 13.0 [7–19] | 2.5 / 3.2 [1–7] | 12.0 / — | 13.0 / 18.7 | 43.1% | 5.9% | 1 / 9 / 2 |
| **MICRO** | 12 | **16.0 / 16.8** [8–27] | **4.0 / 4.2** [1–7] | 13.0 / — | 14.0 / 18.3 | 32.1% | **16.1%** | 3 / 5 / 4 |
| **HPCA** | 12 | **15.0 / 14.3** [5–21] | **4.0 / 4.0** [2–7] | **14.0** / — | 20.5 / 24.2 | 52.4% | 11.8% | **4** / 3 / 5 |
| **ASPLOS** | 12 | 12.0 / 13.1 [7–21] | 2.5 / 2.5 [0–7] | 12.5 / — | **22.0 / 23.7** | **58.1%** | 13.5% | 0 / 8 / 4 |
| **2011–2015** | 14 | 13.0 / 13.0 [7–21] | 3.5 / 3.9 [1–7] | **12.0 / 3.0** | **10.0 / 15.3** | **29.8%** | **5.5%** | 1 / 9 / 4 |
| **2016–2022** | 18 | 14.5 / 14.7 [5–26] | 3.0 / 3.2 [1–7] | **13.0 / 3.0** | **18.0 / 21.5** | **46.3%** | **11.8%** | 4 / 8 / 6 |
| **2023–2026** | 16 | **15.5 / 15.0** [7–27] | 3.0 / 3.5 [0–7] | **15.0 / 3.0** | **22.0 / 25.3** | **57.4%** | **17.4%** | 3 / 8 / 5 |

> **PyMuPDF 真值校验（20 篇 OA PDF 精确排版块，261 图 / 63 表）**：图注词数中位数 **13.0**（均值 18.5，IQR 7–27，p90=39，max=77），表注词数中位数 **7.0**（均值 10.0，p75=14，max=42），多句图注占比 **44.1%**，含结论/主张图注占比 **13.0%**——与 48 篇全样本统计高度吻合（误差主要源自非 OA 会议中 ASPLOS/近期长图注略多）。

#### (2) 关键预算洞见

1. **“12–16 图 + 2–4 表”是体系结构顶会最稳健的黄金预算区间**（48 篇中位数 15 图 + 3 表，152 篇大样本稳定在 12→15 图 + 3 表）。图数量极端偏低（如 `AVA` 仅 5 图却把 24 张图压进 Fig 3）或极端爆炸（如 `Turnpike` 13 页塞 26 图）均对应严重的视觉失衡；唯独 `Whisper`（MICRO 2022, 23 图）和 `Neu10/XueLN024`（MICRO 2024, 27 图）这类 16 页长文因评估敏感度丰富才合法突破 20 图。
2. **15 年图表通货膨胀清晰可见**：在 152 篇大样本与 48 篇精读样本中，**图数量中位数同步从 12–13 张（2011–2015）攀升至 15–15.5 张（2023–2026）**（增幅 ~20%），而**表数量中位数 15 年纹丝不动维持在 3 张**。这与会议正文页数从 11–12 页放宽至 13–15 页（不含参考文献）以及现代 LLM/多维度消融实验增多直接相关。
3. **会议文化差异**：**MICRO 与 HPCA 图表最密集**（中位 15–16 图 + 4 表），强调详尽微架构参数与硬件面积/功耗开销表；**ASPLOS 表格最少**（中位 2.5 表，甚至出现 0 表杰作 `Pond` ASPLOS'23 与 `FastTTS` ASPLOS'26），但**图注显著最丰满**（中位 22 词、58.1% 多句），体现系统会议重视单图自洽叙事。
4. **分章节图表比例（基于 31 篇顶层章节精确映射子集：438 图、118 表）**：

| 论文章节区段 | 图数量及占比 | 表数量及占比 | 核心功能定位 |
|---|---:|---:|---|
| 1. Introduction | 24 (5.5%) | 0 (0.0%) | 首页/第 2 页问题 Teaser 或全局愿景图（几乎从不在 Intro 放表） |
| 2. Background & Motivation / Characterization | 88 (20.1%) | 26 (22.0%) | 瓶颈量化实证图、攻击/问题案例、相关工作特性对比表 |
| 3. Architecture / System Design | 199 (45.4%) | 44 (37.3%) | 总体架构框图、机制演进分镜、算法状态机、硬件存储/面积/协议开销表 |
| 4. Methodology & Setup | 12 (2.7%) | 17 (14.4%) | 仿真器/平台配置表、负载套件表（表占比远高于图占比！） |
| 5. Evaluation & Sensitivity | 103 (23.5%) | 23 (19.5%) | 主性能/能耗图、细分拆解、参数敏感度、硬件开销汇总表 |
| 6. Discussion / Related Work / Conclusion | 12 (2.7%) | 8 (6.8%) | 综合比较矩阵或跨层路线图 |

> 注：受部分论文把“设计验证/微基准评估”嵌入 Design 章节（如 `Pond` §4、`RowHammer` §4、`LLM.265` §3）影响，若按 **三大宏观叙事模块** 统计篇均占比，约为：**引言与动机 25.4% ：设计与方法论 47.0% ：评估与讨论 27.6%**（近乎 **1 : 2 : 1** 的黄金骨架；若纯按图表内容分类统计全部 670 图，**定量数据图 [动机实证 8.1% + 评估结果 39.6% = 47.6%]** 与 **架构/机制示意图 [52.4%]** 恰好各占半壁江山！）。

---

### 2.2 规范图表分类体系与 Figure 1 定位策略

1. **体系结构论文 6 大规范图型配比（48 篇 `deep_read` 全量 670 图）**：
   - **评估结果数据图（39.6%）**：主加速/开销、能耗/周期分解、敏感度、扩展性、消融。
   - **微架构/系统总览框图（16.0%）**：总体框图、层次放大、流片/版图、拓扑映射。
   - **机制演进与实例推演图（12.8%）**：时间线对照、状态机分镜、协议交互、代码片段。
   - **动机与瓶颈实证数据图（8.1%）**：在提出方案之前用数据证明问题严重性与改进上限（headroom）。
   - **背景示意与其他设计子图（23.6%）**：基础硬件背景、辅助结构、数据格式示意。
2. **Figure 1 放置策略：何时放 Page 1 vs Page 2？**
   - 在全部 48 篇论文中，**68.8%（33/48）在前两页即亮出 Figure 1**：**Page 1 占 16.7%（8/48）**、**Page 2 占 52.1%（25/48）**、Page 3+ 占 31.3%（15/48，其中 `HFI` ASPLOS'23 甚至推迟到 Page 7 才放首图，前 6 页全靠代码列表与威胁模型表推进）。
   - **Page 1 Teaser 的年代崛起**：从 2011–2015 年的 **1/14（7.1%）** 升至 2016–2026 年的 **7/34（20.6%）**，且集中出现在 **HPCA（4/12）与 MICRO（3/12）** 及 **加速器/ML（4/12）与安全（2/8）** 领域。
   - **有效的 Page 1 Figure 1 必属四类之一**（拒绝把平庸的基础背景塞上首页！）：
     1. **双目标问题+愿景量化 Teaser**：`SRS`（HPCA'23, p1 Fig 1）一图定调攻防双重 `GOAL`；`Chasing Carbon`（HPCA'21, p1 Fig 1）展示 2030 全球 ICT 能耗危机；`QPlacer`（ISCA'25, p1 Fig 1）展示量子串扰失真 vs 面积权衡。
     2. **方案覆盖度/范式对比 Teaser**：`LLM.265`（MICRO'25, p1 Fig 1）直观对比现有量化仅覆盖单一张量 vs 本文通吃全部 5 类张量。
     3. **极短核心攻击/问题代码示例**：`InvisiSpec`（MICRO'18, p1 Fig 1）15 行 Spectre v1 代码直接把威胁模型具象化。
     4. **Page 2 强动机图（最稳妥主流）**：`FastTTS`（ASPLOS'26, p2 Fig 1）左显存墙+右 Pareto 延迟跃迁；`Swarm`（MICRO'15, p2 Fig 1）四联图揭示有序不规则并行度。

---

### 2.3 Caption 解剖学：词数分布、结论前置与 15 年演化

#### (1) 词数分布与年代剧变

- **48 篇全量分布（671 图注 / 164 表注）**：
  - **图注词数**：`p10=5`, `p25=8`, **`p50=17`**, `p75=31`, `p90=45`（均值 `21.2`；20 篇 PyMuPDF 真值 `p50=13`, `IQR=7–27`, `p90=39`）。
  - **表注词数**：`p10=3`, `p25=5`, **`p50=9`**, `p75=19`, `p90=35`（均值 `14.3`；PyMuPDF 真值 `p50=7`, `p75=14`）。可见**表注天然比图注短一半左右**，通常只需精准名词短语概括表内对象与关键高亮约定。
- **15 年图注结构跃迁（最震撼的阶段 B 量化发现）**：
  - **2011–2015**：图注中位仅 **10 词**，单句名词短语占 **70.2%**，含结论/量化主张仅 **5.5%**（典型如 `SALP` ISCA'12 `Fig 1: DRAM bank organization` 仅 3 词）。
  - **2016–2022**：图注中位增至 **18 词**，多句占 **46.3%**，结论主张率翻倍至 **11.8%**。
  - **2023–2026**：图注中位达 **22 词**，多句占 **57.4%**，结论主张率**超 3 倍跃升至 17.4%**！
- **标杆 vs 普通论文的图注区分度**：`exemplar` 图注中位词数比 `contrast_ordinary` 高 **50%**（**18.0 词 vs 12.0 词**），多句自洽率高出 **16.7 个百分点**（**47.9% vs 31.2%**），结论主张率更是普通论文的 **2 倍以上**（**13.2% vs 6.5%**）！这说明顶会评审在“先翻图后读文（figure-skimming）”时，自洽且带核心结论的图注具有巨大加分效应。

#### (2) 四类高水准图注范式 vs 两类劣质图注（全为原文逐字引述）

1. **范式 A：`<精炼标题> + (§章节回链) + <斜体一句话结论>`（推荐度最高，现代系统/体系结构金标准）**
   - `conf__asplos__LiBHEZNSRLAHFB23`（Pond, ASPLOS 2023, p6 Fig 8, 14w）：
     > *"Figure 8: **Pool access latency comparison (§4.1).** Pond reduces latencies by 1/3 compared to switch-only designs."*
   - `conf__asplos__LiBHEZNSRLAHFB23`（Pond, ASPLOS 2023, p4 Fig 5, 27w）：
     > *"Figure 5: **CDF of slowdowns (§3.3).** Higher remote latency (red) only slightly affects the head of the distribution (workloads with less than 5% slowdown). The body and tail of the distribution see significantly higher slowdowns."*
   - *点评*：即便图表因 LaTeX 浮动漂移到下一页，`(§4.1)` 立即建立与正文的双向锚点，斜体尾句让速读审稿人 2 秒抓牢 takeaway。全语料库 48 篇中已有 **8 篇（多为 ASPLOS/MICRO 标杆）**采用图注内章节回链（`§X.Y` / `Sec. X`）。
2. **范式 B：`<实验变量描述>: <带精确数字的结论>`（评估图表最佳范式）**
   - `conf__micro__KhanUNSLJK22`（Whisper, MICRO 2022, p3 Fig 1, 23w）：
     > *"Fig. 1: Data center application limit study: an ideal branch predictor achieves an average IPC speedup of 12.4% (1.3%–26.4%) over the state-of-the-art 64KB TAGE-SC-L baseline."*
   - `conf__micro__KhanUNSLJK22`（Whisper, MICRO 2022, p13 Fig 21, 16w）：
     > *"Fig. 21: Whisper’s performance for various baseline branch predictor’s sizes: Whisper reduces even 1MB TAGE-SC-L’s mispredictions by 11.2%."*
   - `conf__hpca__WooSN23`（SRS, HPCA 2023, p10 Fig 14, 36w）：
     > *"Fig. 14. The normalized performance of Scalable and Secure Row Swap (Scale-SRS) and Randomized Row Swap (RRS) compared to a not-secure baseline at $T_{RH}$ of 1200. Scale-SRS and RRS incur an average slowdown of only 0.7% and 4% respectively, with several benchmarks in RRS incurring >10% slowdown."*
   - `conf__isca__ChenES16`（Eyeriss, ISCA 2016, p11 Fig 12, 53w）：先说明 `(a)-(d)` 与归一化基准，末句收束：*"The RS dataflow is 1.4× to 2.5× more energy efficient than other dataflows."*
3. **范式 C：直接断言句标题（Claim-as-Title）**
   - `conf__micro__JeffreySYES15`（Swarm, MICRO 2015, p2 Fig 1, 11w）：
     > *"Figure 1: Dijkstra’s single-source shortest paths algorithm (`sssp`) has plentiful ordered irregular parallelism."*
   - `conf__micro__XueLN024`（Neu10, MICRO 2024, p5 Fig 9, 15w）：
     > *"Fig. 9: The current VLIW-style ISA causes NPU underutilization, as it cannot exploit available MEs at runtime."*
4. **范式 D：问题导向式图注（Question-Form Captions，极适合特征剖析/攻击探索类论文）**
   - `conf__isca__KimDKFLLWLM14`（RowHammer, ISCA 2014, p8 Fig 7–9）：连续三图连发三问——*"Figure 7. How many cells are affected by an aggressor row?"* / *"Figure 8. How many rows are affected by an aggressor row?"* / *"Figure 9. Which rows are affected by an aggressor row?"*；`LLM.265`（MICRO 2025, p4 Fig 2）*"Fig. 2. Why does the Video Codec Work for LLM?"*。
5. **反模式 1：懒惰哑巴图注（Lazy Non-Self-Contained Captions）**
   - 如 `conf__micro__ZengKLJ21`（MICRO 2021, p5 Fig 10）*"Figure 10: LICM at 2c"*（3 词，不翻正文根本不知 `2c` 指代什么）；p10 Fig 23 *"Figure 23: Store breakdown; 2-entry CLQ; 10-cycle WCDL"*（毫无结论，仅罗列缩写）；`conf__asplos__ChenML0MLF26`（ASPLOS 2026, p10 Fig 14）*"Figure 14. Algorithm accuracy (e.g., 1.5/7 for 1.5B+7B)."*（连是哪个模型、评估方法与结论均未点明）。
6. **反模式 2：臃肿图例替代型图注（Bloated Legend-Dump Captions）**
   - 当一张图画得过度拥挤时，作者被迫把图注写成 75–96 词的长段字典，如 `conf__hpca__LazoRMBVSCUC22`（HPCA 2022, p9 Fig 3, 77 词 & p12 Fig 5, 96 词逐字母解释 `A) lane 1; B) lane 2; ... M) AVA structures`）。**图注的最佳甜区是 15–35 词（1–2 句，最多 3 句）；超过 50 词往往意味着图形本身需要拆图或改为图内直标。**

---

### 2.4 图文耦合机制：引入动词、编号同步与“趋势综合 vs 念柱子”

#### (1) 图表引入动词分布（48 篇 `deep_read` 全文实测）

- **引图动词 Top 8**（共捕获 477 次显式 `Figure X <verb>` 句式）：**`shows`（340 次，71.3%）** 遥遥领先，其次为 **`illustrates`（39，8.2%，多用于架构/原理图）**、**`presents`（21，4.4%）**、**`compares`（16，3.4%）**、**`depicts`（12，2.5%）**、**`plots`（10，2.1%，专用于数据曲线/散点）**、**`provides`（8）**、**`reports`（4）**。
- **引表动词 Top 5**（共 105 次）：**`shows`（55，52.4%）**、**`summarizes`（22，21.0%）**、**`lists`（7，6.7%）**、**`presents` / `compares` / `reports` / `describes`（各 4 次）**。
- **风格启示**：顶会写作从不刻意堆砌花哨动词（如 `elegantly unveils / holistically showcases`），而是克制地用 **`shows`**（通用主力）、**`illustrates / depicts`**（框图/演进）、**`compares / plots`**（对比/曲线）、**`summarizes / lists`**（表格）。

#### (2) 微架构框图的“内联编号步进法”（Step-Badge Prose Walkthrough）

在 `SALP`（p3）、`Elastic Cuckoo`（p4）、`SRS`（p7）、`Constable`（p6, p9）与 `StreamBox-HBM`（p12）中，正文直接内嵌与图完全同款的圆圈徽章引导阅读视线：

> *"During the rename stage, a load instruction first checks the SLD using the load PC (**❶ in Fig. 8**). If the `can_eliminate` flag is set in the corresponding SLD entry, Constable breaks the load data dependence using the last-fetched value stored in the SLD entry and eliminates its execution (**❷**). If the `can_eliminate` flag is not set, Constable checks the stability confidence level... (**❸**)."* — `conf__isca__BeraRRMNGOKSSM24`（ISCA 2024, p6）

这种“视线坐标锚定”把复杂微架构控制流的阅读阻力降低了一个数量级。

#### (3) 实验结果段落：“趋势综合 + 机理归因” vs “念柱子反模式”

48 篇文本分析显示，标杆论文有 **7/32（21.9%）** 系统化采用显式结构化洞察标记（`"We make three key observations. First, ..."` / `"Finding 6 ... Implication ..."` / `"We draw two conclusions."`），远高于普通论文的 **1/10（10.0%）**。对比两段真实评估正文，高下立判：

- **标杆范式（框架交代 → 结构化宏观结论 → 差异的微架构因果解释）**：
  - `conf__isca__KimSLLM12`（SALP, ISCA 2012, p10）：
    > *"Figure 13 shows the performance improvement of SALP-1, SALP-2, and MASA on a system with 8 subarrays-per-bank over a subarray-oblivious baseline... **We draw two conclusions. First**, SALP-1, SALP-2 and MASA consistently perform better than baseline for all benchmarks. On average, they improve performance by 6.6%, 13.4%, and 16.7%, respectively. **Second**, MASA captures most of the benefit of the 'Ideal,' which improves performance by 19.6%... **The difference in performance improvement across benchmarks can be explained by a combination of factors related to their individual memory access behavior. First**, ... (>25 MPKI, >15 WMPKI)..."*
  - `conf__asplos__XuSLBWLX026`（PF-LLM, ASPLOS 2026, p12）：
    > *"Figure 10(a) shows that on 1 NVIDIA H20 GPU, our system achieves an inference throughput of up to 234 requests per second. **This high performance is due to three factors**: 1) the small 0.5B parameter count of PF-LLM; 2) the input context lengths are relatively short, with most assembly contexts being under 3000 tokens, as shown in Figure 10(b); 3) our methodology of analyzing all load instructions in a binary provides a large number of independent requests."*
- **反模式（机械“念柱子” / 评估段才补背图例定义）**：
  - `conf__hpca__LazoRMBVSCUC22`（AVA, HPCA 2022, p9）：
    > *"Figure 3-b3 shows the performance results. For AVA-X2 there are not swap operations, thus a similar performance to NATIVE-2 is achieved, and a speedup of 1.58X over the baseline configuration. AVA X4 achieves a speedup of 1.71X over the baseline configuration. For AVA X8, ... causing a slight performance degradation (1.64X)..."* —— 逐根报出图中肉眼可见的单个柱高数字，却缺乏跨 6 个负载的统合规律提炼。
  - `conf__micro__ZengKLJ21`（Turnpike, MICRO 2021, p10）：
    > *"Figure 21 shows the performance results of the following 8 cases... Turnstile: is the state-of-the-art work... incurs a 29% overhead... WAR-free Checking: ... reduces the overhead to 25%. Fast Release: ... reduces the overhead to 22%..."* —— 在结果段逐条解释 8 个冗长图例并逐一念数字，令读者陷入流水账。
- **跨引用一致性警戒**：即便在顶会标杆中，我们也实测捕获了 **3 处真实图文交叉引用错位**——`FireSim`（p11 将 Fig 11 误写为 `"Figure VI"`）、`Constable`（p11 §9.1.1 将 Fig 11 误引为 `"Fig. 14"`）、`Elastic Cuckoo`（p4 正文引 `Figure 4(a)/(b)` 但图中遗漏 `(a)(b)` 标号）。必须始终用 LaTeX `\ref{}` 生成编号并在终稿前逐一核验子图标号！

---

### 2.5 Table vs Figure vs Prose 决策边界

对 48 篇 `deep_read` 论文全部 **164 张表格** 按主题分类，得到了极具说服力的经验决策边界：

| 表格主题类别 | 数量（共 164 表） | 占比 | 典型实例 |
|---|---:|---:|---|
| 1. 系统/微架构/平台配置与仿真参数 | 67 | **40.9%** | `Swarm` Table 3, `CloudSuite` Table 1, `Elastic Cuckoo` Table 2, `SRS` Table III |
| 2. 评测负载、基准套件与输入特征 | 25 | **15.2%** | `Constable` Table 4, `Swarm` Table 4, `Whisper` Table 1, `Vector Runahead` Table 2 |
| 3. 硬件存储、面积、功耗、能耗与时序开销 | 24 | **14.6%** | `SALP` Table 1, `Eyeriss` Table IV, `Constable` Table 1, `SRS` Table IV–V, `LLM.265` Table II |
| 4. 定性特征对比、分类矩阵、协议规范、ISA/API 与符号表 | 21 | **12.8%** | `PVCoherence` Table 1, `StreamBox-HBM` Table 1, `Eyeriss` Table I & III, `M-ANT` Table I |
| 5. 纯定量实验主结果表（错误数/PPL/概率/QPS） | 9 | **5.5%** | `RowHammer` Table 5–7, `FireSim` Table III, `ρHammer` Table 6, `DynamoLLM` Table 1–2 |
| 6. 其他混合汇总表 | 18 | 11.0% | — |

**核心边界规则（Table vs Figure vs Prose）**：
1. **何时必须用 Table（而非 Figure 或 Prose）**：
   - **异构多维精确查表**（单位、类型各异，如核数/频率/L1/L2/ROB/DRAM 参数表、存储字节数逐模块累加表、协议状态转移 diff 表）——占全部表格的 **~83%**；
   - **极小样本跨量级精确数值**（如 `RowHammer` p11 Table 7 的 $1.4\times 10^{-11}$ vs $3.6\times 10^{-44}$，或 `Eyeriss` p8 Table IV 的 `200× / 6× / 2× / 1×`）；
   - **高阶融合技巧——热图表格（Heatmap Table）**：如 `conf__hpca__StojkovicZGTC25`（DynamoLLM, HPCA 2025, p3 Table 1），当既要看二维参数网格内的精确能耗数字（Wh），又要一眼识别 SLO 违约灰格与最优能耗带时，把逐行热图底色嵌入 booktabs 表格可一举两得。
2. **何时必须用 Figure（而非 Table）**：
   - 凡需展示**趋势、排序分布、相对比例、长尾 CDF、多维权衡前沿、结构空间拓扑或时序并发重叠**，一律用 Figure（超过 94% 的实验对比均采用 Figure 而非纯数字大表）。
3. **何时直接用 Prose（既不画图也不建表）**：
   - 若仅有 **2–4 个同维度标量**（例如 `"On average, PARA degrades performance by only 0.197% (max 0.745%)"`——`RowHammer` p11），直接写进一句简洁正文，绝不为 3 个数硬凑一张孤零零的柱状图或 2 行小表。

---

## 3. 面向 Phase 2 Skill 蒸馏的可执行视觉设计准则与提交前核查清单

以下全部规则直接源自阶段 A（20 篇/92 页 PNG）与阶段 B（48 篇全量统计）的双重实证，不依赖任何特定绘图工具，可直接蒸馏为体系结构论文写作 Skill 的视觉规范模块：

### 一、图表全局规划与预算准则
1. **预算护栏**：12–15 页体系结构顶会论文目标预算为 **12–16 张图 + 2–4 张表**（图与表之比约 4:1）；内容配比大致保持 **引言与动机 ~25% ：架构设计与机制 ~45–50% ：评估与敏感度 ~25–30%**。切忌少于 6 图硬塞 24 宫格（`AVA`），也忌超过 22 图搞单栏微缩条形码轰炸（`Turnpike`）。
2. **Figure 1 黄金位置**：务必在 **Page 2 结束前**亮出 Figure 1（68.8% 顶会惯例）。仅当 Figure 1 是强冲击力的“问题量化 + 目标愿景 Teaser / 范式对比 / 极短核心攻击代码”时才放 **Page 1**，绝不把教科书式背景图浪费在首页。
3. **Table / Figure / Prose 三分界**：参数配置、负载清单、硬件面积/存储开销与定性特性对比放 **Table**；趋势、分布、分解、权衡、结构与时序放 **Figure**；2–4 个孤立标量直接写进 **Prose**。

### 二、色彩、字体与版面铁律
4. **全篇语义调色板锁定（Semantic Palette Contract）**：开笔前先定义 3–5 色的低饱和度、色盲友好且灰度明度分明的配色表（如“基线 = 浅灰/中灰，本文主方案 = 深藏青/深teal，理想上限/强调 = 暖砖红或黑”），**严格贯彻全文所有图表，严禁跨图红蓝反转**（反例：`Pond` p13 Fig 20 vs Fig 21）。
5. **双重冗余编码**：任何 ≥2 组序列的图形都必须叠加第二视觉通道——折线图用**色相 + 线型（实/虚/点）+ 点型**；柱状图超 3 组时必须用**明度梯度 + 稀疏纹理（hatch）**，禁止 4–5 阶纯灰无纹理混排（反例：`SALP` Fig 13–15、`Elastic Cuckoo` Fig 15），禁止高饱和彩虹色、亮黄 `#FFFF00` 柱体以及无意义的一维渐变 colorbar（反例：`FastTTS` Fig 4）。
6. **单栏 vs 双栏尺度与字号底线**：图内所有文字在最终印刷尺寸下须 **≥ 7pt**；单栏图每组柱不超过 6–8 个横轴类别（测试集 ≥ 12 个一律升级双栏全宽）；严禁单栏内左右硬塞两张独立图（反例：`Turnpike` p3 Fig 3–4）或用 `wrapfigure` 环绕极窄文字。
7. **共享单一图例 & 轴标零冗余**：多子图共享同一套图例时，**只放一个总图例**（置顶或置右）；共享坐标轴时省略内部重复轴标题并确保相邻子图纵轴标尺一致（或显式分栏独立标出）。

### 三、微架构框图与实验图表专项工艺
8. **框图四要素**：(a) 从左到右或从上到下单向主数据流；(b) **实线 = 数据通路，虚线 = 控制/失效/元数据通路**；(c) 复杂系统用“宏观分层 + 虚线放大框”拆解，单盒内不超过 5–8 词；(d) 机制演进与状态变化一律用**具体实例 + 圆圈编号 `❶→❷→❸`（或 `(A)→(G)`）**并与正文内联同步。有真实流片、PnR 版图、Profiler 波形或终端输出时优先纳入。
9. **实验图五大高阶技巧**：
   - 个体测试集柱图按核心收益**升序或按套件分组排序**，并用**竖向虚线或浅灰底纹隔离 `GEOMEAN` 区** + 在汇总柱顶直标精确数值；
   - 优先使用**曲线/区域旁直接标注 + 差值箭头（`-36% ↓`）**替代远距图例；
   - 遇到单一极端离群值时，锁定主体纵轴并在出界处**诚实直标真实数值（如 `117×`、`max 124%`）**；
   - 严禁画**饼图**、严禁画 **>6 层堆叠柱**、严禁用**连续折线连接无序离散测试集**、审慎对待双 y 轴（若必须用，仅限因果强相关的两项且清晰标注左右轴归属与单位）；
   - 纵轴诚实性：默认从 `0` 开始；若归一化加速/开销必须局部放大，须标出 `1.0` 基准虚线与精确数字，或对大跨度空白使用显式断轴符号 `//`。

### 四、表格、图注与图文耦合准则
10. **Booktabs 极简表格工艺**：强制 `\toprule` / `\midrule` / `\bottomrule` + `\cmidrule` 分组，**绝对零竖线、零糖果彩色斑马底纹**（最多用 5% 极淡灰隔行）；文本左对齐、数字右对齐并加千分位逗号、统一合理有效数字（通常 1–2 位小数）、仅加粗本文行或每行最优/最差值并在表注写明加粗含义。
11. **“标题 + 回链 + 结论”图注公式**：推荐长度 **15–35 词（1–2 句）**——首句点明变量与对象（跨页复杂图附 `(§X.Y)`），次句直给核心定量或定性 takeaway；表注保持 **7–15 词**精准概括。避免 3–4 词哑巴图注，也避免 >60 词图例字典型图注。
12. **正文耦合“三拍法”**：(1) 用克制动词引入（`shows / illustrates / compares / plots / summarizes`）；(2) 框图按 `❶→❷→❸` 逐步导读，数据图先提炼 **2–3 条编号核心观察（Observations / Findings）**；(3) 深入解释现象背后的**微架构/系统机理与异常负载归因**，绝不逐根复述柱高数字。

### 五、终稿提交前 60 秒视觉核查清单（Pre-Submission Visual Audit）
- [ ] **黑白打印抽检**：将整篇 PDF 转为灰度查看，所有曲线、柱体与热图是否依然 100% 可辨？
- [ ] **跨图色彩一致性核对**：同一基线与本文方案在 Fig 1 至最后一图中的颜色、纹理、图例顺序是否完全一致、无反转？
- [ ] **矢量图拼写与单位审查**：人工逐字朗读每张图内坐标轴、盒内文字与表内单位，清除 `Efficiecny` / `Lantecy` / `Bit Fsuion` / 缺平方 `mm` / 空格不统一等隐蔽错误？
- [ ] **零碰撞与完整性核查**：是否存在文字撞框、刻度粘连（`128256512`）、标签压图注、图内曲线/颜色漏进图例、或坐标轴缺失单位？
- [ ] **图文编号双向核对**：正文所有 `Fig. X(a)` / `Table Y` 是否与实际图表号、子图标号及步骤徽章 `❶–❺` 一一对应且无重号/错号？
- [ ] **图注独立可读测试**：只看全部图、表与 Caption（不读正文），能否在 3 分钟内完整复述本文的动机、设计与核心实验结论？

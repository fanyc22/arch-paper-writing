# 维度 6 & 维度 10 深度分析报告：计算机体系结构顶会论文用词、命名体系、LaTeX 微排版与三桶批判性反例库

> **研究定位与数据边界**：本报告对应 Phase 1B 的 **Dimension 6（用词、专业用语、命名体系与 LaTeX 微排版）** 与 **Dimension 10（批判性好坏对照与人类/AI 反例库）**，与逐字核验原文库 `exemplar_bank.md`（`EX-01`–`EX-46`）配套产出。所有量化统计与引文均基于：
> 1. **`deep_read` 深度精读池（48 篇，总词数 516,069 词）**：细分 4 个子层——`exemplar_pre2023`（2011–2022 标杆，22 篇，232,182 词）、`exemplar_2023plus`（2023–2026 标杆，10 篇，118,187 词）、`contrast_ordinary`（2015–2022 人类普通/弱文对照，10 篇，101,817 词）、`contrast_post2023`（2024–2026 后 LLM 时代 AI 污染对照，6 篇，63,883 词）；人工精读覆盖 44+ 篇原文页面，原文库收录 **43 篇不重复 `deep_read` 论文**的 46 条逐字摘录。
> 2. **`macro_pool` 宏观统计池（152 篇，总词数 1,582,805 词）**：覆盖 ISCA / MICRO / HPCA / ASPLOS 各 38 篇，跨越 `2011-2015`（47 篇）、`2016-2022`（65 篇）、`2023-2026`（40 篇）三大时代。
> 3. **`post2023_ai_marker_hits.json` 专项扫描集**：2024–2026 四大顶会中命中高频 AI 词汇标记的 152 篇论文及上下文片段。
> 4. **严格隔离承诺**：全过程零接触、零引用 `manifest.json` 中的 8 篇 `held_out_test` 隔离测试论文。所有原文引述格式统一为 `(ShortName, VENUE YEAR, paper_id, p. X)`，页码与文本均已对照 `corpus/macro_cache/<paper_id>.json` 逐字核实。

---

## 0. 核心发现与三桶批判框架（Executive Summary）

研究计算机体系结构顶会写作，首要认知纪律是：**“绝不能因为一篇论文发表在 ISCA/MICRO/HPCA/ASPLOS，甚至拿了 Best Paper，就默认它的每一段英文都值得模仿。”** 我们的定量扫描与 44+ 篇逐页精读揭示，顶会论文语言质量必须严格划分为**三个批判性桶（Three Buckets）**：

| 批判桶位 | 原文库标签 | 语料对应层 | 核心语言肖像与对待原则 |
| :--- | :---: | :--- | :--- |
| **Bucket 1：纯人工精工标杆** | `[GOLD-HUMAN]` | `exemplar_pre2023` 主体 + 干净的 `exemplar_2023plus`（如 `Pond`, `HFI`, `Constable`） | 极高机制信息密度、具体微架构动作动词、显性因果逻辑（`because/instead/hence`）、克制的量化边界与优雅破折号插入语——**Phase 2 唯一正面模仿基准** |
| **Bucket 2：Class A 人类差文与标杆瑕疵** | `[BAD-HUMAN]` / `[EXEMPLAR-FLAW]` | `contrast_ordinary`（10 篇全检出）+ 预 2023 标杆的局部硬伤（`SIGMA`, `Eyeriss`, `Whisper`, `Chasing Carbon`, `SolarCore`） | **超高被动语态墙（123.95/万词）**、母语直译病句、缩略词字母汤撞车、中途改名、零数字摘要、防御性审稿补丁、编辑残留——**人类作者常见失误，需定点纠偏** |
| **Bucket 3：Class B 后 2023 AI 污染文** | `[AI-TAINTED]` / `[EXEMPLAR-FLAW]` | `contrast_post2023`（6 篇全检出）+ 已发生 AI 润色渗漏的 2025–2026 获奖论文（`PF-LLM`, `DynamoLLM`, `LLM.265`） | 表面主动语态（被动仅 **61.52/万词**，全组最低），实则充斥虚浮包装动词（`enhance` **22.6×**、`facilitate` **22.0×**）、宏大紫文开场、分词拖尾（`, ensuring` **15.7×**、`, enabling` **7.0×**）、`Challenge I/II/III` 模具与**缝合断层（Frankenstein Seam）**——**Phase 2 硬红线拦截对象** |

### 五大颠覆性实证发现

1. **Class A 与 Class B 沿“被动语态轴”彻底反向分裂**：`contrast_ordinary`（人类差文）的被动语态（`be + V-ed/en`）高达 **123.95 / 万词**，比纯人工标杆（**88.55**）高 40%；而 `contrast_post2023`（AI 污染文）却骤降至 **61.52 / 万词**。这说明 LLM 会制造一种“表面主动流畅、实则空洞无物”的伪流畅假象（用 `enhances / facilitates / empowers / ensures` 代替具体硬件动作），审查系统不能仅靠“降被动”判断是否好文。
2. **因果语法大反转——纯人工讲 `because`，AI 爱贴 `, enabling / , ensuring / Additionally,`**: 对比 `exemplar_pre2023` 与 `contrast_post2023`，朴素因果连词 `because` 从 **10.98 暴跌至 3.29 / 万词（-3.3×）**，`since` 从 **8.70 跌至 4.07**，`instead` 从 **3.62 跌至 1.41**；与此同时，空洞分词尾缀 `, ensuring` 暴涨 **15.7×**（`0.09 → 1.41`），`, enabling` 暴涨 **7.0×**（`0.56 → 3.91`），句首 `Additionally,` 暴涨 **10.0×**（`0.39 → 3.91`），`not only ... but also` 暴涨 **3.4×**（`0.56 → 1.88`）。
3. **“长破折号（em-dash）= AI 味”在体系结构顶会中被彻底证伪**：剔除 IEEE 模板自带的 `Abstract—` 与 `Index Terms—` 后，纯正文 Unicode 长破折号（`—`）密度呈现完全相反的梯度：`exemplar_pre2023` **8.66 / 万词**、`exemplar_2023plus` **8.21 / 万词**、`contrast_ordinary` **6.09 / 万词**，而 `contrast_post2023` 反而最低，仅 **2.19 / 万词**（相差 **4.0 倍**！）。母语资深架构师（`Clearing the Clouds`, `Swarm`, `RowHammer`, `Pond`, `HFI`）极擅长用成对或后置长破折号完成紧凑定义与机制解释。
4. **2025–2026 顶会 Best Paper 已出现显著 AI 润色渗漏（Award-Paper AI-Drift）**：ASPLOS 2026 Best Paper `PF-LLM` 在 `7.1` 小节误贴一整段 131 词的 GPT 总章节导语（`"In this section, we delve into the rationale ... broader landscape"`，见 `EX-33`）；HPCA 2025 Best Paper `DynamoLLM` 首页密集命中 10 处/7 类 AI 标记词（`pivotal`, `paramount`, `underscores`, `To pave the way`, `seamlessly`, `holistic`）同时伴随 `"and other."` 与 `"an 40%"` 笔误（`EX-11`）；MICRO 2025 Best Paper `LLM.265` 全篇摘要零数字且 p. 10 残留 `<latexit>` XML 标签（`EX-04`）。**2023+ 标杆层不再天然纯净，必须经由 2011–2022 纯人工基准校准。**
5. **AI 味检测必须坚持“多信号共现 + 搭配上下文”，严防领域专有名词误杀**：在 `post2023_ai_marker_hits.json` 的 152 篇 2024–2026 论文中，单字 `realm` 多次命中合法的体系结构专有名词——ARM CCA 官方硬件隔离状态 `Realm Management Extension (RME)` / `the Realm`（`conf__asplos__ChoiCJK26`, `conf__asplos__YangQRLYNG26`）与 `Google’s REALM`（`conf__isca__JiangSGAYD25`）；2014 标杆 `PVCoherence` 中的 `delve` 则是真诚克制的否定句 `"we intentionally do not delve deeply"`（`EX-16`）。

---

## 1. 体系结构原生词库与搭配色谱（Domain-Native Lexicon & Collocation Palette）

### 1.1 动词体系：具体微架构动作动词 vs 膨胀包装动词

体系结构写作最本质的语言美学是**“主语是具体硬件/软件实体，动词是物理或协议层可观测动作”**。以下实证表汇总了 48 篇 `deep_read` 论文（按每万词频次与出现论文数）中“膨胀/包装动词”与“体系结构本位动词”的断层分化：

#### 表 1-1：膨胀/包装动词在四个语料子层的分布（每万词频次 [出现篇数]）

| 动词（词族） | `exemplar_pre2023` (n=22) | `exemplar_2023plus` (n=10) | `contrast_ordinary` (n=10) | `contrast_post2023` (n=6) | AI 组 / 纯人工标杆倍率 | 诊断结论 |
| :--- | :---: | :---: | :---: | :---: | :---: | :--- |
| `enhance` | 0.34 (8) | 1.69 (4) | 0.29 (3) | **7.67 (6/6)** | **22.6×** | 头号空心包装动词（全组 100% 论文泛滥） |
| `facilitate` | 0.22 (5) | 0.93 (5) | 0.10 (1) | **4.85 (6/6)** | **22.0×** | 典型 LLM 官腔，掩盖真实机制动作 |
| `underscore` | 0.04 (1) | 0.25 (3) | 0.10 (1) | **1.10 (4/6)** | **27.5×** | 后 2023 标配“强调”词，2023+ 标杆亦已渗入 |
| `delve` | 0.04 (1)* | 0.17 (2) | 0.00 (0) | **1.10 (3/6)** | **27.5×** | 预 2023 唯一命中系否定句 `do not delve` |
| `empower` | 0.00 (0) | 0.08 (1) | 0.00 (0) | **1.10 (1/6)** | **∞** | 纯商业/LLM 宣传词，纯人工标杆为 0 |
| `streamline` | 0.00 (0) | 0.00 (0) | 0.00 (0) | **0.63 (2/6)** | **∞** | 纯 LLM 润色词 |
| `foster` | 0.04 (1) | 0.00 (0) | 0.00 (0) | **0.63 (3/6)** | **15.8×** | 非体系结构语域动词 |
| `navigate` | 0.09 (2) | 0.00 (0) | 0.00 (0) | **1.10 (2/6)** | **12.2×** | 隐喻滥用（`navigate the trade-off/space`） |
| `mitigate` | 1.21 (9) | 4.65 (8) | 2.36 (3) | **5.32 (6/6)** | **4.4×** | 仅安全/RowHammer 语境合理，勿滥用替代 `reduce/avoid` |
| `enable` | 5.30 (21) | 14.30 (10) | 8.35 (9) | **12.68 (6/6)** | **2.4×** | 2023+ 整体明显通胀，尤须警惕 `, enabling` 拖尾 |
| `utilize` | 2.63 (15) | 4.65 (7) | 4.32 (6) | **5.17 (6/6)** | **2.0×** | 纯人工偏好直接用 `use`；`utilize` 仅在谈硬件利用率时合理 |
| `leverage` | 1.90 (14) | 4.40 (8) | 4.32 (9) | **3.76 (6/6)** | **2.0×** | 人类差文与 AI 均爱滥用，应限额 ≤ 2 次/千词 |

#### 表 1-2：纯人工标杆高频使用的体系结构本位强动词（按语义家族与每万词频次）

| 语义家族 | 本位强动词（`exemplar_pre2023` 每万词频次 [篇数]） | `contrast_post2023` 频次 | 语料实证地道搭配（精确出处） |
| :--- | :--- | :---: | :--- |
| **流水线与乱序执行** | `stall` (4.82 [9]), `squash` (3.92 [4]), `retire` (0.95 [6]), `speculate` (0.60 [4]), `dispatch` (0.52 [2]), `serialize` (0.39 [4]) | `stall` 1.88 / `squash` 0.00 / `retire` 0.16 / `dispatch` 0.00 | `spend the majority of their time stalled` (`Vector Runahead`, ISCA'21, `conf__isca__NaithaniA0E21`, p. 1); `destined to be squashed` (`InvisiSpec`, MICRO'18, `conf__micro__YanCS0FT18`, p. 1); `serialize requests that can potentially be served in parallel` (`SALP`, ISCA'12, `conf__isca__KimSLLM12`, p. 1) |
| **存储层次、缓存与内存** | `evict` (0.90 [9]), `bypass` (1.12 [8]), `invalidate` (0.52 [4]), `flush` (0.47 [7]), `coalesce` (0.30 [4]), `remap` (0.17 [2]), `reclaim` (0.17 [1]), `prefetch` (6.98) | `invalidate` 0.16 / `coalesce` 0.16 / `reclaim` 0.00 / `remap` 0.16 | `bypasses the LLC-SB and accesses main memory` (`InvisiSpec`, MICRO'18, `conf__micro__YanCS0FT18`, p. 9); `coalesce many sandbox teardowns into one large teardown` (`HFI`, ASPLOS'23, `conf__asplos__NarayanGTRM0FVL23`, p. 11); `pack multiple Page Table Entries (PTEs) into a single TLB entry` (`RMM`, ISCA'15, `conf__isca__KarakostasGACHM15`, p. 2) |
| **并行、隐藏与带宽调度** | `exploit` (5.38 [17]), `overlap` (3.70 [13]), `interleave` (0.99 [7]), `hide` (0.90 [10]), `saturate` (0.78 [7]), `mask` (0.69 [3]), `amortize` (0.30 [3]), `throttle` (0.26 [2]) | `exploit` 2.35 / `interleave` 0.31 / `amortize` 0.00 / `mask` 0.16 / `throttle` 0.16 | `hiding the serialization of dependent loads` (`Vector Runahead`, ISCA'21, `conf__isca__NaithaniA0E21`, p. 10); `amortize the cost of hfi_enter` (`HFI`, ASPLOS'23, `conf__asplos__NarayanGTRM0FVL23`, p. 11); `starve the out-of-order core of reorder buffer and issue queue resources` (`Vector Runahead`, ISCA'21, p. 10) |
| **硬件监控、追踪与开销归因** | `track` (4.09 [15]), `incur` (3.36 [18]), `eliminate` (2.71 [11]), `suffer` (1.55 [15]), `trigger` (1.46 [12]), `expose` (1.25 [11]), `dominate` (1.21 [8]) | `track` **0.16** / `incur` **1.10** / `eliminate` **0.63** / `dominate` **0.31** | `tracks modifications to the source architectural registers` (`Constable`, ISCA'24, `conf__isca__BeraRRMNGOKSSM24`, p. 6); `expose the vulnerability of commodity DRAM chips` (`RowHammer`, ISCA'14, `conf__isca__KimDKFLLWLM14`, p. 1); `without incurring significant delays` (`Clearing the Clouds`, ASPLOS'12, `conf__asplos__FerdmanAKVAJKPAF12`, p. 2) |

> **关键观察**：对比两表可以看到惊人的语义空心化现象——`contrast_post2023` 组在 `track`（`4.09 → 0.16`，下降 **25.6×**）、`incur`（`3.36 → 1.10`）、`dominate`（`1.21 → 0.31`）、`eliminate`（`2.71 → 0.63`）、`amortize`（`0.30 → 0.00`）等具体因果与机制动词上全面萎缩，取而代之的是 `enhance`（**7.67**）、`facilitate`（**4.85**）、`optimize`（**6.73**）这类万金油抽象动词。

#### 表 1-3：“膨胀/包装动词 → 体系结构本位动词”替换配方

| 禁用/限流动词 | 常见空洞语境 | 精准本位替换（按具体硬件语义选择） |
| :--- | :--- | :--- |
| `enhance` | `enhance performance / locality / efficiency` | `improve`, `increase`, `boost`, `raise`, `extend`（或直接写清指标：`cuts latency by X%`, `raises LLC hit rate`） |
| `facilitate` | `facilitate communication / debugging / sharing` | `support`, `allow`, `let`, `simplify`, `speed up`, `carry out` |
| `utilize` | `utilizes an on-chip buffer / TaskID` | `uses`, `reads`, `consults`, `indexes`（`utilize` 仅在谈资源利用率如 `under-utilized` 时使用） |
| `leverage` | `leverages hardware support / observation` | `uses`, `exploits`, `builds on`, `relies on`, `repurposes` |
| `enable`（泛滥时） | `... , enabling efficient execution` | 改为独立主句或具体动作：`allows X to Y`, `lets the core overlap...`, `removes the serialization between...` |
| `mitigate`（非安全/错纠语境） | `mitigate latency / memory overhead` | `reduce`, `hide`, `mask`, `amortize`, `cut`, `eliminate`, `curb` |
| `underscore` / `highlight` | `Our results underscore the importance of...` | `show`, `demonstrate`, `confirm`, `indicate`, `point to` |
| `delve into` | `we delve into the inner workings of...` | `we detail`, `we describe`, `we examine`, `we analyze`, `Section 4 presents` |
| `empower` / `foster` / `streamline` | `empowers designers / streamlines execution` | `lets designers`, `simplifies`, `cuts`, `automates`, `eliminates manual...` |

---

### 1.2 认识论克制与权威对冲（Authentic Hedging & Understated Authority）

顶尖体系结构论文的权威感从不来自“革命性、前所未有、完美平衡”等营销修辞，而来自**精确的边界界定、坦诚的局部限制与冷静的数量级估算**。四组语料的量化对比清晰展现了纯人工标杆的克制色谱：

| 认识论/边界表达 | `exemplar_pre2023` | `exemplar_2023plus` | `contrast_ordinary` | `contrast_post2023` | 纯人工地道用法实证 |
| :--- | :---: | :---: | :---: | :---: | :--- |
| `up to` | **4.44** | **4.23** | 4.13 | **1.41** | 明确区分峰值与均值：`reduces ... by up to 40%`；绝不把峰值当常态 |
| `typically` | **2.45** | **2.28** | 0.88 | 3.76 | 表达常见工程现实：`typically suffer from extreme limitations` (`PVCoherence`, HPCA'14, p. 2) |
| `roughly` | **0.90** | 0.08 | 0.29 | **0.00** | 资深架构师做一阶量级估算：`split the die area into two roughly equal parts` (`Clearing the Clouds`, ASPLOS'12, p. 2) |
| `modest` | **0.86** | 0.42 | 0.49 | **0.16** | 克制描述硬件开销或收益：`modest number of entries` (`RMM`, ISCA'15, p. 1)；`impact ... is modest` (`DynamoLLM`, HPCA'25, p. 10) |
| `in practice` | **0.56** | **0.68** | 0.29 | 0.47 | 区分理论抽象与硬件现实：`In theory, ... In practice, however, resources are physically distributed` (`Amdahl's Law Market`, HPCA'18, p. 1, `EX-36`) |
| `for most` | **0.56** | 0.34 | 0.59 | **0.00** | 限定适用负载集合，主动留出例外空间 |
| `at the cost of` | **0.43** | 0.25 | 0.59 | 0.47 | 显式写出体系结构权衡代价：`high parallel throughput at the cost of poor single thread performance` (`MorphCore`, MICRO'12, p. 1, `EX-15`) |
| `conservatively` | **0.43** | 0.17 | **0.00** | **0.00** | 建模假设向不利于自己的方向取整以增强可信度（人类差文与 AI 组均为 **0.00**！） |
| `intuitively` / `ideally` | **0.30 / 0.26** | 0.08 / 0.42 | 0.10 / 0.10 | 0.16 / **0.00** | 先给直觉或理想上限再落回现实折损（`In the ideal case, ... However, this is often not achievable`） |

**三种权威姿态的鲜明对比**：
- **纯人工克制权威（`[GOLD-HUMAN]`）**：主动亮出短板与假设边界。例如 `RowHammer`（ISCA'14, `conf__isca__KimDKFLLWLM14`, p. 1, `EX-03`）在 110/129 模组全部出错的震撼数据后，仅冷静下结论 `"many deployed systems are likely to be at risk"`；`Darwin`（ASPLOS'18, `conf__asplos__TurakhiaBD18`, p. 10, `EX-26`）在 15,000× 加速背后坦承 `"always limited by the DRAM bandwidth ... (64% of theoretical maximum)"`；`HFI`（ASPLOS'23, `conf__asplos__NarayanGTRM0FVL23`, p. 12, `EX-27`）直言 `"HFI’s overhead is slightly larger than MPK-based protections, which range from 1.9% to 5.3%. This is because HFI takes a few cycles to move metadata..."`；`Pond`（ASPLOS'23, `conf__asplos__LiBHEZNSRLAHFB23`, p. 13, `EX-32`）在结论中写明 `"assuming CXL increases latency by 222%"`。
- **Class A 人类弱对冲/防御退缩（`[BAD-HUMAN]`）**：双重弱对冲叠床架屋（`"can potentially benefit"`，`StreamBox-HBM`, ASPLOS'19, `conf__asplos__MiaoJPML19`, p. 13, `EX-34`），或生硬的防御性退让（`"We do not consider graph processing in this paper because we do not innovate in this context."`，`ChoPIM`, ISCA'20, `conf__isca__ChoKLE20`, p. 4, `EX-35`）。
- **Class B AI 浮夸零边界（`[AI-TAINTED]`）**：滥用绝对化自夸形容词（`"strikes the perfect of such a balance"`, `"breakthrough effectiveness"`, `"valiant efforts"`，`ρHammer`, MICRO'25, `conf__micro__ChenTTLZQ25`, p. 1/9；`"harmonizing the delicate balance"`, `"marks a pivotal advancement"`，`QPlacer`, ISCA'25, `conf__isca__Zhang0D0AO0B0025`, p. 2, `EX-46`；`"Comprehensive evaluation shows"`，`FastTTS`, ASPLOS'26, `conf__asplos__ChenML0MLF26`, p. 1）。

---

### 1.3 原生因果、转折与让步句法库（Causal, Contrast & Concession Repertoire）

这是本报告最具操作价值的句法统计发现之一：**纯人工标杆依赖“显性从属因果 + 短句平推”，而 AI 污染文依赖“句首累加胶水词 + 句尾现在分词悬垂拖尾”**。

#### 表 1-4：因果、转折与衔接标记在四个子层的频次对比（每万词）

| 逻辑类别 | 表达形式 | `exemplar_pre2023` | `exemplar_2023plus` | `contrast_ordinary` | `contrast_post2023` | 变化趋势与诊断 |
| :--- | :--- | :---: | :---: | :---: | :---: | :--- |
| **纯人工偏爱：显性直接因果** | `because` | **10.98** | 6.68 | **11.59** | **3.29** | AI 组骤降 **3.3×**（宁可用 `, thereby ...ing` 也不直说 `because`） |
| | `since` | **8.70** | 5.84 | **9.13** | **4.07** | AI 组下降 **2.1×** |
| | `hence` | **2.63** | 1.61 | 1.28 | **0.63** | 纯人工最爱的简洁推理词，AI 组下降 **4.2×** |
| | `as a result` | **2.02** | 1.86 | 2.06 | **0.63** | AI 组下降 **3.2×** |
| **纯人工偏爱：锐利对比与真实遗憾** | `instead` | **3.62** | 2.79 | 2.75 | **1.41** | 方案替代转折核心词，AI 组下降 **2.6×** |
| | `whereas` | **0.95** | **1.52** | 0.98 | **0.16** | 精确二分对比，AI 组几近消失（降 **5.9×**） |
| | `unfortunately` | **1.42** | **1.44** | 0.98 | **0.31** | 纯人工引出架构痛点的王牌过渡词（`SALP`, `InvisiSpec`, `PVCoherence`），AI 组降 **4.6×** |
| **AI 偏爱：句首机械累加胶水** | `Additionally,` | 0.39 | 1.69 | 1.67 | **3.91** | AI 组暴涨 **10.0×**！典型“逐点灌水”信号 |
| | `Consequently,` | 0.82 | 1.10 | 0.59 | **2.03** | AI 组上涨 **2.5×** |
| | `Moreover,` | 1.64 | 0.93 | 0.98 | **2.66** | 过度依赖句首副词强行粘合松散句子 |
| | `Furthermore,` | 1.55 | 1.52 | 1.57 | **2.50** | 同上 |
| **AI 偏爱：分词拖尾与伪对称** | `, ensuring` | 0.09 | 0.00 | 0.20 | **1.41** | AI 组暴涨 **15.7×**！（如 `QPlacer` p. 2: `..., ensuring frequency domain isolation`） |
| | `, enabling` | 0.56 | 0.93 | 0.29 | **3.91** | AI 组暴涨 **7.0×**！（如 `FastTTS` p. 1: `..., enabling edge LLMs...`） |
| | `, thereby ...ing` | 0.73 | 0.59 | 0.59 | **1.72** | AI 组暴涨 **2.4×**（6/6 篇全部出现！） |
| | `not only ... but also` | 0.56 | 0.59 | 0.79 | **1.88** | AI 组暴涨 **3.4×**，常用于空洞双夸句 |
| | `despite` | 0.90 | 0.85 | 0.59 | **2.50** | AI 组暴涨 **2.8×**（`Despite its great potential / transformative potential...`） |
| | `while` | 12.27 | 16.25 | 16.99 | **18.78** | 过度用 `While X, Y` 替代清晰分句 |

> **段落逻辑启示**：精读 `Amdahl's Law Market`（HPCA'18, `conf__hpca__ZahediLL18`, p. 1, `EX-36`）与 `SRS`（HPCA'23, `conf__hpca__WooSN23`, p. 6, `EX-37`）可见，顶级纯人工段落**几乎不用 `Additionally / Moreover / Furthermore`**，而是靠 **Given-Before-New 词汇链**（把前句尾部的新概念自然提为下句主语）与 **平行结构**（`With reservations, ... With priorities, ... Finally, with entitlements, ...`）实现丝滑衔接。

---

## 2. 命名体系与术语卫生（Naming Systems & Terminology Hygiene）

### 2.1 系统与方法命名模式（48 篇 `deep_read` 全量分类）

对 `deep_read` 全部 48 篇论文的标题与核心系统名逐一归类，得到极有说服力的分布规律：

| 命名策略 | 总数 (/48) | `exemplar` (/32) | `contrast_ordinary` (/10) | `contrast_post2023` (/6) | 典型案例与评估 |
| :--- | :---: | :---: | :---: | :---: | :--- |
| **1. 朴素英文词/隐喻/专名**（Plain / Metaphoric） | **10** | **8** (25.0%) | 1 | 1 | `Pond` (ASPLOS'23), `Whisper` (MICRO'22), `Constable` (ISCA'24), `Swarm` (MICRO'15), `Darwin` (ASPLOS'18), `GhostRider` (ASPLOS'15), `Contiguitas` (ISCA'23), `DaDianNao` (MICRO'14) —— **极易读易记、口头讨论友好** |
| **2. 语义复合/混成词**（Coined Compound） | **18** | **10** (31.3%) | 5 | 3 | `FireSim` (ISCA'18), `MorphCore` (MICRO'12), `InvisiSpec` (MICRO'18), `Eyeriss` (ISCA'16), `Graphicionado` (MICRO'16), `LLM.265` (MICRO'25), `SolarCore` (HPCA'11), `PVCoherence` (HPCA'14), `DynamoLLM` (HPCA'25) —— **体系结构第一大主流，一眼看懂领域** |
| **3. 干净技术首字母缩写**（Clean Initialism） | **8** | **6** (18.8%) | 2 | 0 | `SALP` (Subarray-Level Parallelism, ISCA'12), `RMM` (Redundant Memory Mappings, ISCA'15), `SRS` (Secure Row-Swap, HPCA'23), `HFI` (ASPLOS'23), `SIGMA` (HPCA'20), `PF-LLM` (ASPLOS'26) —— **逐词对应真实机制，不硬凑梗** |
| **4. 强行凑梗的反向缩略词**（Forced Backronym） | **2** | **0** (0.0%) | **0** | **2** (33.3%) | `PICACHU` (**P**lug-**I**n **C**GR**A** **H**andling **U**pcoming..., ASPLOS'25, `EX-06`); `M-ANT` (**M**athematically **A**daptive **N**umerical **T**ype, HPCA'25, 且正文自己拼成 `MANT`, `EX-39`) —— **100% 落入反例池，标杆组为 0！** |
| **5. 纯描述性机制/研究标题（无自造系统名）** | **10** | **8** (25.0%) | 2 | 0 | `Vector Runahead` (ISCA'21), `Autonomous NIC Offloads` (ASPLOS'21), `Elastic Cuckoo Page Tables` (ASPLOS'20), `Flipping Bits in Memory Without Accessing Them` (ISCA'14), `Clearing the Clouds` (ASPLOS'12), `Chasing Carbon` (HPCA'21) —— **高达四分之一标杆根本不造炫酷名字！** |

**核心命名铁律**：
1. **朴素清晰胜过强行造词**：如果技术本身就是一句清晰的名词短语（如 `Vector Runahead`、`Elastic Cuckoo Page Tables`、`Autonomous NIC Offloads`），**不要为了“显得像系统论文”而强塞一个尴尬缩略词**。
2. **严禁 Forced Backronym**：若缩写需要塞进 `Handling Upcoming`（`PICACHU`）或生硬副词 `Mathematically`（`M-ANT`）才能勉强拼出彩蛋词，或使用难以在论文讨论中正常拼读/键入的希腊符号（`ρHammer` 在不同 PDF 抽取中易乱码且无法直接 ASCII 检索），应立即放弃，改用 1–2 音节朴素英文词（如 `Pond`, `Swarm`, `Constable`）或直观复合词（如 `FireSim`, `InvisiSpec`）。

### 2.2 硬件组件名、小节标题与修饰词链卫生

1. **小节标题风格实证**：
   - 在 48 篇深度语料的标题清洗统计中，纯人工标杆的小节标题平均长度为 **3.65 词（预 2023）**与 **3.86 词（2023+）**，典型特征是**“朴素 2–4 词实义名词短语”**或**“部件/机制：核心动作”**（例如 `SALP`, ISCA'12, `conf__isca__KimSLLM12`, p. 2–7：`2.2 Timing Constraints`, `2.3 Subarrays: Physical Organization of Banks`, `5.1 SALP-1: Relaxing tRP`, `5.2 SALP-2: Per-Subarray Row-Address Latches`, `5.4 Exposing Subarrays to the Memory Controller`）。
   - 反观 `contrast_post2023`，其正文中**冒号总密度飙升 55%**（**128.20 / 万词** vs 其他三组惊人一致的 **82.07–82.60 / 万词**），核心驱动正是机械套用 `Challenge I: ...` / `Challenge-1: ...` / `Solution: ...` / `Takeaway 1: ...` 模板（`challenge_lbl` 标记密度在 `contrast_post2023` 达 **1.72 / 万词**，是 `exemplar_pre2023` 0.04 的 **43 倍**！）。
2. **硬件组件名：拒绝自造华丽概念，优先功能直译**：
   - 优秀示范：`Constable`（ISCA'24, `conf__isca__BeraRRMNGOKSSM24`, p. 6, `EX-22`）把被检测的稳定访存直接命名为朴素的 `likely-stable` load，把两张小硬件表直接叫 `Register Monitor Table` 与 `Address Monitor Table`；`InvisiSpec`（MICRO'18, `conf__micro__YanCS0FT18`, p. 9, `EX-20`）把乱序识别计数器直接叫 `Epoch ID`，把缓冲叫 `circular buffer`；`RMM`（ISCA'15, p. 1）直接叫 `range table` 与 `range TLB`。
3. **三词以上连字符修饰链（Modifier Chains）的精细辨析**：
   - 统计 48 篇中 3 词以上连字符短语（`h3`）均值：`exemplar_pre2023` 为 **13.4 次/篇**，`exemplar_2023plus` 升至 **19.8 次/篇**。但逐条检视样本必须区分两类：
     - **合法行业固化复合形容词**：`out-of-order`（`MorphCore` 44 次中绝大部分为此）、`state-of-the-art`、`end-to-end`、`just-in-time`、`out-of-bounds`、`out-of-sequence`、`ahead-of-time`——属于体系结构固定术语，不必机械拆分。
     - **需压制的非固化多层前置堆叠**：如 `Whisper`（MICRO'22 Best Paper，全语料最高 **58 处**，`EX-41`）密集堆叠 `novel profile-guided ...`, `hard-to-predict`, `locally-optimal` 与 10 词术语名 `Read-Once Monotone Boolean Formulas with Implication and Converse Non-Implication`；`Constable`（34 处）出现 `load-data-dependent instructions`, `hard-to-scale hardware`；`PICACHU`（29 处）出现 `plug-in coarse-grained reconfigurable accelerator`。原则：**非固化前置定语链超过 2 个连字符时，优先拆成后置介词短语或定语从句**（如 `instructions that depend on load data` 优于 `load-data-dependent instructions`）。

### 2.3 术语锁定与缩略词预算（Terminology Locking & Acronym Hygiene）

在 48 篇 `deep_read` 中，独立大写缩略词数量中位数在预 2023 标杆为 **13 个/篇**（均值 13.3），2023+ 标杆升至 **17 个/篇**（均值 20.5，主要因现代云/AI/PIM 论文同时横跨硬件与系统栈，如 `Pond` 41 个、`Autonomous NIC Offloads` 41 个、`UPMEM PIM` 39 个）。**真正摧毁可读性的不是行业标准缩写（`DRAM`, `TLB`, `LLC`, `CXL`, `NUMA`），而是“本文新造的撞车缩写”与“中途漂移/改名”**：

| 术语卫生事故类型 | 真实语料铁证（精确出处） | 危害诊断与硬规则 |
| :--- | :--- | :--- |
| **1. 同族新造缩写字母汤撞车** | `AVA` (`conf__hpca__LazoRMBVSCUC22`, HPCA'22, p. 2/5, `EX-23`) 同篇塞入 `VRF`, `P-VRF`, `M-VRF`, `VVR`, `VRLT`, `FRL`, `PFRL`, `MVL`, `RAC`——7 个 V/F/R/L 排列组合 | 读者被迫每两句回翻定义表。**规则**：本文**新造**硬件表/部件缩写全篇上限 **≤ 5 个**，且严禁在相邻模块中制造仅差一两字母的视觉撞车缩写。 |
| **2. 中途临时改名（Mid-Paper Rename）** | `Eyeriss` (`conf__isca__ChenES16`, ISCA'16 Top Picks, p. 4 vs p. 9)：p. 4 定义 `SOC-MOP, MOC-MOP, MOC-SOP`，p. 9 突然宣布 `"To save space, the SOC-MOP, MOC-MOP and MOC-SOP OS dataflows are renamed as OSA, OSB and OSC, respectively."` | 强迫读者建立双重映射表。**规则**：若绘图空间放不下长名，**从第一次引入时**就定为简洁名，绝不中途换马甲。 |
| **3. 中途劫持重定义旧缩写** | `Turnpike` (`conf__micro__ZengKLJ21`, MICRO'21, p. 2)：`"Turnstile leverages its SB as a gated store buffer (GSB) [9, 36]; hereafter, SB refers to GSB."` | 极易引起指代歧义。**规则**：一词一义全局锁死；若需区分新旧结构，自始至终写作 `GSB`。 |
| **4. 本论文系统名自身大小写/连字符分裂** | `QPlacer` (`conf__isca__Zhang0D0AO0B0025`, ISCA'25, p. 1–2, `EX-46`)：标题写 `QPlacer`，摘要与正文通篇写 `Qplacer`；`M-ANT` (`conf__hpca__HuZ00GH00GL25`, HPCA'25, p. 1, `EX-39`)：标题写 `M-ANT (... Numerical Type)`，摘要写 `MANT (... numeric type)`；`ChoPIM` (`conf__isca__ChoKLE20`, ISCA'20, p. 4, `EX-35`)：节标题 `CHOPIM` vs 正文 `Chopim` | 暴露低级校对失守。**规则**：在 LaTeX 导言区定义 `\newcommand{\sysname}{Pond}`，全文所有系统名必须通过宏调用，实现 100% 拼写锁定。 |

---

## 3. LaTeX 微排版与机械规范（LaTeX Micro-Typography & Mechanical Conventions）

### 3.1 交叉引用规范：四大顶会 × 三大年代实证矩阵

对 `macro_pool` 全部 152 篇论文（约 158 万词）及 `deep_read` 48 篇进行全量正则扫描与人工抽检，揭示出极鲜明的**会议传统差异**与**时代演化趋势**：

#### 表 3-1：交叉引用与 `e.g.,`/`i.e.,` 按四大顶会分布（152 篇 `macro_pool`，各 38 篇）

| 顶会 (n=38) | `Figure` 全拼（篇数） | `Fig.` 缩写（篇数） | `Figure` 占比 | `Section` 全拼（篇数） | `Sec.` 缩写（篇数） | `§` 符号（篇数） | `Table` vs `Tab.` | `e.g.,` 加逗号比例 | `i.e.,` 加逗号比例 |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| **ISCA** | 1,101 (35) | 305 (15) | 78.3% | 463 (37) | 3 (1) | 46 (3) | 351 vs **0** | 83.4% (246/295) | 87.8% (202/230) |
| **MICRO** | 1,165 (35) | 401 (16) | 74.4% | 466 (31) | 35 (3) | 43 (3) | 288 vs **0** | 87.6% (318/363) | 90.7% (332/366) |
| **HPCA** | 1,167 (34) | **441 (21)** | 72.6% | 409 (34) | **101 (4)** | **0 (0)** | 266 vs **5** | 85.7% (270/315) | 92.1% (246/267) |
| **ASPLOS** | **1,395 (38)** | 62 (4) | **95.7%** | 337 (30) | 18 (2) | **298 (11)** | 311 vs **0** | **91.8%** (281/306) | 87.7% (157/179) |
| **全池合计** | **4,828** | **1,209** | **80.0%** | **1,675** | **157** | **387** | **1,216 vs 5** | **87.2%** | **89.9%** |

#### 表 3-2：交叉引用与 `e.g.,`/`i.e.,` 按三大年代演变（152 篇 `macro_pool`）

| 年代 (篇数) | 使用 `Fig.` 篇数占比 | 使用 `§` 篇数占比 | `e.g.,` 加逗号占比 | `i.e.,` 加逗号占比 |
| :--- | :---: | :---: | :---: | :---: |
| `2011-2015` (47) | 4/47 (**8.5%**) | 2/47 (**4.3%**) | 80.6% (299/371) | 82.3% (288/350) |
| `2016-2022` (65) | 27/65 (**41.5%**) | 8/65 (**12.3%**) | 86.0% (499/580) | 90.7% (398/439) |
| `2023-2026` (40) | 25/40 (**62.5%**) | 7/40 (**17.5%**) | **96.6%** (317/328) | **99.3%** (251/253) |

**四条直接指导 LaTeX 排版的硬规律**：
1. **ASPLOS 与 HPCA 风格泾渭分明**：投 **ASPLOS** 首选全拼 `Figure 1`（95.7%）与 `Section 3` 或 `§3`（29% 论文用 `§`，如 `Pond`, `HFI`, `Autonomous NIC Offloads`）；投 **HPCA**（纯 IEEE 模板）**绝对不要用 `§`**（0/38 篇！），统一用 `Section` 或 `Sec.`，图引用可选 `Figure` 或 `Fig.`；投 **ISCA / MICRO** 最稳妥通用解为全拼 `Figure 1` + `Section 3`。
2. **“IEEE 句首 `Figure` / 句中 `Fig.` 分裂规则”在实战中为 0 遵守**：我们对 48 篇 `deep_read` 逐句切分句首与句中位置后发现，严格遵守该分裂规则的论文为 **0 / 48 篇**！实际做法是 **43 / 48 篇（89.6%）在正文里自始至终只用同一种形式**（全用 `Figure` 或全用 `Fig.`），仅 5 篇失范混用（如 `SIGMA` HPCA'20、`AVA` HPCA'22、`PICACHU` ASPLOS'25、`Graphicionado` MICRO'16、`Neu10` MICRO'24）。因此，Phase 2 规则应要求**全篇正文 100% 锁死单一形式**（推荐 `Figure` + `Section` 或 ASPLOS 专用 `Figure` + `§`），用 LaTeX 宏 `\figref{}` / `\secref{}` 强制统一。
3. **永远不要缩写 `Table`**：全池 152 篇出现 1,216 次 `Table` 仅 5 次 `Tab.`（集中于单篇），更不可生造 `Tbl. III`（如 `M-ANT`, HPCA'25）。
4. **`e.g.,` 与 `i.e.,` 必须带美式逗号**：到 2023–2026 年，带逗号比例已达 **96.6% (`e.g.,`)** 与 **99.3% (`i.e.,`)**；且严禁误写为 `"For e.g.,"`（`SIGMA`, HPCA'20, `conf__hpca__QinSKNS0KK20`, p. 11，语义重复）。

### 3.2 引文语法整合（Citation Integration）

在修正了 `Author et al. [9] proposed` 误匹配后，我们对 48 篇 `deep_read` 进行了精确引文语法审计：

| 引文句法模式 | `exemplar_pre2023` | `exemplar_2023plus` | `contrast_ordinary` | `contrast_post2023` | 规范判定 |
| :--- | :---: | :---: | :---: | :---: | :--- |
| 句首 `In [X], ...`（引文作介词宾语） | 0.04 (仅 1 处：`Eyeriss` p. 5) | **0.00 (0)** | 0.10 (1 处：`Alvarez` p. 11) | 0.00 (0) | **禁止**（`EX-40`） |
| 裸 `[X] Verb`（引文编号直接当主语） | 0.13 (3 处全在 `SolarCore` p. 11–12) | 0.08 (1 处偶发：`Constable` p. 9) | 0.00 (0) | 0.00 (0) | **禁止**（`EX-43`） |
| 弱被动 `described/reported in [X]` | 0.73 (17 处) | 0.34 (4 处) | **1.96 (20 处，2.7×)** | 0.31 (2 处) | **压制**（人类差文典型弱句法） |
| 地道标杆：`Author et al. [X]` / `Prior work [X]` / 句尾附注 `[X]` | 主导范式（`Author et al.` 2.28 / `prior work` 0.82） | 主导范式（`prior work` 1.10） | 混杂 | 主导范式 | **推荐** |

**引文检验的“遮挡测试（Cover-Up Test）”**：用手盖住正文中的 `[12]`，如果句子立刻语法残缺（如 `In [22], special registers...` → `In , special registers...`；`[34] investigated...` → `investigated...`），则引文整合不合格！必须改写为 `Prior work [22] implements...`、`Smith et al. [34] investigate...` 或作为整句末尾的括号附注 `... [22].`。同时，在 LaTeX 中务必加载 `\usepackage{cite}` 或 `natbib` 的 `sort&compress` 选项，彻底杜绝 `TimeCache`（ISCA'21, p. 1–2, `EX-38`）中未排序的 `[47] [11] [22] [44] [9] [6] [17]`、同段混用 `[16, 38]` 与 `[21] [42]`，以及 `PVCoherence`（HPCA'14）中未合并的 `[31][4][30]`。

### 3.3 破折号迷思证伪与常见微排版要素

| 微排版要素 | 48 篇实证数据（`pre23` / `23+` / `ord` / `post23AI`） | 正面标杆范式与负面踩坑案例 |
| :--- | :--- | :--- |
| **正文长破折号（Unicode `—`）** | **8.66** / **8.21** / 6.09 / **2.19**（每万词，已剔除 `Abstract—`） | **证伪“破折号=AI”**：顶尖母语作者高频善用长破折号做插入定义与机制解释（`Clearing the Clouds` `EX-08`、`Swarm` `EX-19`、`Amdahl's Law Market` `EX-36`、`RowHammer` `EX-03`）。**反面踩坑**：① `SIGMA` (p. 2, `EX-10`) 与 `Constable` (p. 6, `EX-22`) 用短连字符 `-` 冒充破折号（LaTeX 应写 `---`）；② `FastTTS` (ASPLOS'26) 把长破折号误用于行号范围 `(lines 18—19)`（数值范围必须用短破折号 en-dash `--` 即 `18–19`！）。 |
| **粗体段首引导词（`\paragraph{...}`）** | **40.8** / **44.4** / 32.7 / 38.3（处/篇） | 体系结构论文扫读性利器，用于设计子部件、实验维度和相关工作分组（标杆显著高于人类差文）。须全篇统一末尾是否带句号（推荐 `\paragraph{Foo.}`）。 |
| **项目符号与行内枚举** | bullets: 5.0 / 9.2 / 8.6 / 8.0；`(1)(2)`: 2.3 / 4.0 / 1.8 / 0.7；`(i)(ii)`: 1.3 / 0.1 / 0.1 / 0.3 | 2023+ 标杆明显偏好数字行内枚举 `(1) ... (2) ...`（4.0 次/篇）而非罗马小写 `(i)(ii)`（仅 0.1 次/篇），而 AI 组常用对称三联 `i)... ii)... iii)...`（`FastTTS` p. 1）。 |
| **脚注（Footnotes）** | **1.0** / **2.0** / 0.6 / 0.2（处/篇） | 标杆平均仅 1–2 个，用于**不打断主叙事的精确工程注记或术语澄清**（如 `SALP` ISCA'12 p. 1 注脚 `Intel Sandy Bridge dedicates 264 pins for two channels [14]`、p. 4 澄清 `subarray` 与 `row of tiles` 对应关系）。切忌在脚注里藏核心设计逻辑或长篇辩解。 |
| **等宽字体 `\texttt{}` 与斜体 `\emph{}`** | 精读核验 | `\texttt{}` 严格用于指令名、函数/API、寄存器名、负载名（如 `enqueue_task`, `dequeue_task` in `Swarm` `EX-19`; `hfi_set_metadata` in `HFI` `EX-27`）；`\emph{}` 仅用于**首次引入核心定义词**或极克制的对比强调，禁止全段大面积斜体或滥用引号作“伪强调”（scare quotes，如 `AVA` HPCA'22 误用两个右引号 `”compatible”`）。 |
| **行内数学与单位间距** | 精读核验 | 变量符号须用数学模式 `$N$`, `$t_{RP}$`，乘号用 `$\times$`（`5.7×`, `1.86×`）而非字母 `x`；数字与单位之间用不换行空格 `~`（`16~GB`, `3.2~GHz`）；标点后绝不漏空格（反例：`QPlacer` `Fig.1`、`Turnpike` `ainment,Turnstile`）。 |

### 3.4 终稿机械卫生失败清单（真实已发表顶会论文事故汇编）

即便通过同行评审发表，多篇顶会论文（含 2021–2026 Top Picks / Best Paper）仍留有令人震惊的机械校对事故，这些全部应直接转化为 Phase 2 的自动化发稿前扫描规则：

- **未编译引文占位符**：`PF-LLM`（ASPLOS'26 Best Paper, `conf__asplos__XuSLBWLX026`, p. 2）：`[2, 18, 21, 35? ]`
- **残留外部工具 XML 标签**：`LLM.265`（MICRO'25 Best Paper, `conf__micro__XuW0CLZW25`, p. 10）正文中遗留 `<latexit>` 标签，且含 `Comparision` / `uncomprssed` 拼写错
- **改稿残片 + 拼写错 + 漏闭括号三连击**：`Chasing Carbon`（HPCA'21 Top Picks, `conf__hpca__GuptaKLTLW0W21`, p. 2, `EX-42`）：`"highglights the need for computer systems to directly minimize directly optimize ... (e.g., raw-material procurement, fabrication, packaging, and assembly."`
- **数量声明与实际枚举不符**：`PF-LLM`（ASPLOS'26 Best Paper, p. 10）：`"three of the mostly widely-used"` 紧接着列了 4 个模型（且 `mostly widely-used` 语法错误）
- **重复词与残缺介词链**：`Correction Prediction`（HPCA'15, `conf__hpca__DuweJ015`, p. 7）：`"Depending on the the desired level"`；`QPlacer`（ISCA'25, `conf__isca__Zhang0D0AO0B0025`, p. 2）：`"Fig.1 illustrates a comparison of with"`；`DynamoLLM`（HPCA'25 Best Paper, `conf__hpca__StojkovicZGTC25`, p. 1/10）：`"education [5] and other."` / `"an 40% error"`；`PREMA`（HPCA'20, `conf__hpca__ChoiR20`）：`schdeuler`, `grammer`, `chracterization`

---

## 4. 三桶批判性反例法医学目录（Forensic Anti-Pattern Catalog）

### 4.1 Class B 反例库：后 2023 AI 污染 / LLM-ese 全景解剖

#### 4.1.1 15 年宏观断崖跃迁实证（152 篇 `macro_pool`）

把时间轴拉长到 2011–2026 全部 152 篇宏观语料，大量词汇呈现典型的**“2011–2022 近似为零 → 2023–2026 断崖垂直起飞”**的阶跃函数（Step Function），这在统计学上排除了自然语言渐进演化的可能，直接指向大语言模型写作辅助的全面渗透：

| AI 指纹词（词根） | `2011-2015` (n=47) | `2016-2022` (n=65) | `2023-2026` (n=40) | 2023–2026 相对前代跃升 |
| :--- | :---: | :---: | :---: | :--- |
| `pivotal` | 0.00 (0/47) | 0.00 (0/65) | **0.16 (5/40)** | **0 → 12.5% 论文**（纯后 2023 产物） |
| `meticulous*` | 0.00 (0/47) | 0.00 (0/65) | **0.18 (4/40)** | **0 → 10.0% 论文**（纯后 2023 产物） |
| `democratiz*` | 0.00 (0/47) | 0.00 (0/65) | **0.11 (2/40)** | **0 → 5.0% 论文**（纯后 2023 产物） |
| `intricate` | 0.00 (0/47) | 0.03 (2/65) | **0.49 (7/40)** | **16.3×**（篇数比例 3.1% → 17.5%） |
| `underscore` | 0.00 (0/47) | 0.03 (2/65) | **0.38 (13/40)** | **12.7×**（篇数比例 3.1% → **32.5%**！） |
| `seamless*` | 0.07 (3/47) | 0.14 (6/65) | **0.67 (16/40)** | **4.8×**（篇数比例 **40.0%**！） |
| `unveil` | 0.00 (0/47) | 0.01 (1/65) | **0.16 (3/40)** | **16.0×** |
| `foster` | 0.00 (0/47) | 0.01 (1/65) | **0.11 (4/40)** | **11.0×** |
| `delve` | 0.04 (2/47)* | 0.00 (0/65) | **0.18 (5/40)** | 2016–2022 为 0 → 2023–2026 **12.5%** |
| `landscape` | 0.00 (0/47) | 0.06 (4/65) | **0.22 (6/40)** | **3.7×**（篇数比例 15.0%） |
| `orchestrate` | 0.02 (1/47) | 0.10 (6/65) | **0.29 (9/40)** | **2.9×**（篇数比例 22.5%） |
| `holistic` | 0.11 (4/47) | 0.09 (4/65) | **0.25 (9/40)** | **2.8×**（篇数比例 22.5%） |
| `paradigm` | 0.36 (7/47) | 0.45 (15/65) | **1.17 (11/40)** | **2.6×**（且在污染文中单篇高频复读如 `M-ANT` 11 次） |
| `synerg*` | 0.07 (2/47) | 0.13 (5/65) | **0.31 (8/40)** | **2.4×**（篇数比例 20.0%） |
| `crucial` / `comprehensive` / `notably` | 0.22 / 0.27 / 0.13 | 0.38 / 0.17 / 0.29 | **1.35 / 1.17 / 0.74** | 分别跃升 **3.6× / 6.9× / 2.6×**（`crucial` 达 67.5% 论文） |

#### 4.1.2 `post2023_ai_marker_hits.json`（152 篇）扫描规律与“防误杀”法医学铁律

`post2023_ai_marker_hits.json` 覆盖 2024–2026 四大顶会中命中 10 个标志词（`delve, pivotal, holistic, intricate, underscores, seamlessly, fosters, multifaceted, realm, paramount`）的 **152 篇不重复论文**（ASPLOS 60 篇、HPCA 33 篇、ISCA 30 篇、MICRO 29 篇；命中 3 词者 3 篇、2 词者 14 篇、1 词者 135 篇）。对片段的逐条法医学复核证明：**单字扫描绝对不能直接定罪**，必须识别合法假阳性：
- **硬件/系统专有名词假阳性**：ARM CCA 架构官方硬件隔离态 `Realm Management Extension (RME)` 与 `the Realm`（如 `conf__asplos__ChoiCJK26`、`conf__asplos__YangQRLYNG26`），以及检索增强语言模型 `Google’s REALM [22]`（`conf__isca__JiangSGAYD25`）。
- **否定式克制声明假阳性**：`PVCoherence`（HPCA'14, `conf__hpca__ZhangBES14`, p. 2, `EX-16`）的 `"we intentionally do not delve deeply into the theoretical foundations"`。
- **局部孤立技术定语假阳性**：`Autonomous NIC Offloads`（ASPLOS'21, `conf__asplos__PismennyEYL0T21`, p. 5, `EX-21`）中孤立出现的 `"size-preserving for seamless interoperation with software TCP/IP"`，全文无任何其他 AI 指纹。

**结论**：只有当**同一段落或相邻两页出现 ≥ 2 类独立 AI 信号**（紫文词 + 宏大容器句式 + 分词拖尾 + 机械模板），或命中高特异性短语搭配（如 `in the (ever-evolving|intricate) realm of`、`we delve into the (rationale|inner workings)`、`harmonizing the delicate balance`、`marks a pivotal advancement`）时，才判定为 Class B AI 污染。

#### 4.1.3 Class B 七大结构性病灶（均附逐字核验证据）

1. **病灶 B1：紫文词法通胀（Lexical Inflation）**——用高亢华丽却零技术增量的动词/形容词包裹平凡事实。典型：`Hestia`（MICRO'24, `conf__micro__XuLZLW0024`, 全文 59 次/19 类 AI 词；p. 5 `EX-24`：`"transcends conventional debugging methods ... scrutinize ... sheds light on the intricate details"`）；`QPlacer`（ISCA'25, `conf__isca__Zhang0D0AO0B0025`, p. 2 `EX-46`：`"meticulously designed ... multifaceted interactions ... pivotal advancement ... harmonizing the delicate balance"`）。
2. **病灶 B2：宏大空洞开场与抽象容器词（Grandiose Macro Openers & Wrapper Nouns）**——引言不从体系结构瓶颈起笔，而是从“过去十年人工智能深刻重塑了人类社会”起笔，并堆砌 `realm / landscape / paradigm / pillar / horizon`。典型：`PICACHU`（ASPLOS'25, `conf__asplos__QinXT0Z25`, p. 1：`"In the past decade, the landscape of artificial intelligence (AI) has undergone a profound transformation, with Transformer-based Large Language Models (LLMs) redefining the capabilities of AI ... reshaping both industry and human life."`）；`QPlacer`（ISCA'25, p. 1 `EX-13`：`"In the ever-evolving realm of quantum computing ... have captivated people’s attention, offering immense potential of computation to unravel intricate problems"`）；`M-ANT`（HPCA'25, `conf__hpca__HuZ00GH00GL25`, 全文 `paradigm` 高达 11 次，p. 1 `EX-39` `"killer computer applications"`）。
3. **病灶 B3：机械 `Not only X, but also Y` 与对称“三联排比”（Symmetrical Rule-of-Three）**——用假装工整的三段式包装掩盖机制深度。典型：`FastTTS`（ASPLOS'26, `conf__asplos__ChenML0MLF26`, p. 1–2 `EX-30`：`"three novel techniques: i) ... ii) ... iii) ..."` + `"healthcare, autonomous driving, and defense"` + `"privacy, energy efficiency, or responsiveness"`）；`QPlacer` p. 2 & `Hestia` p. 5 频繁使用 `"not only ... but also ..."` 吹捧自家设计。
4. **病灶 B4：模板化 `Challenge I / II / III` 与 `Takeaway / Key Insight` 克隆**——无论问题是否自然呈现三层结构，一律硬拆成三个对称 `Challenge-1/2/3` 对应三个 `Solution-1/2/3`。典型：`ρHammer`（MICRO'25, `conf__micro__ChenTTLZQ25`, p. 2 `EX-18` 的 `Challenge I / II / III` 且在两页内把 `"novel prefetch-based hammering paradigm"` 复读 4 次）；`FastTTS`（ASPLOS'26 的 `Challenge-1/2/3`）。
5. **病灶 B5：悬垂分词拖尾空洞总结（Participle-Tail Bloat）**——每句话末尾机械粘一条 `, thereby ...ing` / `, enabling ...` / `, ensuring ...` / `, paving the way for ...`（实证频次比纯人工标杆高 **2.4×–15.7×**），把因果关系揉成一团模糊的善后口号。典型：`LLM.265`（MICRO'25, p. 1 `EX-04`：`"thereby alleviating memory requirements ... making it a highly effective solution"`）；`QPlacer`（p. 2 `EX-46`：`"ensuring frequency domain isolation"`）；`ρHammer`（p. 1：`"thereby effectively preventing early Rowhammer strategies"`）。
6. **病灶 B6：口号化愿景与商业公关语域（Sloganized Hype）**——典型：`FastTTS`（ASPLOS'26, p. 2 `EX-30`：`"essential for realizing democratized agentic AI"`）；`DynamoLLM`（HPCA'25, p. 1：`"To pave the way towards energy-efficient and sustainable LLM inference clusters"`）；`ρHammer`（MICRO'25, p. 1/9：`"valiant efforts"`, `"strikes the perfect of such a balance"`）。
7. **病灶 B7：缝合断层（The Frankenstein Seam）**——后 2023 顶会最具诊断价值的独有现象！作者仅把摘要、引言首段或章节导语丢给 LLM 润色，自己则手写其余技术细节且未通读，导致**满级 GPT 紫文与破碎非母语语法在同一页甚至相邻两句间零距离撞车**：
   - `QPlacer`（ISCA'25, p. 1 `EX-13` & p. 2 `EX-46`）：`"In the ever-evolving realm ... unravel intricate problems"` 下一句立刻变成 `"particularly the utilizing fixed-frequency transmon qubits ... stands out"`；p. 2 `"harmonizing the delicate balance"` 下一句立刻跌成 `"To achieve these"`, `"to setup minimum spacing, and partitioning resonators space"`, `"Fig.1 illustrates a comparison of with"`。
   - `Hestia`（MICRO'24, p. 5 `EX-24`）：`"In the intricate realm of HLS ... we delve into the inner workings of this innovative interpreter."` 下一行进入 `A. Software Simulation` 立刻跌成 `"We implement an interpreter for SCF dialect ... The software level doesn’t contain any hardware information like timing and resource."`。
   - `PF-LLM`（ASPLOS'26 Best Paper, p. 12 `EX-33`）：一整段 131 词的 GPT Section 7 总导语直接被误贴进 `7.1 Assembly Code vs. Source Code as Input:` 开头，随后突兀切回 `"Our PF-LLM takes input from the assembly code directly stripped from the binary..."`。

#### 4.1.4 2025–2026 获奖论文 AI 漂移警示表（Award-Paper AI-Drift Audit）

| 获奖论文 | 荣誉与出处 | AI 漂移与校对硬伤铁证 | 给 Phase 2 的核心教训 |
| :--- | :--- | :--- | :--- |
| **PF-LLM** | ASPLOS 2026 Best Paper (`conf__asplos__XuSLBWLX026`) | 12 处/9 类 AI 词；p. 12 误贴 131 词纯 GPT 章节导语进 `7.1`（`EX-33`）；p. 2 留未解析引文 `[2, 18, 21, 35? ]`；p. 10 `"three of the mostly widely-used"` 列 4 项 | **绝不能把 2025–2026 Best Paper 的过渡段/讨论段当作正面范本** |
| **DynamoLLM** | HPCA 2025 Best Paper (`conf__hpca__StojkovicZGTC25`) | 10 处/7 类 AI 词集中轰炸 p. 1（`pivotal`, `paramount`, `underscores`, `To pave the way`, `seamlessly`, `holistic`）；同页漏复数 `"and other."`、p. 10 `"an 40% error"`（`EX-11`） | 论文获奖源于扎实系统工作而非首页 LLM 润色；相反，首页紫文拉低了专业质感 |
| **LLM.265** | MICRO 2025 Best Paper (`conf__micro__XuW0CLZW25`) | 全篇摘要 183 词 **0 个量化数字**（`EX-04`）；正文出现 `delve deeper`, `underscoring`, `seamlessly`；p. 10 漏 `<latexit>` XML 标签与 `Comparision`/`uncomprssed` | 创意极佳（视频编解码器复用为张量编解码器）但写作/校对仓促，不可照抄摘要体例 |

---

### 4.2 Class A 反例库：人类差文（`contrast_ordinary`）与预 2023 标杆瑕疵

与后 2023 AI 污染截然不同，Class A 人类差文（2015–2022 `contrast_ordinary` 全 10 篇均有显著样本）的问题不是“过度光滑浮夸”，而是**“晦涩、僵硬、失控、疏于读者共情”**：

1. **病灶 A1：被动语态说明书墙（Passive Datasheet Walls）**——`contrast_ordinary` 被动语态高达 **123.95 / 万词**。典型如 `Correction Prediction`（HPCA'15, `conf__hpca__DuweJ015`, p. 9 `EX-29`）评估方法段**连续 7 句全部被动语态**（`was chosen ... were run ... was determined ... were determined ... was scaled ... was scaled ... are not scaled`）；`TimeCache`（ISCA'21, `conf__isca__OjhaD21`, p. 1）冗长弱被动 `"Partitioning has been seen to be associated with higher overheads"`。
2. **病灶 A2：非母语直译与语法碎裂（Non-Native Calques & Broken Syntax）**——`Alvarez SPM`（ISCA'15, `conf__isca__AlvarezVMCGMNAV15`, p. 1 `EX-17`）西语直译 `"being the primary concerns the power consumption originated in..."`, `"responsible of"`, `"big importance"`, `"allow to map"`；`AVA`（HPCA'22, `conf__hpca__LazoRMBVSCUC22`, p. 5 `EX-23`）`"will not be longer used"`、`"larger MVL configurations holds"`；`Turnpike`（MICRO'21, `conf__micro__ZengKLJ21`, p. 5 `EX-44`）东亚直译 `"a checkpoint cannot but be placed"`, `"In the input-saving point of view alone"`, `"a store instructions"`；`PREMA`（HPCA'20, `conf__hpca__ChoiR20`, p. 5 `EX-45`）双重情态 `"need not have to distinguish"`。
3. **病灶 A3：零数字摘要与摘要复读机（Zero-Number Abstracts & Copy-Paste Intro）**——`iThreads`（ASPLOS'15, `conf__asplos__Bhatotia0ABR15`, p. 1 `EX-05`）摘要以 `"shows significant performance gains"` 糊弄；`ChoPIM`（ISCA'20, `conf__isca__ChoKLE20`, p. 1）摘要 77 词/62 词马拉松长句且 0 数字；`Authenticache`（MICRO'15, `conf__micro__BachaT15`, p. 1–2 `EX-12`）与 `TimeCache`（ISCA'21, p. 1–2 `EX-38`）把摘要整段直接复制粘贴进引言。
4. **病灶 A4：臃肿名词化与嵌套 `of` 链（Nominalization Bloat）**——`AVA`（p. 5 `EX-23`）`"The freeing up of a physical register occurs in two distinct cases."`；`TimeCache`（p. 2 `EX-38`）连套三个 `of`：`"retain the benefits of a shared cache of allowing each process access to the entire cache and of cache occupancy by a single copy..."`。
5. **病灶 A5：防御性审稿补丁（Defensive Reviewer Patches）**——`ChoPIM`（ISCA'20, p. 4 `EX-35`）生硬负气声明 `"We do not consider graph processing in this paper because we do not innovate in this context."`。
6. **病灶 A6：流水账 Related Work 与缩写字母汤**——`StreamBox-HBM`（ASPLOS'19, `conf__asplos__MiaoJPML19`, p. 13 `EX-34`）点名册写法 + `"No prior work, however..."`；`AVA`（HPCA'22）7 个视觉撞车缩写。

#### 预 2023 顶级标杆论文祛魅审计表（`[EXEMPLAR-FLAW]` — 学什么 vs 绝不学什么）

| 经典标杆论文 | 值得学习的闪光点 | **绝对不可模仿的局部瑕疵（精确出处）** |
| :--- | :--- | :--- |
| **SIGMA** (HPCA'20 Best Paper, `conf__hpca__QinSKNS0KK20`) | 微架构设计图清晰、矩阵稀疏性拆解直白 | p. 1 宏大开场 + 病句 `"Within SIGMA includes..."`；p. 1–2 多处主谓一致错（`"GEMMs comprises"`, `"compute requirements ... has grown"`, `"recent research focus"`）；p. 2 `; and therefore is` + `-` 代破折号；p. 5 同页混用 `Sec. IV`/`Section IV`；p. 11 `"For e.g.,"`（`EX-10`） |
| **Eyeriss** (ISCA'16 Top Picks, `conf__isca__ChenES16`) | Row Stationary 数据流分类体系极清晰、能耗分解严谨 | p. 5 句首引文作介词宾语 `"In [22], special registers..."`（`EX-40`）；p. 9 中途临时改名 `"SOC-MOP, MOC-MOP and MOC-SOP ... are renamed as OSA, OSB and OSC"` |
| **Whisper** (MICRO'22 Best Paper, `conf__micro__KhanUNSLJK22`) | 生产数据中心分支画像扎实 | p. 1–2 密集自夸 `novel` 4 次；全语料最高 58 处三词以上修饰链；超长术语名与行末漏连字符（`EX-41`） |
| **Chasing Carbon** (HPCA'21 Top Picks, `conf__hpca__GuptaKLTLW0W21`) | 开创碳足迹实证框架、Takeaway 提炼有力 | p. 2 终稿失校三连击 `"highglights ... to directly minimize directly optimize ... (e.g., ..., and assembly."`（`EX-42`） |
| **PVCoherence** (HPCA'14 Best Paper, `conf__hpca__ZhangBES14`) | 极其出色的范围界定与认识论克制（`EX-16`） | 摘要缺少具体验证加速/状态空间缩减量化数字；引文未合并 `[31][4][30]` |
| **SolarCore** (HPCA'11, `conf__hpca__LiZCL11`) | 跨域问题定义清晰 | p. 11–12 三处裸引文编号直接作主语 `"[34] investigated ... [36] proposed ..."`（`EX-43`） |

### 4.3 Class A vs Class B 双轴鉴别诊断矩阵

| 诊断维度 | 纯人工标杆 (`[GOLD-HUMAN]`) | Class A 人类差文 (`[BAD-HUMAN]`) | Class B AI 污染 (`[AI-TAINTED]`) |
| :--- | :--- | :--- | :--- |
| **被动语态密度** | 适中（**72–89 / 万词**） | **极高（124 / 万词）** | **异常偏低（62 / 万词）** |
| **表面语法流畅度** | 高且有节奏变化 | 低（母语直译、单复数/介词错） | 局部极高，但常伴**缝合断层** |
| **动词信息密度** | 极高（`stall/squash/track/bypass/incur`） | 中偏低（名词化埋没动词） | **极低**（`enhance/facilitate/empower/ensure`） |
| **因果组织方式** | `because/since/instead/hence` + 词汇链 | 零散长句 + 弱被动 | `, enabling / , ensuring / , thereby` + `Additionally,` |
| **长破折号使用** | 高频精准（**8.2–8.7 / 万词**） | 中等（6.1 / 万词） | **极低（2.2 / 万词）** |
| **冒号与模板密度** | 自然适中（82 / 万词） | 自然适中（83 / 万词） | **飙升（128 / 万词，`Challenge I/II/III`）** |
| **量化态度** | 报均值+区间+代价+假设边界 | 常漏数字或干瘪报数 | 报峰值+口号吹嘘（`Comprehensive`, `breakthrough`） |

---

## 5. 真实语料 Bad → Good 改写示范与 Phase 2 可执行规则集

### 5.1 六组基于真实语料的 Bad → Good 精改示范

#### 示范 1：Class B AI 宏大紫文开场 + 缝合断层 → 纯人工机制直入（原出处：`QPlacer`, ISCA'25, `conf__isca__Zhang0D0AO0B0025`, p. 1, `EX-13`）
- **Bad（原文）**：
  > In the ever-evolving realm of quantum computing, quantum computers (QCs) in Noisy Intermediate-Scale Quantum Computing (NISQ) [71] have captivated people’s attention, offering immense potential of computation to unravel intricate problems in chemistry [16], [45], biology [49], algorithms [32], [82], and machine learning [12], [91]. Superconducting QCs [4], [47], particularly the utilizing fixed-frequency transmon qubits anchored by Josephson junctions (JJs), stands out as a leading option for scalable quantum computing.
- **Good（精改）**：
  > Superconducting quantum computers built from fixed-frequency transmon qubits [4], [47] now exceed 1,000 physical qubits [41], driven by fast gate speeds [6], [7], [27] and error rates approaching fault-tolerance thresholds [80]. However, scaling physical layout to thousands of qubits exposes severe inter-qubit and resonator crosstalk that degrades gate fidelity.
- **改写心法**：整段砍掉 `"In the ever-evolving realm ... captivated people's attention ... unravel intricate problems"` 科普废话；修复 `the utilizing` 与 `stands out` 主谓一致错误；第 1 句落到真实物理硬件规模（`1,000 physical qubits`），第 2 句立刻亮出物理瓶颈（`crosstalk degrades gate fidelity`）。

#### 示范 2：Class B AI 空洞章节导语 + 缝合跌落 → 直接切入设计实质（原出处：`Hestia`, MICRO'24, `conf__micro__XuLZLW0024`, p. 5, `EX-24`）
- **Bad（原文）**：
  > In the intricate realm of HLS, where high-level descriptions evolve into complex hardware designs through a sequence of transformation passes, the need for a comprehensive debugging mechanism is paramount. The multi-level interpreter in Hestia transcends conventional debugging methods by offering the capability to simulate and scrutinize HLS designs at various levels of abstraction. The interpreter not only simplifies the debugging process but also sheds light on the intricate details of hardware synthesis. In the following paragraphs, we delve into the inner workings of this innovative interpreter. A. Software Simulation: We implement an interpreter for SCF dialect to inspect the internal state of execution. The software level doesn’t contain any hardware information like timing and resource.
- **Good（精改）**：
  > Hestia executes an HLS design across multiple MLIR abstraction levels so developers can isolate bugs introduced by specific lowering passes.
  > **A. Software Simulation.** At the highest level, Hestia interprets the SCF dialect to inspect program state before hardware lowering, without modeling cycle timing or hardware resources.
- **改写心法**：把 80 词零信息量的紫文导入段压缩为 1 句 21 词的机制总纲；修复漏定冠词（`the SCF dialect`）、消除学术禁用缩写 `doesn't` 与单复数错（`hardware resources`）。

#### 示范 3：Class B 模板化 `Challenge` + 抽象空转 → 精准机制瓶颈陈述（原出处：`ρHammer`, MICRO'25, `conf__micro__ChenTTLZQ25`, p. 2, `EX-18`）
- **Bad（原文）**：
  > Challenge I: Complex DRAM Address Mappings. A critical prerequisite for launching effective Rowhammer attacks is the ability to reverse-engineer the correct DRAM address mapping of the target system in order to precisely locate the victim rows. ... To overcome these limitations, we present a new layout-agnostic reverse-engineering methodology that leverages selective pairwise measurements and structured deduction to accurately and generically recover mappings...
- **Good（精改）**：
  > **DRAM Address Mapping.** Launching RowHammer requires knowing which physical addresses map to adjacent rows in the same bank. Prior reverse-engineering heuristics [30, 56, 65, 68] fail on Alder Lake and Raptor Lake processors because DDR5 adds bank groups and wider XOR bank-indexing functions [24, 31]. We recover the bank and row functions without prior layout assumptions by measuring row-buffer conflict latencies across selected address pairs and solving the resulting linear constraints.
- **改写心法**：去掉 `Challenge I:` 模具和 `A critical prerequisite` 空话；用 `because` 直接点明硬件变更原因；把空洞的 `structured deduction to accurately and generically recover` 替换为可感知的真实算法动作（`measuring row-buffer conflict latencies ... and solving linear constraints`）。

#### 示范 4：Class A 连续七句被动语态墙 → 主动清晰评估方法段（原出处：`Correction Prediction`, HPCA'15, `conf__hpca__DuweJ015`, p. 9, `EX-29`）
- **Bad（原文）**：
  > An aggressive branch predictor was chosen to not unduly penalize Deep Pipe. Performance simulations were run using Gem5 [5], fast forwarding for 1 billion instructions and executing for 1 billion instructions. Frequency for a given voltage was determined by the linear scaling in [2]. Nominal dynamic and static power overheads were determined using the simulation results and McPAT [19]. Low supply voltage dynamic power was scaled quadratically with respect to voltage [32]. Low supply voltage static power was scaled cubically with respect to voltage [32].
- **Good（精改）**：
  > We model an aggressive branch predictor so branch mispredictions do not unduly penalize Deep Pipe. Using gem5 [5], we fast-forward each benchmark for 1 billion instructions and simulate the next 1 billion instructions. We derive operating frequency at each voltage via linear scaling [2], compute nominal dynamic and static power with McPAT [19], and scale low-voltage dynamic and static power quadratically and cubically with supply voltage [32], respectively.
- **改写心法**：将 6 个死气沉沉的被动单句重构为 3 个以 `We` 为主语的紧凑主动句，动词精准落在 `model / fast-forward / simulate / derive / compute / scale`，词数精简 22%，可读性翻倍。

#### 示范 5：Class A 非母语直译 + 臃肿名词化 → 干净直接架构因果句（原出处：`Alvarez SPM`, ISCA'15, p. 1 `EX-17` & `AVA`, HPCA'22, p. 5 `EX-23`）
- **Bad（原文）**：
  > Unfortunately, the cost of performing these actions becomes an obstacle to scaling up the number of cores, being the primary concerns the power consumption originated in the caches and the increasing amount of coherence traffic in the Network on-Chip (NoC). ... However, SPMs suffer from poor programmability as the software is responsible of explicitly transferring data... / The freeing up of a physical register occurs in two distinct cases. ... claim and free a physical register that will not be longer used.
- **Good（精改）**：
  > Unfortunately, hardware coherence limits core scaling because cache lookups consume substantial power and coherence messages congest the NoC. ... However, SPMs complicate programming because software must explicitly transfer data and keep copies coherent. / AVA frees a physical register in two cases. ... reclaim a physical register once it is no longer live.
- **改写心法**：消灭西语独立分词 `being the primary concerns`、误用介词 `responsible of`、语序错 `will not be longer used` 与冗余名词化 `The freeing up of ... occurs in`，全部换成短小有力的本位动词（`limits`, `consume`, `congest`, `complicate`, `frees`, `reclaim`）。

#### 示范 6：获奖/人类差文零数字摘要 → 完整量化与代价闭环（原出处：`LLM.265`, MICRO'25, `EX-04` & `iThreads`, ASPLOS'15, `EX-05`）
- **Bad（原文节选）**：
  > Building on insights gained from video codecs, we further show that the hardware of the video codecs can be customized and enhanced to significantly improve tensor encoding/decoding throughput without incurring substantial costs, making it a highly effective solution for large-scale model deployment without requiring significant modifications to the existing GPU architecture.
- **Good（模板化改写示范，数字占位符供作者填入实测值）**：
  > By customizing GPU video codec blocks with `<specific HW change>`, LLM.265 raises tensor compression throughput by `<X×>` and cuts KV-cache/weight memory footprint by `<Y%>`, while adding only `<Z%>` die area and `<W%>` accuracy drop across `<N>` LLM benchmarks.
- **改写心法**：把连续四个空洞形容词（`significantly`, `substantial`, `highly effective`, `significant`）与分词拖尾（`, making it...`）全部拔除，替换为**“具体硬件改动 + 收益数值 + 面积/精度代价 + 负载规模”**四元组。

---

### 5.2 Phase 2 Skill 可直接落地的硬规则与自动化检查阈值

供 Phase 2 写作与审校 Skill 直接编入 System Prompt 与 Python Linter：

1. **红灯禁词表（零容忍，除非为 ARM `Realm` 等专有名词或直接引用他人标题）**：
   - 紫文词：`delve`（肯定句）、`pivotal`、`paramount`、`meticulous(ly)`、`multifaceted`、`intricate`、`ever-evolving`、`unravel`、`harmoniz*`、`empower`、`foster`、`streamline`、`unveil`、`valiant`、`groundbreaking`、`transformative`、`democratiz*`、`captivated`。
   - 空心搭配：`in the ... realm of`、`broader landscape`、`pave the way`、`delicate balance`、`has recently emerged as a promising candidate`、`Despite its great potential`、`killer computer applications`、`Comprehensive evaluation shows`。
2. **黄灯限流表（每万词上限，超出即触发改写）**：
   - `enhance` ≤ 0.5、`facilitate` ≤ 0.3、`underscore` ≤ 0.2、`seamless(ly)` ≤ 0.3、`holistic` ≤ 0.2、`paradigm` ≤ 0.5、`synerg*` ≤ 0.2、`crucial` ≤ 0.6、`novel` 全文 ≤ 2 次（最好 0 次）、`utilize` 全文 ≤ 2 次（优先 `use`）、`leverage` ≤ 2.0。
   - 句法限流：句首 `Additionally,` ≤ 0.8/万词；`, enabling` ≤ 0.8/万词；`, ensuring` ≤ 0.3/万词；`, thereby ...ing` ≤ 0.8/万词；`not only ... but also` ≤ 0.6/万词；`Challenge I/II/III` 模板仅在确实存在正交物理挑战时使用，禁止强行凑三。
3. **正向风味基准（纯人工健康区间）**：
   - 被动语态密度控制在 **55–90 / 万词**（连续被动句绝不超过 **2 句**，防止 Class A 被动墙）。
   - 因果显性度：`because` + `since` + `hence` 合计应明显高于 `, enabling` + `, ensuring` + `, thereby`（健康比值 ≥ 5:1）。
   - 摘要与结论硬指标：Abstract 必须含 **至少 1 组收益数字 + 1 组开销/约束或测试集规模**；Conclusion 限 **1 段 5–7 句**，收束于带边界假设的端到端数字，零口号。
   - **禁止误杀**：允许并鼓励在定义与机制补注中规范使用 LaTeX 长破折号 `---`（健康密度 4–10 / 万词）；绝不把 `---` 用于数值范围（数值范围一律用 `--`）。
4. **命名、术语与微排版铁律**：
   - 系统名优先 1–2 音节朴素词、语义复合词或干脆不造名（纯机制标题）；**禁用 Forced Backronym**。
   - 本文**新造**硬件结构缩写 ≤ 5 个，严禁字母汤撞车，严禁中途改名或重定义旧缩写；系统名必须用 LaTeX 宏全局锁定。
   - 交叉引用按目标顶会单选锁死（ASPLOS: `Figure` + `§` 或 `Section`；HPCA: 禁用 `§`，选 `Figure`/`Fig.` + `Section`/`Sec.`；ISCA/MICRO: `Figure` + `Section`）；**永远全拼 `Table`**；`e.g.,` / `i.e.,` **强制加逗号**；引文通过**遮挡测试**（零句首 `In [X],`，零裸 `[X] Verb`），加载 `cite`/`natbib` 自动排序合并。
5. **终稿发稿前自动化正则自检清单（6 项必过）**：
   - `\[\d+.*\?` 或 `\?\?`（拦截 `PF-LLM` 式未解析引文）
   - `<latexit|TODO|FIXME|XXX`（拦截 `LLM.265` 式工具残片）
   - `\b(\w+)\s+\1\b`（拦截 `Duwe` `"the the"` 及 `Chasing Carbon` 残片）
   - `\(.*[^)]$` 跨段未闭合括号与不配对引号（拦截 `Chasing Carbon` p. 2 与 `AVA` `”compatible”`）
   - `\b(Fig|Sec|Tab)\.\d` 无空格引用及 `,` 后缺空格（拦截 `QPlacer` `Fig.1` 与 `Turnpike` `ainment,Turnstile`）
   - `\b(doesn't|don't|can't|won't|isn't|aren't)\b` 学术禁用口语缩写（拦截 `Hestia` p. 5 缝合断层）与 `\b(In\s+\[\d+|^\[\d+\]\s+[a-z]+ed)\b`（拦截引文作名词）。

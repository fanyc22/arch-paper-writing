# 维度五：实验方法论、评估叙事、定量修辞、相关工作、结论与四大顶会风格矩阵（2011–2026）

> **分析范围与语料审计**
> - **宏观语料池（`macro_pool`）**：共 **152 篇**（ISCA / MICRO / HPCA / ASPLOS 各 38 篇；按时代划分为 `2011–2015` 47 篇、`2016–2022` 65 篇、`2023–2026` 40 篇）。全部统计直接基于 `corpus/macro_cache/<paper_id>.json` 自动抽取与人工抽检复核。
> - **深度精读集（`deep_read` 48 篇中完成全文后半部与方法/评估/相关工作/结论逐页精读 41 篇）**：覆盖 **25 篇 `exemplar`**（ISCA 7、MICRO 6、HPCA 5、ASPLOS 7）、**全部 10 篇 `contrast_ordinary`**（普通录用人类论文）与 **全部 6 篇 `contrast_post2023`**（2024–2026 年带明显 AI 润色/模板化/过度宣传痕迹的录用论文）。
> - **严格零泄漏承诺**：`manifest.json` 中 8 篇 `held_out_test` 论文从未读取、未纳入任何统计、未在本报告中引用。
> - **引用规范**：全部英文引文均为 `corpus/macro_cache/<paper_id>.json` 中的逐字原句，标注格式为 `(ShortName, VENUE YEAR, paper_id, p. X)`。

---

## 0. 核心发现总览（Macro + Micro 交叉印证）

在系统拆解七大子维度之前，先给出 152 篇宏观扫描与 41 篇精读得出的六个最反直觉、最具区分度的核心信号：

| 观察指标 | `exemplar` (n=32) | `contrast_ordinary` (n=10) | `contrast_post2023` (n=6) | 全池 152 篇趋势（`2011–15` → `2016–22` → `2023–26`） |
|---|---:|---:|---:|---|
| **Methodology 中位字数** | **768w** | 688w（分化极大：95w–3,161w） | **1,073w**（偏臃肿） | 765w → 807w → **908w** |
| **Evaluation 中位字数** | 2,049w | 2,188w | 2,410w | 2,241w → 2,041w → 2,311w（ASPLOS 最长 **2,638w**） |
| **评估负面/诚实披露密度（次/千词）** | **1.72** | 0.86（低 2.0×） | **0.72**（低 **2.4×**） | 顶会顶尖论文讨论退化/局限的频率是 AI 味论文的 **2.4 倍** |
| **正文 AI 浮夸词频（次/篇）** | 1.66 | 0.90 | **12.33** | 0.60 → 0.85 → **4.08**（15 年暴涨 **6.8 倍**） |
| **评估百分比两位小数占比** | 7.8%（整数占 70.0%） | 8.5%（整数占 85.5%） | **33.9%**（高 **4.3×**） | 4.5% → 4.6% → **13.2%**（虚假精度蔓延） |
| **Related Work 后置比例** | **96.3%** (26/27) | 87.5% (7/8) | 80.0% (4/5) | 88.1% → 85.2% → **93.3%**（ASPLOS 高达 **97.0%**） |
| **RW 句首直接 `[引用]/Author` 比例** | 4.75% | 2.33% | **8.67%**（流水账抬头） | 4.56% → 5.01% → 5.07% |
| **独立 Discussion / Limitations 章节** | **37.5% / 12.5%** | 30.0% / **0.0%** | **16.7% / 0.0%** | Discussion: 25.5% → 26.2% → **35.0%** |
| **Conclusion 中位字数 / 句数** | 160w / 7 句 | 176w / 7 句 | **107.5w / 4.5 句** | **199.5w (9句) → 165.5w (8句) → 107.0w (5句)** |
| **Abstract–Conclusion 3-gram 重合率** | **9.51%** | 10.66% | **18.07%**（近 2×） | 11.13% → 9.91% → 12.34%（个别高达 44.1%） |
| **Conclusion 含 AI 浮夸词比例** | 16.1%（含晚近顶奖污染） | 0.0% | 16.7% | **0.0% → 4.7% → 12.8%** |

**批判性总纲**：不要把“顶会录用”甚至“Best Paper”等同于“写作范本”。精读揭示了一个清晰的三分格局：
1. **顶级人类工匠**（如 *Swarm*, *Vector Runahead*, *SALP*, *InvisiSpec*, *MorphCore*, *Pond*, *Autonomous NIC Offloads*, *PVCoherence*, *DynamoLLM*, *uPIMulator*）：方法论干练且死磕基线公平性，评估按机制而非按柱子讲故事，主动剖析 slowdown/outlier/噪声边界，结论克制收尾。
2. **平庸人类缺陷**（`contrast_ordinary`）：机械念柱状图、正文/表格/插图三重复写、有效数字乱象、省略关键 head-to-head 基线、流水账 Related Work。
3. **2023–2026 AI 润色侵蚀**（既重灾于 `contrast_post2023`，也已渗入 2024–2026 年的 **Best Paper** 如 *PF-LLM*, *LLM.265*, *Constable*）：一路高歌猛进零反思、用形容词代替机制归因、两位甚至四位小数噪音、Conclusion 沦为 Abstract 的低信息量同义改写加宏大愿景口号。

---

## 1. 实验方法论章节工艺（Evaluation Methodology Craft）

### 1.1 篇幅控制与章节形态：0.5–1.0 页的“表文分工”法则

152 篇全池中，实验方法论呈现两种主流组织：**独立一级章节**（59 篇，常见于 ISCA 18、HPCA 18、MICRO 14）与 **Evaluation 下的首节子章节**（49 篇，如 `Experimental Setup` / `Methodology`；在 `2023–2026` 时代子章节占比反超，达 21 vs 15）。

真正拉开档次的不是叫独立章还是子章节，而是**信息密度与表文分工**：
- **`exemplar` 黄金区间为 430–850 词（中位 768 词，约 0.5–0.9 页）**，例如 *Vector Runahead* (430w)、*Scale-SRS* (468w)、*Contiguitas* (552w)、*PVCoherence* (668w)、*DaDianNao* (748w)、*DynamoLLM* (768w)、*SALP* (771w)、*Elastic Cuckoo* (807w)、*Swarm* (830w)、*MorphCore* (852w)。
- 反观极端分化：部分平庸论文要么偷工减料（*AVA* 95w、*Alvarez15* 137w，把关键建模假设藏在正文夹缝里），要么陷入参数倾倒（*Turnpike* 3,161w，*PICACHU* 方法与实现混写达 5,226w）。而 `exemplar` 中超过 2,000 词的特例均属于**需要系统级建构/原型校准的重量级实证或工具论文**（*CloudSuite* 1,957w、*Eyeriss* 2,075w、*Pond* 2,091w、*HFI* 2,524w、*Darwin* 3,012w）——它们的篇幅花在**实验可信度论证**而非无意义的参数罗列上。

**顶尖论文的标准四模块骨架**（对应 4 个清晰加粗段落或 4 个紧凑子节）：
1. **Simulation / Prototype Platform & Validation**（仿真器/FPGA/真机/流片版本 + 关键校准误差边界）；
2. **Area, Power & Timing Modeling**（CACTI/McPAT/DSENT/Synopsys DC/Cadence Innovus + 工艺节点、电压/频率、缩放到同工艺的换算口径）；
3. **Workloads & Input Selection Rationale**（不仅列套件名，更交代*为何选这批、为何筛掉某些子项、SimPoint/warmup 窗口长度*）；
4. **Baselines & Fairness Justification**（不仅列竞品名，更交代*如何保证竞品不是稻草人*）。

**配置表铁律**：把所有静态微架构数字（ROB/IQ/LSQ/L1/L2/LLC 容量与延迟、DRAM 时序参数、带宽、工艺节点）一次性收进 `Table X: System / Baseline Configuration`，**正文严禁重复念表格里的数字**，正文只负责解释“为什么采用这一配置”以及“模型有哪些简化假设”。

### 1.2 平台校准与面积/功耗建模的“诚实交代”

顶会审稿人最警惕“黑箱仿真器”和“漏算外围电路的面积/功耗声明”。一流论文在方法论阶段就主动封堵质疑：

- **仿真器 vs 真机交叉验证（Simulator Validation）**：
  - *Contiguitas* (`conf__isca__ZhaoXWSYMWRST023`, ISCA 2023 Best Paper, p. 11) 专门用 `Linux-Sim` 与 `Linux-Real` 实机比对，直接报出误差区间（`-6%` 到 `+10%`），而非空口声称“高保真”。
  - *Pond* (`conf__asplos__LiBHEZNSRLAHFB23`, ASPLOS 2023 Distinguished, p. 9–10) 在实机方法论中明确声明 BIOS 关闭 Hyper-Threading、Turbo Boost 与 C-states 以压低噪声，并报告实验规模与复现抽检：
    > "With multiple repetitions and 158 workloads, our evaluation spans more than 3,500 experiments and 10,000 machine hours. Most experiments used lab servers; we spot check outliers on production servers." (Pond, ASPLOS 2023, `conf__asplos__LiBHEZNSRLAHFB23`, p. 10)
- **明确暴露建模局限（Model Disclaimers）**：
  - *Swarm* (`conf__micro__JeffreySYES15`, MICRO 2015 Best Paper, p. 9) 在方法论中直接用加粗标题自曝理想化假设，不藏着掖着：
    > "**Idealized memory allocation:** ... Designing concurrent, high-performance allocators is complex [26, 65]. Instead, the simulator allocates and frees memory in a single cycle." (Swarm, MICRO 2015, `conf__micro__JeffreySYES15`, p. 9)
  - *InvisiSpec* (`conf__micro__YanCS0FT18`, MICRO 2018, p. 13) 使用 CACTI 报完 SB 面积/功耗后，主动加一句防过度解读声明：明确指出 CACTI 估计 *does not include random logic*。
  - *Constable* (`conf__isca__BeraRRMNGOKSSM24`, ISCA 2024 Best Paper, p. 10–11) 用 CACTI 7.0（22nm）按明确公式缩放到 14nm，并额外用 3,400 条 trace 做 Golden-Check 功能正确性验证。

### 1.3 工作负载筛选与基线公平性（防“稻草人基线”的金标准）

判断一篇体系结构论文方法论是否达到 Best Paper 水准，**最硬的试金石是“对竞品基线的善意与苛刻程度”**。

| 公平性黄金做法 | 顶尖正例（Verbatim 证据） | 反面教材（平庸/AI 论文缺陷） |
|---|---|---|
| **主动调优竞品参数** | *Constable* (ISCA 24 Best Paper, `conf__isca__BeraRRMNGOKSSM24`, p. 11): *"For EVES, we use the optimized implementation that won the first championship value prediction (CVP-1) in the 32 KB storage budget track [4]. ... For RFP, we sweep and select the configuration parameter values that provide the highest performance benefit over the baseline."* | *Turnpike* (MICRO 21, `conf__micro__ZengKLJ21`, p. 11) 面对在 4-entry SB 上表现很差的竞品 Turnstile，虽做了扩大 SB 的敏感性，却在正文里带着炫耀口吻写 *"to highlight the performance of Turnpike, we enlarge the store buffer of Turnstile—though it performs poorly..."* |
| **验证基线未注水（Anti-Sandbagging）** | *DaDianNao* (MICRO 14 Best Paper, `conf__micro__ChenLLZHWLCXST14`, p. 9) 在拿自研芯片比 NVIDIA GPU 之前，先证明自己的 CUDA Convnet 基线比多核 SIMD CPU 快 `4.07×`、与 Ciresan 等人文献一致（`10×–60×`），排除“写了个慢 GPU 代码刷倍数”的嫌疑。 | *TimeCache* (ISCA 21, `conf__isca__OjhaD21`, p. 8–9) 整篇评估**完全没有与任何已有安全缓存方案做定量 head-to-head 对比**，只和无防护基线比开销。 |
| **给竞品上“加强版/理想版”并测试组合增益** | *Vector Runahead* (ISCA 21, `conf__isca__NaithaniA0E21`, p. 9–10) 不仅给竞品 PRE 理想化 stalling-slice 表，还专门评测加强版 PRE（多带来 `3.5%` 增益）以确认自身仍有压倒性优势；*Constable* (p. 11) 除单挑 `EVES` 外还测 `EVES+Constable` 与 `EVES+Ideal Constable`。 | *PICACHU* (ASPLOS 25, `conf__asplos__QinXT0Z25`, p. 9, 12) 方法论拼写出错（*"we comapre PICACHU against Gemmini [27] and Tandem [28]"*），对比 Tandem 时在正文只报单点峰值（*"maximum speedup of 1.55×"*），不报几何平均。 |
| **诚实交代剔除的子测试集** | *PVCoherence* (HPCA 14 Best Paper, `conf__hpca__ZhangBES14`, p. 10) 明确交代 PARSEC 中剔除了 `streamcluster` 和 `fluidanimate`（因与 gem5 不兼容），并援引 Alameldeen & Wood 跑多次仿真加 `±1 std-dev` 误差棒；*Swarm* (p. 9) 明确解释为何 `astar` 没有软件并行基线（会牺牲解质量）以及为何 `bfs` 选 2799 层深图。 | 许多普通论文直接写 *"we evaluate 12 SPEC benchmarks"*，从不解释为什么少了其余 17 个——审稿人默认你在 cherry-pick。 |

---

## 2. 评估叙事编排（Evaluation Narrative Choreography）

### 2.1 经典五段式评估叙事弧线

精读 25 篇 `exemplar` 表明，顶会一流评估绝不是把所有图按做实验的先后顺序堆出来，而是严格遵循**“结论先行 → 因果拆解 → 边界扫频 → 代价结算 → 异常深挖”**的五段式认知推进：

1. **Stage 1：Headline End-to-End Results（主指标总览）**
   先直接回答引言抛出的核心主张：端到端性能（Speedup / Throughput / Tail Latency）、能效（Energy / EDP / ED²P）或芯片面积归一化性能。给出总体均值（Geomean / Harmonic Mean / Weighted Speedup）与分布区间，并按**工作负载微架构行为特征**（而非字母序）分群解读。
2. **Stage 2：Mechanism Attribution & Ablation（因果归因与消融拆解）**
   这是区分“真体系结构贡献”和“黑箱调参”的分水岭——必须用增量消融（Additive Ablation）或组件贡献分解证明**每一项设计机制各自贡献了多少增益、为什么起作用**。
   - **极简典范**（仅用 1 段清晰递进）：*Vector Runahead* (`conf__isca__NaithaniA0E21`, ISCA 2021, p. 10) 一口气把整体 `1.79×` 拆成三阶物理因果：
     > "This same reordering, implemented with 64 scalar micro-ops instead of 8 vector micro-ops, is still sufficient to gain an average 1.47× speedup. The optimization of packing these into fewer vector operations, due to their now-SIMD layout, increases performance to 1.69× by virtue of improving compute throughput and by requiring fewer issue queue slots so that loads can issue earlier. Finally, altering the termination condition, such that Vector Runahead completes the entire chain of memory accesses before exiting, allows it to cover longer chains, of multiple main memory accesses..." (Vector Runahead, ISCA 2021, `conf__isca__NaithaniA0E21`, p. 10)
   - **反直觉阶梯瀑布流（Waterfall Attribution）**：*Darwin* (`conf__asplos__TurakhiaBD18`, ASPLOS 2018 Best Paper, p. 11) 用 Fig. 13 逐步把软件基线 `Graphmap` 变换到 `Darwin`，**第一步就诚实展示纯软件改用 D-SOFT+GACT 反而带来 `2.1× slowdown`**，随后靠 GACT 硬件加速（`380×`）、4 通道 DRAM + SRAM bins（`61×`）、流水化（`1.4×`）层层翻盘——这种“先抑后扬”的瀑布拆解把软硬件协同设计的必要性讲透了。
   - **AI 味消融反例**：*FastTTS* (`conf__asplos__ChenML0MLF26`, ASPLOS 2026, p. 11) 写了整整三段消融分析，充斥 *"minimizing evictions is paramount"*、*"significant"*、*"substantial"* 等空洞定性词，却**通篇几乎不给增量数字**，读完仍不知道三个技巧各占几成。
3. **Stage 3：Sensitivity & Scalability Sweeps（参数敏感性与扩展性扫频）**
   检验设计是否脆弱（如核数、缓存容量、DRAM 通道/Bank 数、负载压力、延迟预算、频率惩罚）。高水平写法不是画 10 张单调曲线，而是**寻找拐点（Knee）、饱和区（Saturation）和解析规律**：
   - *MorphCore* (`conf__micro__KhubaibSHWP12`, MICRO 2012 Best Paper, p. 9) 直接给出频率惩罚的闭式经验律：
     > "For an X% frequency penalty, performance of ST and MT workloads reduces by ∼ X/2% and X% respectively as compared to a MorphCore with no frequency penalty. This is because our ST workloads are core+memory bound while our MT workloads are mostly core bound." (MorphCore, MICRO 2012, `conf__micro__KhubaibSHWP12`, p. 9)
   - *DynamoLLM* (`conf__hpca__StojkovicZGTC25`, HPCA 2025 Best Paper, p. 10–11) 揭示负载越高节能递减（`51% → 40% → 23.4%`）以及 Pool 数量的 **U 型拐点**（`2/4` 太粗粒度、`9` 最优、`12/16` 碎片化反噬）。
4. **Stage 4：Overhead, Hardware Cost & Verification（面积/功耗/流量/代码复杂度结算）**
   芯片面积（mm² 与占比）、静态/动态功耗、片上网络流量、存储开销、内核代码改动行数（如 *Autonomous NIC Offloads*, ASPLOS 2021, p. 11–13 精确报告 `568 LoC` / `210 LoC` 以及实验标准差 `<1.6%` / `<2.61%`）。
5. **Stage 5：Case Studies, Outliers & Adversarial Stress Tests（异常解剖与最坏情况压测）**
   用微架构显微镜头解剖退化样本或对抗性极端场景。例如 *Contiguitas* (ISCA 2023 Best Paper, p. 11) 主动构造关闭大页、每秒 1,000 次不可移动分配的 `Very High` 对抗性最坏压力测试，证明即便在极端退化下开销也仅 `0.2% / 0.3%`；*Swarm* (MICRO 2015 Best Paper, p. 11–12) 专门做 100 Kcycle 的 `astar` 细粒度执行轨迹解剖，并借助 Table 5 理想化剥离把看似惊人的“超线性 `122×`”诚实拆回 `54×` 纯并行增益（其余来自缓存局部性）。

### 2.2 负面结果、性能退化与异常值处理：最强的“人类可信度指纹”

宏观统计显示，`exemplar` 在评估中讨论退化/局限/异常的密度为 **1.72 次/千词**，是 `contrast_ordinary`（0.86）的 **2.0 倍**、是 `contrast_post2023`（0.72）的 **2.4 倍**。**AI 生成或深度 AI 润色文本最致命的破绽之一，就是把实验写成“全胜凯歌”**（哪怕图中明明输了一半也硬夸 *"consistently achieves superior performance"*）。

以下是顶会顶尖作者处理负面结果与异常值的 **五种高信任度范式**（全部附逐字原句）：

1. **直接承认局部输给竞品，阐明架构权衡的本质**：
   - *MorphCore* (`conf__micro__KhubaibSHWP12`, MICRO 2012 Best Paper, p. 8–9) 毫不遮掩自己在单线程下频率慢 `2.5%`、性能略输 OOO-2，在多线程下又输给小核与 CoreFusion（`-8%`），靠“全场景综合权衡胜出”赢得审稿人彻底信服：
     > "MorphCore runs at a 2.5% slower frequency than OOO-2, achieving 98.8% of the performance of OOO-2." (MorphCore, MICRO 2012, `conf__micro__KhubaibSHWP12`, p. 8)
   - *Swarm* (`conf__micro__JeffreySYES15`, MICRO 2015 Best Paper, p. 10) 坦白单核开倒车与多核局部不如软件实现：
     > "At 1 core, Swarm is 33% slower than serial bfs; however, Swarm scales to 43× at 64 cores." (Swarm, MICRO 2015, `conf__micro__JeffreySYES15`, p. 10)
   - *SIGMA* (`conf__hpca__QinSKNS0KK20`, HPCA 2020 Best Paper, p. 12) 主动解释为何在两个 GEMM 上输给 Eyeriss v2（单操作数驻留 vs 双操作数驻留），并坦承功耗高 2× 但被 6× 加速抵消。
2. **主动暴露高昂开销与最坏情况样本，并拆解微架构成因**：
   - *InvisiSpec* (`conf__micro__YanCS0FT18`, MICRO 2018, p. 11) 面对安全防护的巨大代价，第一句话就给实话，紧跟三大微架构根因：
     > "Under TSO, the average execution time of IS-Sp and IS-Fu is 22% and 80% higher, respectively, than Base. There are three main reasons for the slowdowns of IS-Sp and IS-Fu: validation stalls, lack of cache state reuse after branch squash, and contention due to two accesses per load." (InvisiSpec, MICRO 2018, `conf__micro__YanCS0FT18`, p. 11)
     随后更直接点名最坏情况 `omnetpp`（~100% 退化）与 `gamess`/`cactusADM`/`tonto`（100%–150%）。
   - *DynamoLLM* (`conf__hpca__StojkovicZGTC25`, HPCA 2025 Best Paper, p. 10) 既报 P99 改善，也把同一句话里 P50 变慢端上桌，还诚实承认省下的电费（`$4.4/hr`）在昂贵 GPU VM 租金（`$1362.7/hr`）面前微乎其微：
     > "[DynamoLLM reduces] the P99 TTFT and TBT latencies by 5.3% and 11.1% over SinglePool, respectively, while it increases the P50 TTFT and TBT latencies by 11.4% and 7.6%, respectively." (DynamoLLM, HPCA 2025, `conf__hpca__StojkovicZGTC25`, p. 10)
3. **诚实披露零增益（Null Result）与“噪声内无意义加速”**：
   - *PVCoherence* (`conf__hpca__ZhangBES14`, HPCA 2014 Best Paper, p. 10) 拒绝把仿真噪声吹成性能提升——这是教科书级别的科学克制：
     > "While there are some differences in the runtimes, they are “within the noise.” On some benchmarks, PV-MOESI even has a marginally shorter runtime than OP-MOESI, but these differences are also within the noise and are not meaningful speedups." (PVCoherence, HPCA 2014, `conf__hpca__ZhangBES14`, p. 10)
   - *Elastic Cuckoo* (`conf__asplos__SkarlatosKXT20`, ASPLOS 2020 Best Paper, p. 12) 专门划出一组低页表遍历开销应用（`MCF`, `Cactus`, `Streamcluster`, `XSBench`），坦白在 THP 下几乎无收益且没有劣化。
4. **用底层机制化解与前人文献的“反直觉分歧”**：
   - *Autonomous NIC Offloads* (`conf__asplos__PismennyEYL0T21`, ASPLOS 2021 Distinguished, p. 13) 面对与前人 RDMA 扩展性研究相反的现象，精准定位到包批处理退化机制：
     > "TCP packet batching becomes less effective with more connections: from 48 packets per batch with 128 connections, to only 8 packets per batch with 128 K connections." (Autonomous NIC Offloads, ASPLOS 2021, `conf__asplos__PismennyEYL0T21`, p. 13)
5. **反面警示——AI 式“遮丑”如何毁掉可信度**：
   - *QPlacer* (`conf__isca__Zhang0D0AO0B0025`, ISCA 2025, p. 9–10) 正文反复高唱 *"Qplacer consistently achieves superior performance"*，然而翻到 Fig. 13（p. 10），在 6 个拓扑中有 3 个（`Aspen-11`, `Aspen-M`, `Grid`）面积比 Classic 基线更差或被基线反超（`0.951`, `0.863`, `0.834`），正文却几乎一笔带过，毫无微架构归因。审稿人一旦核对图与文，信任瞬间清零。

---

## 3. 定量修辞与克制规范（Quantitative Rhetoric & Restraint）

### 3.1 趋势综合（Trend Synthesis）vs 机械念柱状图（Bar-Chart Narration）

这是体系结构评估写作中最容易拉高或拉低档次的修辞分水岭。下面给出逐字正反对照：

| 维度 | 顶尖示范：趋势综合 + 机制分群（Trend Synthesis） | 平庸/AI 反面教材：机械念柱状图 / 空泛贴标签 |
|---|---|---|
| **逐字原文** | *"The average memory-intensity of the rightmost applications (i.e., those that gain >5% performance with SALP-1) is 18.4 MPKI (last-level cache misses per kilo-instruction), compared to 1.14 MPKI of the leftmost applications. Second, the advantage of SALP-2 is large for applications that are write-intensive. ... In Figure 13, the three applications (that improve more than 38% with SALP-2) are among both the most memory-intensive (>25 MPKI) and the most write-intensive (>15 WMPKI)."* <br>— (SALP, ISCA 2012, `conf__isca__KimSLLM12`, p. 10) | **机械逐个报菜名（人类平庸）**：<br>*"The first application is Axpy, which represents the ideal scenario for both RG and AVA where RG-LMUL8 and AVA X8 obtain the same performance... The second application is Blackscholes... For LavaMD2... For Particle-Filter... For Somier... Finally, for Swaptions..."* <br>— (AVA, HPCA 2022, `conf__hpca__LazoRMBVSCUC22`, p. 8–10)<br><br>**AI 夸张修辞替代机制解释**：<br>*"Taking 2mm as an example, pinpointing the bug location with Cider demands a formidable 50,207 steps, a testament to its granularity. Conversely, Hestia streamlines the process, requiring merely 2,083 steps..."* <br>— (Hestia, MICRO 2024, `conf__micro__XuLZLW0024`, p. 9) |
| **写作本质差异** | **不按基准名逐一朗读**，而是把 20+ 条柱子按**决定性微架构特征**（`MPKI > 18.4` vs `1.14`、`WMPKI > 15`）聚类成 2–3 个**制度区间（Regimes）**，解释为什么左半边收益微弱、右半边突破 38%，并顺势解释为何个别异常（如 MASA 在少数负载上略逊于 SALP-2 因调度器推迟关键列命令）。 | *AVA* 把读者当成瞎子，按字母序逐一朗读 24 张小图里肉眼可见的柱高，还出现科学计数法刻度 `4.E+06` 与图例拼写错误 `"Naïve X3"`；*Hestia* 用 *"formidable"*、*"a testament to"*、*"streamlines"*、*"merely"* 强行拔高情绪，却没有解释底层抽象层如何剪枝搜索空间。 |

另一类常见平庸病是**“正文-表格-插图三重复写”**与**“正文完全不给数字”**：
- **三重复写**：*TimeCache* (`conf__isca__OjhaD21`, ISCA 2021, p. 8–9) 把全部 33 个 SPEC 基准的精确数据塞进 Table 2，又把同一批数据画成 Fig. 8 和 Fig. 9，还出现低级逻辑与标点事故：
  > "TimeCache with 2MB, 4MB, and 8MB LLC sizes has an average performance overhead of 2.5%, 1.6%, and 1.7% The ratio of first access miss to the overall miss also varies inversely with the cache size." (TimeCache, ISCA 2021, `conf__isca__OjhaD21`, p. 8)
  ——既丢了句号，也没解释为何从 4MB 到 8MB 开销反而从 `1.6%` 反弹到 `1.7%`！
- **无数字空手挥舞**：*Chopim* (`conf__isca__ChoKLE20`, ISCA 2020, p. 10–11) 评估正文回避汇总均值，且 Fig. 12 横轴竟然跳过 `mix5`、重复打印两个 `mix7`。

### 3.2 均值规范与 `up to` 诚实配对

1. **均值口径的学科纪律**（152 篇实证分布）：
   - 归一化加速比 / 相对执行时间（Speedup / Normalized Performance）：必须用 **Geometric Mean**（全池 19.1% 论文明示，HPCA 最高 28.9%、MICRO 23.7%）。
   - 多道/多核吞吐量（Multi-programmed Throughput）：使用 **Weighted Speedup**（系统吞吐）或 **Harmonic Mean**（公平性/平均 IPC，如 ISCA 7.9% 明确区分二者）。
   - 绝对延迟/功耗/能耗求和与算术平均：仅对可加物理量（如总能耗、总时间、绝对延迟）使用 **Arithmetic Mean**，绝不对归一化比率求算术平均。
2. **`up to` 必须与均值成对出现（Anti-Cherry-Picking Rule）**：
   - 全池 152 篇中，正文评估段内 `up to` 在 ±1 句内配对均值/几何平均的比例仅 27.8%（MICRO 35.6%、ISCA 33.3%、HPCA 31.2%、ASPLOS 16.9%；若放宽到全文正文约 43%–47%）。
   - **必须规避的反例**：*PICACHU* (`conf__asplos__QinXT0Z25`, ASPLOS 2025, p. 12) 写 *"PICACHU outperforms Tandem on both LLMs with a maximum speedup of 1.55×"*，刻意不给对 Tandem 的平均加速比；*DaDianNao* (MICRO 2014 Best Paper, p. 1, 10, 12) 在摘要和结论用 64 节点集群对单块 GPU 报 `"up to 450.65x"`，未并列单节点或等面积归一化收益。
   - **正确示范**：一律采用 **"by X% on average (up to Y%)"** 或 **"an average speedup of X× (geomean), reaching up to Y× on [specific regime]"**，均值在前、峰值在后且限定触发场景。

### 3.3 符号统一（`%` vs `×`）与精度克制（反虚假精度）

1. **`%` vs `×` 的分界与排版纪律**：
   - **惯例分界**：幅度 `< 100%`（即 `< 2×`）或描述开销/功耗/面积下降时优先用 **`%`**（如 `18% speedup`, `22% overhead`, `43% energy reduction`）；幅度 `≥ 2×` 或跨代/加速器倍率时用 **`×`**（`1.47×` 到 `43×`），且**全文严禁混用 `2x` / `6×` / `3X` / `times`**（连 HPCA 2020 Best Paper *SIGMA* p. 12 都在相邻三段混用 `2x`/`6×`/`3X`，*M-ANT* HPCA 2025 p. 13 甚至写出语法病句 *"average speedup of 1.70× speedup"*！）。
   - 严禁把 `2.1×` 和 `110%` 含糊混写，尤其要避免 *"reduces energy by 150.31x"*（严格说应为 `150× lower energy` 或 `99.3% energy reduction`，`reduce by >100%` 或 `reduce by Nx` 在物理量表达上极易惹怒挑剔审稿人）。
2. **有效数字纪律——拒绝“仿真器小数点幻觉”**：
   - 全池 152 篇统计显示，`exemplar` 评估中的百分比 **70.0% 用整数、22.0% 用 1 位小数**，合计 **92.0%** 不超过 1 位小数（ASPLOS 整数占比更达 **77.7%**，HPCA 1 位小数规范占比 **25.4%**）。
   - 反观 `contrast_post2023`，**两位小数百分比暴涨到 33.9%**（是 `exemplar` 7.8% 的 **4.3 倍**！），例如 *M-ANT* 通篇 `2.99×`、`4.46×`、`1.83×`、*QPlacer* 图表标满 `0.4698`、`0.6079`、`3.301`。
   - **什么时候允许 ≥3 位小数？** 全池核查 93 处 3+ 位小数百分比后确认：**只有两类极小物理量/可靠性指标合法**——如极高覆盖率 `99.999%`（*Nomura11*）、极低位翻转率 `0.00649%`（*RowHammer*, ISCA 2014）或极小芯片面积占比 `0.014%`（*Contiguitas*, ISCA 2023）。
   - **必须禁止的虚假精度灾难**：
     - 仿真误差 ±5% 却报 5–6 位有效数字：*DaDianNao* (`conf__micro__ChenLLZHWLCXST14`, MICRO 2014 Best Paper, p. 1, 10) 的 `"450.65x"`、`"150.31x"`、`"2595.23x"`；
     - CACTI 原始日志直接粘贴：*Turnpike* (`conf__micro__ZengKLJ21`, MICRO 2021, p. 10 Table 1) 的 `"0.43099 pJ"`，并配以误导性的四舍五入惊叹号 `"delivering 0% average overhead!"` (p. 9)；
     - 表格内有效数字完全失控：*TimeCache* (ISCA 2021, p. 8 Table 2) 同一张表混排 `0.888` / `0.0323` / `3.40` / `0.10145`；*iThreads* (`conf__asplos__Bhatotia0ABR15`, ASPLOS 2015, p. 10 Table 1) 打印荒诞的 `"170900.00%"` 与 `"72612.53%"`；*Hestia* (`conf__micro__XuLZLW0024`, MICRO 2024, p. 12 Table VI) 对耗时 4.3 天的仿真报告 `"373829.28"` 秒（精确到 0.01 秒！）。

---

## 4. 相关工作工艺（Related Work Craft）

### 4.1 位置演变（2011→2026）：后置已成绝对主流，仅特定场景采用“双层结构”

在 152 篇中成功定位独立 Related Work 的 126 篇论文里（其余 26 篇多为合并进 `Background and Related Work` 或省略独立章节），**后置（评估之后、结论之前）高达 88.1%（111/126）**，且在 15 年间进一步向后置收敛：

| 维度分层 | 检出篇数 | 后置（Late）比例 | 前置（Early）比例 | 中位字数 | 句首直接引用/作者占比 |
|---|---:|---:|---:|---:|---:|
| **时代：`2011–2015`** | 42 | 88.1% (37) | 11.9% (5) | 678w | 4.56% |
| **时代：`2016–2022`** | 54 | 85.2% (46) | 14.8% (8) | 537w | 5.01% |
| **时代：`2023–2026`** | 30 | **93.3% (28)** | 6.7% (2) | 541w | 5.07% |
| **会议：ASPLOS** | 33 | **97.0% (32)** | 3.0% (1) | 574w | **2.71%**（最不流水账） |
| **会议：MICRO** | 27 | 88.9% (24) | 11.1% (3) | 585w | 6.67% |
| **会议：ISCA** | 33 | 84.8% (28) | 15.2% (5) | 604w | 4.74% |
| **会议：HPCA** | 33 | 81.8% (27) | 18.2% (6) | **463w** | 5.73% |
| **层级：`exemplar`** | 27 | **96.3% (26)** | 3.7% (1) | **463w** | 4.75% |
| **层级：`contrast_ordinary`** | 8 | 87.5% (7) | 12.5% (1) | 729w | 2.33% |
| **层级：`contrast_post2023`** | 5 | 80.0% (4) | 20.0% (1) | 513w | **8.67%**（**1.8×** 流水账倾向） |

**为何 `exemplar` 96.3% 选择后置且更紧凑（463w vs 普通论文 729w）？**
因为在读完你的完整架构与评估之后，读者才具备与前人机制做精准、无冗余对照的上下文；前置 RW 容易在读者还没理解你到底做了什么之前就堆砌几十篇文献，拖慢进入核心思想的节奏。

**唯一合理的两类例外**：
1. **双层 Related Work（Two-Tier Pattern）**：在 Motivation / Background 中只针对**2–3 个最直接竞争者**做定量/机制对照以立住动机（如 *RowHammer*, ISCA 2014, p. 12 将外围文献收束为 `9. Other Related Work`；*M-ANT*, HPCA 2025, p. 2 将核心量化竞品前置进 `II. Background and Related Work`），其余宽口径文献后置收束。
2. **评估前定锚（Pre-Evaluation Anchor）**：极少数论文（如 *Constable*, ISCA 2024 Best Paper, `conf__isca__BeraRRMNGOKSSM24`, p. 9–10，作为 27 篇 exemplar 中唯一非严格后置的案例）将 `§7 Related Work` 紧贴 `§8 Evaluation` 之前，直接用来论证为何在评估中选择 EVES / ELAR / RFP 作为基线并提前切割与经典 Value Memoization 的三条根本区别。

### 4.2 设计轴分类法（Taxonomic Grouping）vs 文献流水账（Laundry-List）

顶尖相关工作与平庸/AI 相关工作的根本分野，在于**段落主语是“设计维度/底层假设”，还是“某年某作者”**：

- **顶尖范式（按机制假设切轴 + 结构化对比表）**：
  - *Constable* (`conf__isca__BeraRRMNGOKSSM24`, ISCA 2024 Best Paper, p. 10) 将前人指令记忆化（Memoization）工作按**三条底层硬件假设**（① 全指令盲目缓存导致 L1 级大表开销；② 延迟到源寄存器就绪才检索、无法释放保留站压力；③ 缺乏多核一致性与乱序正确性保证）逐一精准对位：
    > "First, prior works aim to memoize (multiple) results of every static instruction... Constable on the other hand (a) only targets loads, and (b) employs a confidence-based mechanism... Second, prior works may delay retrieving the memoized instruction output until its source register values are available [53, 76, 117, 149]. ... Constable, however, explicitly monitors changes in source architectural registers..." (Constable, ISCA 2024, `conf__isca__BeraRRMNGOKSSM24`, p. 10)
  - *uPIMulator* (`conf__hpca__HyunKLR24`, HPCA 2024 Best Paper, p. 13) 在 `Simulators for PIM` 小节先用四句浓缩四类模拟器，再集中用 `First ... Second ...` 提炼**前端自定义链接器**与**后端商用 Per-Bank PIM 建模**两条正交差异，并配 `Table III` 做定性维度矩阵——更难得的是，**在 Table III 里诚实给自己标出 `X`（不支持多线程仿真）**！
  - *Swarm* (MICRO 2015 Best Paper) 与 *SIGMA* (HPCA 2020 Best Paper, p. 12 Table III) 同样善用**分类小标题 + 机制对比表**，让审稿人 10 秒看清你的坐标位置。

- **反面教材——流水账（Laundry-List）与傲慢一刀切（Combative Sweeping Dismissal）**：
  - **经典流水账（`Author et al. [X]` 连续轰炸）**：*ρHammer* (`conf__micro__ChenTTLZQ25`, MICRO 2025, p. 12) 一整段连续以作者名开句，像文献笔记拼接：
    > "As discussed in Section 3.2, Pessl et al. [56] conducted the pioneering work that introduced a brute-force strategy... To reduce the brute-force search space, Wang et al. [65] proposed a knowledge-assisted approach... Jattke et al. [30] extended the strategy to AMD platforms..." (ρHammer, MICRO 2025, `conf__micro__ChenTTLZQ25`, p. 12)
    同理见 *Alvarez15* (`conf__isca__AlvarezVMCGMNAV15`, ISCA 2015, p. 11) 的 `6.1/6.2` 节，甚至顶会名篇 *SALP* (`conf__isca__KimSLLM12`, ISCA 2012, p. 11) 在写 DRAM 专利段时也偶有流水账滑坡。
  - **高风险对抗语气（Combative Dismissal）**：*Turnpike* (`conf__micro__ZengKLJ21`, MICRO 2021, p. 11) 用全称否定句一竿子打翻所有人——审稿人极可能就是你贬低的作者之一：
    > "All prior works either impose a large hardware cost or suffer a high run-time cost. To the best of our knowledge, Turnpike is the first, that reduces both costs effectively..." (Turnpike, MICRO 2021, `conf__micro__ZengKLJ21`, p. 11)
  - **正确语气（Generous, Precise, Orthogonal）**：先准确肯定前人在其目标场景或假设下的优势，再用中性词指出**目标/假设差异或正交互补关系**（如 *"orthogonal and can be combined with..."*、*"targets offline trace optimization, whereas our work operates online..."*、*"assumes 3D-stacked logic-layer PIM, whereas we model per-bank commercial PIM..."*）。

---

## 5. 讨论、局限性与结论章节（Discussion, Limitations & Conclusion）

### 5.1 2018–2026 的新刚需：结构化 `Discussion / Limitations`

宏观数据揭示了一个清晰趋势：独立 `Discussion` 章节比例从 `2011–2015` 的 **25.5%** 攀升至 `2023–2026` 的 **35.0%**；而在 `deep_read` 中，**`exemplar` 的 `Discussion` 占比达 37.5%、显式 `Limitations` 小节达 12.5%**，而 `contrast_ordinary` 与 `contrast_post2023` 的显式 `Limitations` 均为 **0.0%**！

顶尖 `Discussion / Limitations` 章节不是废话凑页数，而是**主动预判并拆除审稿人 Rebuttal 阶段最可能提出的三类致命质疑**：
1. **适用边界与未支持场景（Scope & Missing Features）**：
   - *PF-LLM* (`conf__asplos__XuSLBWLX026`, ASPLOS 2026 Best Paper, p. 13) 设 `7.4 Limitations`，坦诚列出两条硬伤（不支持 JIT 编译代码、依赖离线上采样剖析）：
     > "**7.4 Limitations:** We acknowledge two primary limitations of the current PF-LLM implementation. First, it does not natively support programs requiring Just-In-Time (JIT) compilation..." (PF-LLM, ASPLOS 2026, `conf__asplos__XuSLBWLX026`, p. 13)
   - *uPIMulator* (`conf__hpca__HyunKLR24`, HPCA 2024 Best Paper, p. 13) 直接专设独立一级大章 `VI. SIMULATOR LIMITATIONS AND FUTURE WORK`，开篇即认领缺失功耗/面积模型与 CPU↔DPU 通道保真度偏低两项短板。
2. **设计备选方案与安全/部署扩展（Design Alternatives & Generalizability）**：
   如 *InvisiSpec* (MICRO 2018) 讨论更强威胁模型与硬件复杂度权衡；*Contiguitas* (ISCA 2023 Best Paper) 讨论虚拟化、多页大小与非 Linux OS 迁移。
3. **警惕“伪 Discussion”反面教材**：
   - *Hestia* (`conf__micro__XuLZLW0024`, MICRO 2024, p. 12) 写了一个仅 4 句话的 `5) Discussion`，既无定量边际增量也无诚实局限剖析，纯粹重复上文吹捧自己，属于典型的“为了格式齐全而硬凑的空壳小节”。

### 5.2 结论（Conclusion）解剖学：15 年缩水近半与 AI 污染警报

152 篇（147 篇成功抽取 Conclusion）的跨时代演变呈现出惊人的三项结构漂移：
1. **长度腰斩**：中位数从 `2011–2015` 的 **199.5 词（9 句）** → `2016–2022` 的 **165.5 词（8 句）** → `2023–2026` 的 **107.0 词（5 句）**。当代顶会最佳实践明确收束到 **1 个紧凑自然段、90–150 词（4–6 句）**。
2. **时态漂移**：早期多用过去时（`2011–15` 过去时为主占 34.1% > 现在时 27.3%，如 *"We presented / evaluated / demonstrated"*）；2023–2026 现在时为主反超至 **46.2%**（过去时降至 15.4%）——部分反映写作提速，但更受 AI 习惯用 *"This paper presents..."* 直接复述摘要的强烈影响。
3. **重灾区：摘要复读机 + 宏大空洞收尾**：
   - Abstract–Conclusion 3-gram 重合率在 `exemplar` 中仅 **9.51%**，但在 `contrast_post2023` 中飙升至 **18.07%**（其中 *PICACHU* 高达 **44.1%**、*Hestia* 达 **26.6%**！）。
   - Conclusion 出现 AI 浮夸词的比例从 `2011–2015` 的 **0.0%（0/44）** 暴涨到 `2023–2026` 的 **12.8%（5/39）**。

**高下立判的 Conclusion 逐字对照**：

| 类型 | 逐字原句与出处 | 诊断 |
|---|---|---|
| **极简克制典范（人类精品）** | *"We have demonstrated, characterized, and analyzed the phenomenon of disturbance errors in modern commodity DRAM chips. These errors happen..."* <br>— (RowHammer, ISCA 2014, `conf__isca__KimDKFLLWLM14`, p. 12) | 过去时干脆定论，提炼核心科学发现与工程启示，无一字情绪煽动，不抄摘要原句。 |
| **过短敷衍（平庸人类）** | 仅 2 句话、26 词的结论段，草草收场。<br>— (Turnpike, MICRO 2021, `conf__micro__ZengKLJ21`, p. 11) | 缺乏高层 takeaway 与定量收束，像截稿前最后两分钟硬补的。 |
| **过长煽情（哪怕是 Best Paper 也不可学！）** | 432 词冗长 `Conclusion And Future Work`，并出现过度抒情比喻：*"Whole genome alignments [30] provide the rocket fuel for comparative genomics..."* <br>— (Darwin, ASPLOS 2018 Best Paper, `conf__asplos__TurakhiaBD18`, p. 13) | 把科普愿景与未来工作塞进结论，冲淡了正文硬核技术收尾的克制感。 |
| **AI 典型病灶 #1：摘要复读 + 陈词滥调** | *"...previous state-of-the-art accelerators in LLM inference, presenting a promising avenue for future research on implementing nonlinear operations in LLMs."* <br>— (PICACHU, ASPLOS 2025, `conf__asplos__QinXT0Z25`, p. 12，66 词，与摘要 3-gram 重合 **44.1%**) | 几乎原封不动改写摘要，用 *"presenting a promising avenue for future research"* 万金油句式收尾。 |
| **AI 典型病灶 #2：零数字 + 宏大口号** | *"FastTTS addresses these challenges through three novel synergistic techniques... It narrows their performance gap with cloud-scale models, and advances the vision of democratized agentic AI."* <br>— (FastTTS, ASPLOS 2026, `conf__asplos__ChenML0MLF26`, p. 13) | 通篇结论**零具体实验数字**，堆砌 *"novel synergistic"*、*"advances the vision of democratized agentic AI"* 等典型 LLM 腔调。 |

---

## 6. 四大顶会风格矩阵（ISCA vs MICRO vs HPCA vs ASPLOS）

基于 152 篇均衡语料（每会严格 **38 篇**，跨越 2011–2026）的自动化基础设施/修辞扫描，叠加 41 篇精读的定性体察，四大顶会在实验范式、软硬重心、统计习惯与文风上存在**极其鲜明的社区人格**：

### 6.1 152 篇实证指标对比表（每会 n = 38）

| 评估与写作特征 | **ISCA** | **MICRO** | **HPCA** | **ASPLOS** | 关键差异解读 |
|---|---:|---:|---:|---:|---|
| **RTL / VLSI 综合流片** (`rtl_vlsi_synth`) | **52.6%** (20) | 44.7% (17) | 39.5% (15) | 28.9% (11) | ISCA 最看重硬件可落地性与硅片综合证据 |
| **明确工艺节点** (`process_node`, e.g. 28/14/7nm) | **50.0%** (19) | 47.4% (18) | 47.4% (18) | **15.8%** (6) | ASPLOS 极少落到晶体管工艺节点 |
| **FPGA 原型 / FireSim** (`fpga_proto`) | **31.6%** (12) | 23.7% (9) | **10.5%** (4) | 23.7% (9) | ISCA 引领 FPGA 加速仿真与原型风潮 |
| **CACTI / McPAT / DSENT 面积功耗模型** | 34.2% (13) | **42.1%** (16) | 39.5% (15) | **15.8%** (6) | MICRO 最讲究微架构级面积/能量精细账 |
| **功耗指标深度报告** (`power_metric`) | 26.3% (10) | **39.5%** (15) | 28.9% (11) | 21.1% (8) | MICRO 功耗/EDP/ED²P 关注度居首 |
| **周期精确仿真** (`cycle_accurate`) | 44.7% (17) | 44.7% (17) | **50.0%** (19) | **10.5%** (4) | **ASPLOS 周期精确仿真仅其余三会的 1/4–1/5！** |
| **GPU / 加速器专用仿真** (`sim_gpu_accel`) | 10.5% (4) | 7.9% (3) | **34.2%** (13) | 7.9% (3) | HPCA 是 GPU/DNN/PIM 加速器仿真大本营（**3–4×**） |
| **Linux 内核 / OS / Hypervisor 修改** | 23.7% (9) | 15.8% (6) | 15.8% (6) | **42.1%** (16) | **ASPLOS 操作系统/内核实装占比高出其他三会 2–2.7×** |
| **真机服务器 / GPU / 集群实测** (`real_hw_os`) | 44.7% (17) | 60.5% (23) | 50.0% (19) | **73.7%** (28) | ASPLOS 近四分之三论文必须跑真实硬件与系统栈 |
| **Methodology 中位字数** | 859w | **963w** | **668w** | 778w | MICRO 参数最细密；HPCA 最紧凑 |
| **Evaluation 中位字数** | 2,149w | 2,045w | 1,977w | **2,638w** | ASPLOS 需要端到端系统剖析 + 尾延迟 + 微基准，评估最长 |
| **Geomean 明示占比** | 13.2% | 23.7% | **28.9%** | 10.5% | HPCA/MICRO 标准化汇总口径最严谨 |
| **评估百分比精度：整数 / 1位小数** | 69.0% / 19.7% | 72.5% / 19.8% | 72.3% / **25.4%** | **77.7%** / 9.3% | ASPLOS 偏向简洁整数；HPCA 最偏爱 1 位小数 |
| **Related Work 后置比例 / 中位字数** | 84.8% / 604w | 88.9% / 585w | 81.8% / **463w** | **97.0%** / 574w | ASPLOS 几乎全员后置 RW（且流水账比例最低 **2.71%**） |
| **独立 Discussion 章节占比** | **36.8%** | 34.2% | **13.2%** | 28.9% | ISCA/MICRO 重反思；HPCA 最直接、最少哲学讨论 |
| **评估负面/诚实披露密度（次/千词）** | **1.36** | 0.83 | 1.14 | **1.34** | ISCA 与 ASPLOS 对反常与代价披露最充分 |

### 6.2 四大会议定性写作画像（选刊与定制调性指南）

1. **ISCA — 宏大架构视野 × 硅片落地实证 × 深度反思**
   - **评估重心**：最偏爱“大架构洞见 + 扎实物理落点”（RTL 综合 **52.6%**、工艺节点 **50.0%**、FPGA **31.6%** 全场最高），兼顾工业界真实生产集群（如 *Contiguitas* Meta 生产部署）与前沿芯片流片（*Eyeriss*）。
   - **叙事调性**：视野最宽广、讨论最充分（Discussion **36.8%** 最高，诚实披露 **1.36/1k** 最高）。写 ISCA 评估时，切忌只盯着单点 IPC 小数点，要讲清楚**跨代可扩展性、真实面积/时序闭环与架构权衡边界**。
2. **MICRO — 极致微架构深度 × 精细功耗面积账 × 周期级因果**
   - **评估重心**：方法论最细密（中位 **963w** 最高），对片上结构面积/静态动态功耗（CACTI/McPAT **42.1%**、功耗指标 **39.5%** 均居第一）与流水线级停顿/带宽/缓存冲突归因要求最苛刻（如 *MorphCore*, *InvisiSpec*, *Swarm*, *Whisper*）。
   - **叙事调性**：像解剖精密机械表——审稿人会追问每一个新增队列的端口数、关键路径延迟与最坏情况退化。注意 MICRO 的 AI 浮夸词风险也是四会最高（**2.26 次/篇**，Conclusion 重合率 **14.88%**），投稿 MICRO 必须严守去形容词纪律。
3. **HPCA — 加速器与内存系统引擎 × 周期仿真扫频 × 干脆利落**
   - **评估重心**：周期精确仿真（**50.0%**）、GPU/加速器建模（**34.2%**，远超他会）与 Geomean 口径（**28.9%**）全面领跑，代表如 *SIGMA*, *Scale-SRS*, *uPIMulator*, *DynamoLLM*。
   - **叙事调性**：四会中最务实、最直接——方法论最精炼（**668w**），RW 最短（**463w**），独立 Discussion 仅 **13.2%**（全场最低）。写 HPCA 讲究**图表驱动、多维参数扫频扎实、定量口径统一（如 1 位小数规范 25.4%）、少讲空泛架构哲学**。
4. **ASPLOS — 全栈软硬协同 × 真机/OS 内核实测 × 端到端系统故事**
   - **评估重心**：与另三会截然不同——周期精确仿真骤降至 **10.5%**、工艺节点仅 **15.8%**，取而代之的是**真机/集群实测（73.7%）与 Linux 内核/编译器/运行时实装（42.1%）**（如 *Pond*, *Autonomous NIC Offloads*, *Elastic Cuckoo*, *HFI*, *PF-LLM*）。
   - **叙事调性**：评估最长（中位 **2,638w**），因为必须同时交代微基准（microbenchmarks）、端到端应用吞吐/尾延迟（P50/P99）、系统代码改动量（LoC）与跨层交互异常；数字偏好干净整数（**77.7%**），Related Work 几乎一律后置（**97.0%**）且最忌流水账（句首引用率仅 **2.71%**）。

---

## 7. 批判性反思：顶会获奖论文也不可盲从（Award-Paper Flaw Audit）

遵循“**不要认为只要是顶会论文——哪怕是 Best Paper——就应该全盘学习**”的核心原则，精读直接抓出了 **7 篇 Best Paper** 在评估、修辞与结论中的明确瑕疵。Phase 2 生成规则必须把这些“名家坏习惯”拉入黑名单：

| 获奖论文（均获 Best Paper） | 真实优点（值得学） | 必须坚决剔除的写作瑕疵（逐字实证） |
|---|---|---|
| **DaDianNao** (MICRO 2014, `conf__micro__ChenLLZHWLCXST14`) | 方法论先验证 CUDA GPU 基线不注水；28nm 布局布线面积/功耗扎实。 | **① 6 位有效数字虚假精度**：p. 1/10 写 `"450.65x"`、`"150.31x"`、`"2595.23x"`；<br>**② 尺度不对等宣称**：结论直接拿 64 芯片集群对比单 GPU 喊 `"up to 450.65x"`，未并列单节点/等面积收益。 |
| **Darwin** (ASPLOS 2018, `conf__asplos__TurakhiaBD18`) | Fig. 13 先抑后扬（`2.1× slowdown → 380× → 61×`）的瀑布归因堪称教科书。 | **432 词冗长煽情结论**：p. 13 出现新闻稿式比喻 `"provide the rocket fuel for comparative genomics"`，严重偏离顶会学术克制。 |
| **SIGMA** (HPCA 2020, `conf__hpca__QinSKNS0KK20`) | 坦承两个 GEMM 输给 Eyeriss v2 并给出驻留操作数归因；Table III 清晰对比。 | **排版与符号失控**：p. 12 相邻三段混用 `2x` / `6×` / `3X`；表题出现低级拼写错 `"Table III: Qualitative Comparision"` 及 `"Flexibile"`。 |
| **Contiguitas** (ISCA 2023, `conf__isca__ZhaoXWSYMWRST023`) | Meta 生产数据 + `Linux-Sim` vs `Linux-Real` 误差校准 + `Very High` 最坏压测。 | **口语化与陈词滥调渗入**：p. 10 用非正式过渡 `"Diving deeper, we find..."`；p. 12 结论首句用空泛套话 `"a holistic solution"`。 |
| **Constable** (ISCA 2024, `conf__isca__BeraRRMNGOKSSM24`) | 基线公平性满分（扫优 RFP 参数、测 CVP-1 冠军 EVES + 组合增益 + 3400 trace 校验）。 | **① 过度模板化复读（SAFARI 流水线感）**：p. 11–12 短短两页反复套用 `"We make [two/three] key observations... Based on these results, we conclude that..."` 超 6 次，机械感极强；<br>**② 校对疏漏与空泛尾句**：p. 12 出现 `"and and hence"` 重复词；p. 13 结尾滑向套话 `"inspire future works to explore a multitude of other optimizations"`。 |
| **LLM.265** (MICRO 2025, `conf__micro__XuW0CLZW25`) | 硬件编码架构扎实，跨仿真器 Astra-SIM 验证通信影响。 | **明显 2025 年 AI 润色痕迹 + 语法硬伤**：p. 11 堆砌 `"Remarkably, ... showcasing its reusability and efficiency"`、`"seamlessly"`、`"superior area and power efficiency"`；p. 13 脚注出现语法错误 `"are been verified"`。 |
| **PF-LLM** (ASPLOS 2026, `conf__asplos__XuSLBWLX026`) | 软硬协同思路新颖，p. 13 `7.4 Limitations` 诚实承认 JIT 与离线剖析短板。 | **最典型的“硬核工作被 AI 润色腔毁掉语感”案例**：p. 12 出现 AI 经典黑话 `"we delve into the rationale... within the broader landscape"`、`"remarkably well"`、`"intricate/delicate state"`、`"cohesively"`；p. 13 结论喊 `"This work pioneers..."`；p. 10 甚至出现计数与语法双错：`"three of the mostly widely-used open-source web applications: Apache..., MySQL..., RocksDB... and Xapian..."`（写了 `three` 却列了 **4** 个，`most` 误拼 `mostly`！）。 |

> **核心启示**：2024–2026 年的 Best Paper 依然凭借**硬核体系结构创新、严谨公平基线和实打实的工程深度**夺奖，但它们的**英文润色已经不同程度沾染了 LLM 腔调和校对滑坡**。如果写作工具盲目从 2025–2026 论文语料里模仿修辞，就会把 `delve / remarkably / seamlessly / pioneers / holistic` 当成“获奖秘诀”学进去——这正是本项研究坚持**跨 15 年纵向对照 + 批判性剥离**的最大价值。

---

## 8. 面向 Phase 2 英文写作 Skill 提炼的硬规则清单（Actionable Hard Rules）

以下 **26 条可执行硬规则**可直接转译为 Phase 2 英文学术写作 Skill 的约束与自动质检清单（按 `E` 评估 / `R` 相关工作 / `C` 讨论与结论 / `V` 顶会适配四组编号）：

### A. Evaluation Methodology & Quantitative Rhetoric（`E1–E12`）
- **`E1` [Methodology 篇幅与表文分工]**：将 Methodology 控制在 **450–900 词（0.5–1.0 页）**（大型系统实证/芯片流片可放宽至 1.5 页）。所有静态硬件参数统一放入 `Configuration Table`，正文严禁重复朗读表内数字，只解释建模 rationale、误差校准与简化假设。
- **`E2` [反稻草人基线铁律]**：评估强竞品时，必须显式说明如何保证公平（例如使用竞品开源最优实现、在同等面积/存储预算下扫描其最佳超参、或验证自写基线性能与已发表文献一致）；若架构正交，额外评估 `Baseline + Ours` 组合收益。
- **`E3` [诚实交代基准子集与简化]**：若从标准套件（SPEC/PARSEC/GAP/PrIM 等）中剔除任意子项，必须明确给出技术原因（如编译/仿真器不兼容、无内存瓶颈）；若仿真器存在理想化模块（如单周期内存分配、忽略随机逻辑面积），用显眼句式直接声明。
- **`E4` [五段式评估推进]**：评估章节默认遵循 `End-to-End Headline → Mechanism Attribution / Ablation → Sensitivity & Scalability Sweeps → Area/Power/Overhead Cost → Case Study / Outlier / Stress Test`；严禁把所有图按字母序或实验流水账罗列。
- **`E5` [因果消融硬要求]**：凡正文提出 ≥2 项核心技术组件，评估中必须给出**增量消融（Additive Ablation）或组件分解的精确数值**（如 `1.00× → 1.47× → 1.69× → 1.79×`），严禁仅用 `paramount / significant / substantial` 做无数字消融。
- **`E6` [趋势综合禁念柱子]**：解读多基准柱状图时，禁止按基准名逐一报数（*"The first application is A... The second is B..."*）。必须按**底层微架构指标**（如 MPKI、WMPKI、MLP、重用距离、内存占用、尾延迟敏感度）把负载分成 2–3 个特征区间（Regimes）进行趋势综合与因果解释。
- **`E7` [强制负面/异常/代价披露]**：每篇评估必须包含至少 **2–3 处实质性负面、退化、零收益或反常案例的微架构归因**（解释为何慢了、为何收益低、是否在噪声内、最坏情况界限是多少）。严禁图中有输/平的样本而正文宣称 *"consistently achieves superior performance"*。
- **`E8` [均值口径零容错]**：归一化加速比/相对性能一律用 **Geomean**；多道吞吐明确区分 **Weighted Speedup** 与 **Harmonic Mean**；算术平均仅用于可加绝对物理量。禁止对比率做算术平均，禁止只报告绝对收益而不标明统计口径。
- **`E9` [`up to` 必须成对绑定]**：正文或摘要中每出现一次 `up to Y` / `maximum speedup of Y`，必须在**同一句或紧邻前一句**先给出总体均值（*"X% on average (geomean), and up to Y% on [regime]"*）。禁止孤立展示单点峰值或跨节点规模不对等对比。
- **`E10` [精度克制与禁止虚假精度]**：常规仿真/系统百分比优先用 **整数或 1 位小数**（如 `18%`、`1.6%`），常规倍率用 **1–2 位小数**（如 `1.47×`、`43×`）。严禁对存在 ±3%–10% 建模误差的仿真结果或 4 天长跑时间输出 ≥4 位有效数字（如 `450.65×`、`0.43099 pJ`、`373829.28 s`、`170900.00%`）；仅极小错误率/面积占比（`<0.1%`）与高可靠度（`99.999%`）允许 3+ 位小数。
- **`E11` [符号统一与去重复]**：全文统一倍率符号（优先 `×`，禁止混用 `x` / `X` / `times`）及增减表达（避免 `"1.70× speedup"` 重复词或 `"reduces energy by 150×"` 歧义表述，改用 `"150× lower energy"` 或 `"99.3% energy reduction"`）。同一批数字最多在图、表、正文之一完整呈现，严禁三重复写。
- **`E12` [反模板化机械复读]**：评估小节总结句应随发现内容自然变化，禁止在连续 3 个以上小节反复拷贝完全相同的八股壳子（如连续多次 *"We make three key observations... Based on these results, we conclude that..."*）。

### B. Related Work（`R1–R5`）
- **`R1` [默认后置 + 紧缩预算]**：除非采用双层结构（Motivation 中只对比 2–3 个直系竞品）或紧贴 Evaluation 之前用于确立基线，**默认将 Related Work 置于 Evaluation 之后、Conclusion 之前**（顶会 exemplar 占比 96.3%），篇幅控制在 **450–650 词**。
- **`R2` [按设计轴而非按作者组织]**：每个 Related Work 子段必须以**机制类别、底层假设或设计权衡**作为主题句与小标题，严禁连续超过 2 句以 `Author et al. [X] proposed...` 开句写文献流水账（目标：句首直接引用/作者句占比 `< 5%`）。
- **`R3` [每组必落显式差异]**：每一主题分组的结尾必须用 1–2 句点明**本工作与该类方案的根本架构差异或正交互补性**；若涉及 ≥4 个多维竞品，配一张 4–6 列的定性机制对比表（且表内若有自身短板须诚实标出）。
- **`R4` [慷慨、精准、非对抗语气]**：先准确概括前人工作在其目标设定下的贡献，再用中性技术语言指出假设差异或适用边界；严禁使用 `"All prior works fail / suffer..."` 等一刀切贬损句式。
- **`R5` [避免空洞“首次”宣称]**：慎用 `"To the best of our knowledge, X is the first..."`；若确需界定首创性，必须限定到具体可验证的技术约束上。

### C. Discussion, Limitations & Conclusion（`C1–C5`）
- **`C1` [实质性 Limitations / Discussion]**：优先在评估后设简明 `Discussion` 或 `Limitations` 小节（150–350 词），直面 2–3 条最硬核的适用边界、未支持特性或部署权衡（如 JIT 限制、功耗建模缺口、硬件复杂度上限），绝不写无新信息的“空壳吹捧 Discussion”。
- **`C2` [Conclusion 单段紧凑硬约束]**：Conclusion 严格控制在 **1 个自然段、90–150 词（4–6 句）**；既拒绝 <50 词敷衍两句，也拒绝 >250 词的科普愿景与冗长未来工作清单。
- **`C3` [结论严禁复读摘要]**：Conclusion 与 Abstract 的 **3-gram 重合率必须控制在 <12%**。Abstract 负责“立题 + 预告方法与主数据”，Conclusion 负责“用过去时/完成时收束已验证的核心架构洞见、关键权衡与高层启示”（如 *"We presented..., demonstrated..., and showed that..."*）。
- **`C4` [绝对零 AI 浮夸尾句]**：严禁在 Evaluation、Discussion、Conclusion 中使用 LLM 高频套话与空洞宏大结尾——拉黑清单包括：`delve into`, `broader landscape`, `a testament to`, `formidable`, `seamlessly`, `remarkably`, `cohesively`, `holistic solution`, `pioneers`, `novel synergistic`, `presenting a promising avenue for future research`, `paves the way / advances the vision of democratized...`, `rocket fuel`。
- **`C5` [收尾校对硬关卡]**：投稿前对数字、计数、图例和连词做强制一致性核查（杜绝 *"three applications: A, B, C, and D"*、*"and and"*、*"are been"*、*"comapre"*、*"Comparision"*、*"Bit Fsuion"*、图轴跳号/重复等连 2024–2026 顶奖论文都踩过的低级事故）。

### D. Four-Venue Calibration Rules（`V1–V4`）
- **`V1` [投稿 ISCA 校准]**：强化**硅片可落地性**（RTL 综合/面积/关键路径延迟/工艺节点或 FPGA 原型）与**跨代架构洞察**，配置高诚实度的 `Discussion / Limitations` 探讨长期演进与真实系统边界。
- **`V2` [投稿 MICRO 校准]**：把 **Methodology（微架构细节 + CACTI/McPAT 面积功耗账）**与**周期级停顿/带宽/缓存冲突因果拆解**做到极致；同时严查 AI 修饰词与结论摘要重合度（MICRO 语料中该污染率最高）。
- **`V3` [投稿 HPCA 校准]**：确保**周期精确仿真或 GPU/加速器建模**口径严谨、**Geomean 与 1 位小数规范**高度统一，用紧凑方法论 + 高密度参数扫频与对比表格直击核心性能/能效收益，不堆冗余哲学讨论。
- **`V4` [投稿 ASPLOS 校准]**：以**真实机器/集群 + OS 内核/编译器/运行时实装**为核心证明载体（切勿仅靠纯仿真交差）；评估留足篇幅拆解**端到端吞吐、P50/P99 尾延迟、微基准诊断与工程改动量（LoC）**；百分比尽量用干脆整数，Related Work 坚决后置且杜绝流水账。

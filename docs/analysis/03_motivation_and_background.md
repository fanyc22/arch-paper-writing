# 维度三深度分析报告：背景铺垫、动机论证与问题框定（ISCA / MICRO / HPCA / ASPLOS, 2011–2026）

> **研究范围与方法论**：本报告基于体系结构四大顶会（ISCA、MICRO、HPCA、ASPLOS）2011–2026 年间 **152 篇 `macro_pool` 论文**的自动化量化剖析，以及其中 **34 篇论文**（20 篇获奖/高引 `exemplar` + 8 篇 2023 年前 `contrast_ordinary` 普通中稿论文 + 6 篇 2023–2026 年 `contrast_post2023` 后 LLM 时代中稿论文，严格排除 `held_out_test` 隔离集）的逐页原文精读。所有英文引文与页码均直接核自 `corpus/macro_cache/<paper_id>.json`（1-based 物理 PDF 页码），引用格式为 `(ShortName, VENUE YEAR, paper_id, p. X)`。
>
> **核心批判立场**：**不要认为只要是顶会论文——甚至 Best Paper——就值得照抄。** 本报告严格区分三类文本：（1）顶级的、克制且具必然性说服力的人类学术写作；（2）平庸的人类写作（教科书注水、缺乏实证图表的定性断言、重复自我摘要）；（3）后 2023 年涌现的 AI/模板化写作病灶（机械三局限清单、空洞营销词汇、在动机段提前推销设计并剧透结果）——同时对获奖论文中同样存在的不良写法点名示警。

---

## 1. 语料量化总览：背景与动机论证的 15 年结构性变迁

对 152 篇 `macro_pool` 论文和 48 篇 `deep_read` 论文（剔除 References 后的正文文本）进行脚本化统计（详见表 1），可以清晰看到体系结构论文在「背景与动机」维度上发生了三场剧烈迁移：

| 语料分组 | 样本量 (N) | 正文均字数 | 含显式 Observation / Takeaway / Insight 比例（篇均次数） | 含编号 Observation/Takeaway # 比例（篇均次数） | 含模板化 `"three limitations / challenges"` 比例 | `"However, existing/prior..."` 篇均次数 | 含 Oracle / Ideal / Headroom 实证上界研究比例 | AI 营销词密度（次/万词）\* |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| **全体 `macro_pool`** | 152 | 11,103 | 26.3% (0.80) | 9.9% (0.43) | 15.1% | 0.15 | 39.5% | 0.74 |
| **年代：2011–2015** | 47 | 9,984 | 12.8% (0.28) | 4.3% (0.11) | 14.9% | 0.11 | 23.4% | 0.28 |
| **年代：2016–2022** | 65 | 11,396 | 24.6% (0.75) | 9.2% (0.49) | 9.2% | 0.14 | 40.0% | 0.26 |
| **年代：2023–2026** | 40 | 11,943 | **45.0% (1.48)** | **17.5% (0.70)** | **25.0%** | **0.23** | **57.5%** | **2.07 (7.7×)** |
| 会议：ISCA | 38 | 11,188 | 28.9% (1.21) | 15.8% (0.68) | 23.7% | 0.08 | 34.2% | 0.45 |
| 会议：MICRO | 38 | 11,011 | 21.1% (0.63) | 7.9% (0.26) | 13.2% | 0.21 | 39.5% | 1.15 |
| 会议：HPCA | 38 | 11,243 | 31.6% (0.82) | 10.5% (0.47) | 10.5% | 0.24 | 36.8% | 0.62 |
| 会议：ASPLOS | 38 | 10,972 | 23.7% (0.53) | 5.3% (0.29) | 13.2% | 0.08 | 47.4% | 0.75 |
| **精读层级：`exemplar`** | 32 | 11,573 | 34.4% (1.56) | 21.9% (0.97) | 18.8% | **0.06** | 43.8% | **0.61** |
| **精读层级：`contrast_ordinary`** | 10 | 10,782 | 40.0% (1.50) | 10.0% (0.70) | 10.0% | 0.10 | 40.0% | **0.28** |
| **精读层级：`contrast_post2023`** | 6 | 11,672 | **50.0% (1.00)** | 16.7% (0.50) | 0.0%† | **0.50 (8.3×)** | 66.7% | **8.71 (14.3×)** |

> \* **AI 营销词（Promotional Lexemes）统计口径**：`intricate, paramount, linchpin, meticulously, pivotal, transcend(s/ing), seamlessly, delve(s/d/ing), holistic, synergistic, unleash(es/ing), multifaceted, revolutionize(d/ing), harmonize(ing)` 14 个典型 LLM 润色高频词。2011–2022 年整整 12 年间该指标稳定在 **0.26–0.28 次/万词**；2023 年后全语料暴涨至 **2.07 次/万词（7.7×–8.0×）**，在 `contrast_post2023` 组中更是高达 **8.71 次/万词**（单篇最高为 `Hestia`, MICRO 2024 的 **19.65 次/万词**，全篇 27 次！）。
> † `contrast_post2023` 组中 `"three limitations"` 正则命中为 0，是因为它们大量改用了显式项目符号 `"Challenge-1 / Challenge-2 / Challenge-3"`（如 `FastTTS`, ASPLOS 2026, p. 2）或 `"Firstly... Secondly... Thirdly..."`（如 `PICACHU`, ASPLOS 2025, p. 2），实质仍是机械三段式。

**表 1 揭示的三大宏观信号**：
1. **实证上界论证从「加分项」变为「硬门槛」**：含 Oracle / Ideal / Headroom 上界分析的论文占比从 2011–2015 年的 **23.4%** 一路攀升至 2023–2026 年的 **57.5%**（增幅 2.5×）。今天仅凭「现有方案不够好」的定性叙述已很难通过顶会 PC 审查。
2. **显式结论标签（Observation / Takeaway）爆发 3.5×**：含此类标签的论文从 **12.8%**（篇均 0.28 次）激增至 **45.0%**（篇均 1.48 次）。它在大型实证研究（如 `Pond`、`Constable`）中能提升可扫描性，但在平庸论文中正迅速沦为机械填空的格式装饰。
3. **模板化批评与空洞润色在 2023 年后急剧扩散**：`contrast_post2023` 的 `"However, existing/prior..."` 转折频率是 `exemplar` 论文的 **8.3 倍**（0.50 vs. 0.06），AI 营销词密度是 `exemplar` 的 **14.3 倍**、是 2023 年前普通人类论文的 **31.1 倍**。

---

## 2. 背景铺垫的边界控制：必要背景 vs. 教科书注水

顶会审稿人不是本科生，而是各子领域的一线研究者。背景章节（Section 2）的核心任务**不是科普该领域，而是为 Section 3（动机）与 Section 4（设计）建立最小充分的术语契约与物理约束**。逐页对比 34 篇精读论文，顶级作者与平庸作者在背景控制上呈现出截然不同的纪律。

### 2.1 顶级范例的四大背景裁剪技法

#### 技法一：极简术语契约（Minimal Domain Setup）
最优秀的背景章节往往短得惊人——只定义后文论证**直接依赖**的概念和基线假设，其余一律不讲。
* **`InvisiSpec`（MICRO 2018 最佳论文候选/高引范例）**：整节 `II. BACKGROUND AND TERMINOLOGY` 仅有 **281 词**（不到半栏，p. 2），仅精确定义四个核心术语（Out-of-order execution、Speculative execution、Unsafe speculative load、Memory consistency model），并点明 TSO 与 RC 下投机 load 的 squash 规则，随后立刻切入 `III. THREAT MODEL`（511 词，明确列出保护范围与 `"Out of scope"`，p. 3）。读者读完一页半便已精准进入安全边界，没有任何对乱序核或缓存层次的废话科普。
* **`DynamoLLM`（HPCA 2025 Best Paper）**：在 2025 年写 LLM 推理能耗管理，Section II `BACKGROUND` 严格压缩在 **1 栏之内**（p. 2），只界定后文调度算法直接调用的三个维度：prefill/decode 阶段差异、TTFT/TBT 指标定义、TP2/TP4/TP8 张量并行记号，绝不重复 Transformer 自注意力公式：
  > *"To evaluate the performance, we use: time to first token (TTFT), time between tokens (TBT), and throughput [50], [63]. TTFT is the latency of generating the first output token; while TBT is the latency to generate each new output token."* `(DynamoLLM, HPCA 2025, conf__hpca__StojkovicZGTC25, p. 2)`

#### 技法二：即时背景（Just-in-Time Background）
**不要把所有前置知识堆在 Section 2**。如果某个系统细节（例如 Linux 伙伴分配器、特定 DRAM 刷新电路）只在后文某一个小节的设计中才会用到，顶级作者会刻意把它从 Section 2 删掉，延迟到真正需要它的设计小节开头再引入。
* **`RMM`（ISCA 2015）**：Section 2 `Background` 仅用 **614 词**配合一张高度浓缩的 `Table 1` 对比表（p. 2–3）交代虚拟内存与大页机制；而对于其操作系统侧核心改动所依赖的 Linux 伙伴分配器（buddy allocator），作者没有在 Section 2 提前铺垫，而是延迟到第 6 页的 Section 5.2（`Eager paging`）前才用一段话即时引入：
  > *"Eager paging requires modest changes to Linux’s default buddy page allocator. Default buddy allocator. The buddy allocator splits physical memory in blocks of $2^{order}$ pages, and manages the blocks using separate free-lists per block size..."* `(RMM, ISCA 2015, conf__isca__KarakostasGACHM15, p. 6)`
* **`SALP`（ISCA 2012）**：尽管 DRAM 物理结构是冷门底层知识（Section 2 共 1,959 词），但每一段都严格为后文服务——从 logical bank 递进到 `2.3. Subarrays: Physical Organization of Banks`（p. 3–4），将 `local row-buffer`、`subarray row-decoder` 和 `global row-buffer` 三个物理事实直接锚定为后文 SALP-1 / SALP-2 / MASA 三级设计的改造靶点。字数虽长，但**零闲笔**。

#### 技法三：显式受众校准（Explicit Audience Calibration）
当论文跨领域（如把形式化验证引入体系结构会议 HPCA），读者确实不熟悉交叉领域背景。顶级作者会**坦诚声明背景深度上限**，只讲体系结构读者做设计决策所需的直觉，主动把纯理论留给引用文献。
* **`PVCoherence`（HPCA 2014）**：将参数化验证（Parametric Verification）引入缓存一致性协议设计，作者在 Section 2 开篇与核心理论处两次做显式受众校准：
  > *"Due to space constraints and our intended audience, we intentionally do not delve deeply into the theoretical foundations of PV."* `(PVCoherence, HPCA 2014, conf__hpca__ZhangBES14, p. 2)`
  > *"A rigorous explanation of the theory behind choosing the number of concrete nodes [8] is beyond the scope of this paper, but we provide the intuition here."* `(PVCoherence, HPCA 2014, conf__hpca__ZhangBES14, p. 4)`
  这种清醒的克制既建立了作者对交叉领域的权威感，又避免了把 HPCA 论文写成 CAV 形式化方法教材。

#### 技法四：以「问题驱动标题」或「结构化表格」取代泛泛背景
顶级作者甚至敢于**取消名为 "Background" 的章节**，直接把必要背景编织进问题诊断中：
* **`HFI`（ASPLOS 2023）**：根本不设 "Background" 标题，直接将 Section 2 命名为 `2 LIMITATIONS OF SFI`（p. 2）。一开头直接跳过页表隔离科普（*"The limitations of modern page-based protection architectures for fine-grain isolation are well known [54]."*，`(HFI, ASPLOS 2023, conf__asplos__NarayanGTRM0FVL23, p. 2)`），直奔 WebAssembly SFI 的硬物理天花板——用一行算术推导出 48-bit 虚拟地址空间内 8 GiB 沙箱的上限：
  > *"assume the best case — that each Wasm instance only consumes 8 GiB — then we can run at most 16K ($2^{14}$) Wasm instances concurrently. In FaaS platforms, that spin up a new sandbox in 10s of $\mu$-seconds [20] for every incoming network request, 16K instances is not a large number..."* `(HFI, ASPLOS 2023, conf__asplos__NarayanGTRM0FVL23, p. 3)`
* **`Swarm`（MICRO 2015 Best Paper）**：直接将章节顺序倒置——先写 `2 MOTIVATION`（851 词，用 Pintool 证明有序不规则算法蕴含 158×–3440× 并行度），再写 `3 BACKGROUND ON HW SUPPORT FOR SPECULATIVE PARALLELISM`（606 词），而且该背景节不是泛泛科普 TLS，而是直接用量化数据诊断理想 TLS 为何在 `sssp` 上只能拿到 **1.1×** 并行度（p. 3–4）。背景节因此变成了**进攻性的诊断章节**。

### 2.2 反面教材：教科书注水的两张面孔（平庸人类 vs. 后 2023 AI 润色）

背景注水在 2023 年前和 2023 年后呈现两种不同形态，但本质相同：**把审稿人早已知晓的本科/领域常识占用 1.5–2 页黄金篇幅反复复述**。

1. **传统平庸人类论文的「历史科普与自我复述病」**：
   * **`AVA`（HPCA 2022, `contrast_ordinary`）**：Section 2 `BACKGROUND AND MOTIVATION` 长达 **1,725 词**（p. 2–3），竟在 2022 年的 HPCA 上从历史科普讲起，逐一列举 Intel x86 的 MMX、SSE、AVX、AVX2、MIPS MSA、ARM NEON、NEC 与 Seymour Cray 的经典向量机（*"Common examples for Multimedia extensions include Intel x86’s MMX, SSE, AVX, AVX2... While classical vector extensions for NEC [14] and CRAY [38] are well-known..."*，`(AVA, HPCA 2022, conf__hpca__LazoRMBVSCUC22, p. 2–3)`），全节竟**没有一张实证动机图**来证明向量长度自适应的收益。
   * **`PREMA`（HPCA 2020, `contrast_ordinary`）**：Section 2 `BACKGROUND` 高达 **2,011 词**（p. 2–3），在 2020 年（TPU 论文发表 3 年后、CNN 加速器满天飞的时代）还在教科书式科普神经网络分为 CNN 和 RNN、包含 CONV/ACTV/POOL/FC 层、权重在推理时静态固定，并花整页复述 Google TPU 的 128×128 脉动阵列如何工作：
     > *"deployed DNNs can broadly be categorized as convolutional and recurrent neural networks (CNNs and RNNs). Both of these are designed by combining multiple layers, the most notable ones being the convolutional (CONV), activation (ACTV), pooling (POOL), fully-connected (FC)..."* `(PREMA, HPCA 2020, conf__hpca__ChoiR20, p. 2)`
     而在耗费 2,000 词科普之后，全文甚至**没有给出多任务 NPU 调度中任务饥饿/SLA 违约的实证动机曲线**就直接切入 Methodology（Section 3）。
   * **`CHOPIM`（ISCA 2020, `contrast_ordinary`）**：在 2020 年的 ISCA 上依然在 Section 2（1,211 词，p. 3）从头科普 DRAM 地址由 channel、rank、bank、row、column 组成，以及什么是 bank conflict（*"another row is already open, it must be closed before the target row is opened, which is called bank conflict and increases access latency"*，`(CHOPIM, ISCA 2020, conf__isca__ChoKLE20, p. 3)`）。
   * **`Alvarez15`（ISCA 2015, `contrast_ordinary`）**：Section 2 `Background and Motivation` 耗费 **2,037 词**（p. 2–4）大段复述作者自己前作的软件托管 SPM 编程模型和 `dma-get`/`dma-put`/`dma-synch` API，却对本篇要解决的「SPM 与全局内存地址别名（aliasing）频率」未做任何一条实测统计。

2. **后 2023 论文的「AI 百科式空话科普」**：
   * **`M-ANT`（HPCA 2025, `contrast_post2023`）**：在 2025 年的 HPCA Section II-A（p. 2）居然完整抄写 Vaswani 2017 年的 Multi-Head Attention 三行教材公式（$\text{Attention}(Q,K,V)=\text{softmax}(QK^T/\sqrt{d_k})V$），并解释 softmax 是对 key 做归一化、LLM 推理分 prefill 和 decode 阶段，甚至在 II-B 将最基础的均匀量化公式 $W' = \lfloor W/s \rceil, \hat{W} = s \times W'$ 单独编号为 Equation (1)（p. 3）。
   * **`PICACHU`（ASPLOS 2025, `contrast_post2023`）**：Section 2.1 和 2.3（p. 3–4）充斥着典型的大模型百科式抒情科普——既告诉 ASPLOS 审稿人「激活函数引入非线性」，又赞美「脉动阵列彻底革新了深度学习计算效率、数据富有韵律地流过阵列」：
     > *"Nonlinear functions in activation layers introduce essential nonlinearity, enabling models to capture intricate relationships that exceed the limitations of linear mappings."* `(PICACHU, ASPLOS 2025, conf__asplos__QinXT0Z25, p. 3)`
     > *"DNN accelerators based on systolic array architecture have revolutionized the efficiency of deep learning computations by optimizing the execution of matrix operations, which are central to neural networks... Data flows rhythmically through the array..."* `(PICACHU, ASPLOS 2025, conf__asplos__QinXT0Z25, p. 4)`
   * **对比正面样板 `Eyeriss`（ISCA 2016）**：同样写 CNN 背景（Section III，1,256 词），`Eyeriss` 写于 2016 年（DNN 加速器刚兴起），且其 Section III 不是泛泛科普「CNN 能提取特征」，而是精准形式化 7 维循环参数表（Table I）与三级存储能效比（DRAM vs. Global Buffer vs. RF），为 Section IV 的数据流分类法与 Section V 的 Row Stationary 优化提供直接的数学输入。**可见「是否注水」取决于两重检验：① 该知识在投稿年份是否已是顶会常识（15 年基准线漂移）；② 背景中的每一条定义是否都在后文动机/设计中被精确引用。**

---

## 3. 实证动机论证与「必然性」建构（Empirical Motivation & Inevitability Building）

体系结构顶会最顶级的 Section 2/3，读完后会给审稿人一种**「不可避免感（Inevitability）」**——不是「作者想出了一个巧妙点子，于是找个问题套上去」，而是「系统数据的层层剥离把所有其他路径都堵死了，唯独作者的方向是物理与架构约束下的唯一自然出口」。精读 20 篇 `exemplar` 论文，可提炼出五种杀伤力最强的实证动机建构模式。

### 3.1 顶级范例的五种实证动机范式

#### 范式一：理想上界（Oracle/Ideal Headroom）+ 多层根因下钻
先用理想实验量化「天花板有多大」（回答 *Why care?*），再用受控拆解逐层追问「瓶颈到底在哪」（回答 *Why do existing solutions miss it?*）。
* **`Whisper`（MICRO 2022 Best Paper）**：在 Section II（2,266 词，p. 2–5，配 7 张递进式实证图）完成教科书级下钻链条：
  1. **理想上界**：Ideal branch predictor 在 64KB TAGE-SC-L 上带来平均 **12.4% IPC** 提升（1.3%–26.4%，p. 3）；
  2. **第一层根因**：**76.4%** 的数据中心分支预测失误源于容量问题（capacity misses，p. 4）；
  3. **排除现有 profile 方案**：评估 4b/8b-ROMBF 与 8KB/32KB/Unlimited-BranchNet，仅减少 **3.4%–8.9%** 失误（Fig. 4, p. 4）；
  4. **深层分布差异**：对比 SPEC 与数据中心分支分布 CDF，证明数据中心难以预测的分支极其分散，打破 BranchNet「仅少量极难分支」的核心假设；
  5. **机制锚点**：量化历史长度（最高需 1024-bit）与布尔逻辑操作符（AND/OR/XOR）覆盖率（Fig. 7, p. 5），自然引出 Whisper 的离线布尔公式挖掘。
* **`Constable`（ISCA 2024 Best Paper）**：在 Section 3–4（2,544 词，p. 3–5）构建四级漏斗：
  1. 量化现象：**34.2%** 的动态 load 是 global-stable（且在 Client/Enterprise/Server 上高于 SPEC 2017，p. 3–4）；
  2. 剖析寻址模式（20% PC-relative、42.6% stack-relative、37.4% register-indirect，p. 4）；
  3. 量化性能瓶颈归因（load-port 争用等）与上界对比：**Ideal Constable 获得 9.1% 平均加速**，远高于仅消除数据依赖的 **Ideal Stable LVP（4.3%）**（Fig. 7, p. 5）——直接证明「同时消除数据依赖与微架构资源争用（load execution elimination）」比传统值预测（LVP）有 **2.1×** 的理论红利！
* **`Swarm`（MICRO 2015 Best Paper）**：用自研 Pintool 测出 6 个有序不规则算法在无边界核下的真依赖并行度高达 **158×–3440×**（在 1K 窗口下仍达 62×–827×，p. 3），紧接着在 Section 3 测出哪怕是**零开销、零通信延迟的理想 TLS（Max TLS parallelism）** 在 `bfs`/`sssp`/`astar`/`des` 上也只有 **1.03×–1.15×**（p. 3–4）——形成 **3440× vs. 1.03×** 的震撼反差，把「为何必须硬件支持无序投机任务队列而非循环级 TLS」论证得无懈可击。

#### 范式二：生产级大规模遥测 + 戳破「行业常识迷思」（Debunking Folk Wisdom）
在系统/数据中心方向（ISCA/ASPLOS），最令人信服的动机不是在模拟器的 10 个 benchmark 上跑数字，而是用生产集群遥测揭示一个**反直觉的根因**，直接推翻学界习以为常的假设。
* **`Contiguitas`（ISCA 2023 Best Paper）**：基于 Meta 生产机群数据（Section 2, 2,359 词，p. 3–5），构建了极具说服力的证据链：
  * 硬件趋势剪刀差：4 代服务器 DRAM 容量暴涨而 TLB 覆盖持平，导致页表遍历消耗高达约 20% 周期；
  * 碎片化严峻程度：**23%** 的生产服务器连**单个 2 MB** 连续物理页都分配不出，32 MB 更是高达 **59%**（p. 4）；
  * **核心一击——用统计数据粉碎「重启即可解决碎片化」的行业迷思**：
    > *"It is commonly assumed that memory fragmentation is correlated with server up-time [78, 114]... Our analysis showed there is little to no correlation between memory contiguity availability and server uptime, with the Pearson correlation coefficient between server uptime and the number of free 2 MB pages being only 0.00286."* `(Contiguitas, ISCA 2023, conf__isca__ZhaoXWSYMWRST023, p. 4–5)`
  * **根因锁定**：虽然全机不可迁移的 4 KB 页中位数仅占 **7.6%**，但它们像沙子一样散布在物理内存中，导致高达 **34%** 的 2 MB 块沦为不可迁移，其中超过 **73%** 来自网络收发缓冲区（p. 5）。这直接锁定了后文 Contiguitas 对不可迁移页实施隔离管理的设计必然性。
* **`Pond`（ASPLOS 2023 Best Paper）**：横跨 Azure **100 个生产集群、75 天**遥测（p. 3–5）：量化 **3–27%** 内存搁浅（stranding，95 分位，极端达 36%）、高比例 untouched 内存，再叠加 **158 个代表性负载**在模拟 CXL 延迟（+182% / +222%）下的性能衰减 CDF（p. 4–5），一步步把「为何需要小规模 CXL 池 + ML 预测搁浅/未触及内存」的商业与技术必然性钉死。

#### 范式三：视觉化「理想 vs. 基线」对比与端到端瓶颈拆解
硬件微架构论文中，一张信息密度极高的时间轴或通信对比图，往往胜过三段抽象说理。
* **`SALP`（ISCA 2012）**：在 Section 3（仅 **743 词**，p. 5）通过 `Figure 7` 并排绘制 `Same-bank Timeline (Baseline)` 与 `Diff-bank Timeline ("Ideal")`，用带编号圆点 **`❶ Serialization`、`❷ Write Recovery`、`❸ Extra ACTs`** 直观标出同一 bank 内访问不同 subarray 损失的三大时间开销；紧接着在同一页的 `Figure 8` 直接对比 SALP-1、SALP-2、MASA 如何逐个吃掉 ❶、❷、❸ 三块气泡——动机与设计在视觉上严丝合缝。
* **`Graphicionado`（MICRO 2016）**：在 Section II-C（p. 3）用两张图击穿软件图计算框架（GraphMat）的低效本质：① 实际片外访存流量是理论最优通信量的 **20×–129×**（p. 3）；② 全部执行指令中，**不到 6%** 是在执行真正的用户自定义图计算（`Process_Edge`/`Reduce`/`Apply`）（p. 3），其余 94% 都是软件框架开销与同步。
* **`SIGMA`（HPCA 2020）**：Section II（706 词）先在 V100 上量化 Transformer 与 GNMT 训练中 GEMM 占比约 **70%**（p. 3），再用 `cuSPARSE` 实测稀疏矩阵乘法效率暴跌；Section III（1,295 词）紧接着把一个具体稀疏矩阵映射到固定脉动阵列上（Fig. 4），直观暴露空间利用率崩塌与固定规约拓扑的死结。

#### 范式四：「反直觉负结果」驱动的消融动机
大多数平庸论文只敢报喜，而顶级作者敢在动机阶段通过受控消融主动报告**「什么机制不起作用」**，以此证明自己的架构裁剪不是拍脑袋，而是实证逼出来的。
* **`LLM.265`（MICRO 2025 Best Paper）**：探索用 H.265 视频编解码器压缩 LLM 张量，在 `Figure 2(b)`（p. 4）逐级开启 H.265 编码流水线模块（8 bit → 去对称性 -0.4b → 块划分与变换量化 -4.1b → 帧内预测 -0.6b → 混合精度 -0.3b 降至 2.6 bit），随后**明确标红一个失败阶段**（`+0.5 bit, Not Working!`）：
  > *"Inter-Frame Motion Prediction Does not Work. While the Inter-Frame prediction, including the motion prediction, achieves great efficiency in compressing videos, based on our experiments, it does not..."* `(LLM.265, MICRO 2025, conf__micro__XuW0CLZW25, p. 5)`
  这种诚实而锋利的负结果消融，瞬间说服审稿人为何必须砍掉 H.265 硬件面积最大的帧间运动估计模块，只保留并定制帧内与变换模块。

#### 范式五：提前击碎审稿人的「第一质疑」（Preempting the Reviewer's #1 Objection）
高水平作者在写动机时能精准预判审稿人最容易提出的反驳（「这事为什么不让编译器/OS/现成算法干？」），并在动机节直接拿一手证据把退路封死。
* **`Constable`（ISCA 2024 Best Paper）**：写「硬件消除稳定 load」，审稿人第一秒就会质疑「编译器做循环不变量外提（LICM）和常量传播不就行了吗？」。作者在 Section 3 专门放出 SPEC CPU 2017 `541.leela_r` 的真实源码与 GCC `-O3` 反汇编（Fig. 5(a)(b), p. 4–5），一行行展示 `mov rax, QWORD PTR [rip+0x1f4ac5]`（全局静态指针 `Random::s_rng`）因跨函数调用/别名分析保守性而无法被编译器静态消除，甚至在脚注 6 补刀：*"We also observe that merely increasing the number of x86-64 architectural registers from 16 to 32 has negligible impact on eliminating the global-stable loads at compile time"* `(Constable, ISCA 2024, conf__isca__BeraRRMNGOKSSM24, p. 4)`，一举彻底封死编译器质疑。

### 3.2 动机论证失灵的三种典型病灶

| 病灶类型 | 典型反面案例 | 具体表现与原文实证 | 审稿人视角下的致命伤 |
| :--- | :--- | :--- | :--- |
| **病灶 A：零实证定性拍脑袋（传统平庸人类）** | `Alvarez15` (ISCA 2015, `conf__isca__AlvarezVMCGMNAV15`, p. 4)<br>`AVA` (HPCA 2022, `conf__hpca__LazoRMBVSCUC22`, p. 2–3)<br>`PREMA` (HPCA 2020, `conf__hpca__ChoiR20`, p. 2–3) | `Alvarez15` 靠主观直觉断言无别名：*"it is unnatural to access the same data using strided and random accesses in the same computational parallel loop. This implies that SPM accesses almost never alias..."* `(Alvarez15, ISCA 2015, conf__isca__AlvarezVMCGMNAV15, p. 4)`，**零实测数据**；`AVA` 和 `PREMA` 写完 1,700–2,000 词背景，**零动机实验图**。 | 读者无法确认问题是真瓶颈还是伪命题，也看不到优化天花板有多大。 |
| **病灶 B：动机段空谈哲学 + 提前剧透评估数字（后 2023 甚至蔓延至获奖论文！）** | `PF-LLM` (ASPLOS 2026 **Best Paper**, `conf__asplos__XuSLBWLX026`, p. 4)<br>`PICACHU` (ASPLOS 2025, `conf__asplos__QinXT0Z25`, p. 5)<br>`Hestia` (MICRO 2024, `conf__micro__XuLZLW0024`, p. 4–5) | `PF-LLM` 的 Section 3 `Why an LLM is a Good Choice for Prefetching?`（664 词）**没有任何一张动机表或实证图**，通篇是四段定性抒情，还直接在动机节把后文 Evaluation 的结果提前贴出来自我背书：*"Our PF-LLM model achieves a remarkable 95% accuracy... delivers an average IPC improvement of 18.9%..."* `(PF-LLM, ASPLOS 2026, conf__asplos__XuSLBWLX026, p. 4)`；`PICACHU` 在 Section 3.2 `Figure 3b`（p. 5）竟直接把自己设计的 `PICACHU` 点画进了动机对比图！ | 逻辑倒果为因（用结论当动机）；动机节变成了导言的二次推销，失去问题发现的独立学术价值。 |
| **病灶 C：导言与动机段逐字自我抄袭（后 2023 常见仓促拼贴）** | `M-ANT` (HPCA 2025, `conf__hpca__HuZ00GH00GL25`, p. 2 vs. p. 4) | 第 2 页导言与第 4 页 Section III-B 居然将如下整段**一字不差地复制粘贴**：*"Clustering-based adaptive methods like GOBO [81] and Mokey [82] can sufficiently adapt to various distributions at the group level. However, they require codebooks for quantization and dequantization, leading to high adaptivity at the expense of encoding and computational efficiency."* `(M-ANT, HPCA 2025, conf__hpca__HuZ00GH00GL25, p. 2 & p. 4)`，甚至连 NF4 需 FP16 MAC 的例子也逐字照搬（p. 2 & p. 4）。 | 严重消耗读者耐心，暴露成稿仓促、结构分层失效（未能区分 Intro 的高阶概述与 Motivation 的证据展开）。 |

---

## 4. 前人工作与 Strawman 批评的修辞尺度

如何评价竞争方案（prior work）与朴素基线（strawman），最能区分资深一线学者与初级作者/AI 润色文本。

### 4.1 顶级学者的批评准则：架构权衡隔离 + 公平承认边界
从 `exemplar` 论文的精读中，顶级学者批评前人工作有三条铁律：

1. **隔离根本架构权衡（Trade-off Isolation），而非罗列表面缺点**：
   * **`Eyeriss`（ISCA 2016）**：Section IV `EXISTING CNN DATAFLOWS`（762 词，p. 4–5）没有居高临下地说前人「差」，而是先建立中立、对称的四类数据流分类法（WS / OS 三变体 / NLR），并用 `Table III` 与 `Figure 3` 客观拆解每种数据流在 RF 复用、片上互联复用、psum 累加上的取舍——让读者自己看出：现有数据流都是**局部单维优化**，没有一种能同时最小化全部三种数据搬运能耗。
   * **`InvisiSpec`（MICRO 2018）**：评估最直接的朴素防御（Fence-based）时，先直接量化其真实代价（*"Under TSO, using fences to defend against Spectre attacks slows down execution by 74% relative to a conventional, insecure processor; InvisiSpec reduces the execution slowdown to only 21%."*，`(InvisiSpec, MICRO 2018, conf__micro__YanCS0FT18, p. 2)`），将讨论锚定在可验证的性能成本上，绝不扣「naive / impractical」的空帽子。
   * **`RMM`（ISCA 2015）**：`Table 1`（p. 2）用 6 个精确客观的技术属性列（应用透明性、是否支持多段、大小对齐限制等）把大页、Direct Segments 与 RMM 排成对照表，文字仅用一句克制总结：*"Direct segments are only suitable for big-memory workloads and require application changes."* `(RMM, ISCA 2015, conf__isca__KarakostasGACHM15, p. 3)`，客观、锋利、零情绪词。

2. **明确承认前人在其原始假设下的有效性，再展示新场景如何打破该假设**：
   * **`Whisper`（MICRO 2022 Best Paper）**：在批评神经分支预测器 `BranchNet` 时，不否认它在 SPEC 上的成功，而是实测指出：数据中心的难预测分支高度分散，导致 `BranchNet` 的硬件预算覆盖率暴跌（仅减少 3.4%–8.9% 失误），且离线训练时间高出几个数量级（p. 4–5）。
   * **`ρHammer`（MICRO 2025, `contrast_post2023` 中的正面局部）**：在论证单线程预取锤击优于多线程时，严谨引用前人并解释物理根因——DDR4 的 TRR 采样器要求严格的访问序，多线程在内存控制器队列中相互碰撞会打乱模式、触发额外刷新，加锁同步又会引入串行化开销（p. 9–10）。这种根因级机制分析，远比空喊「prior works fail」更有说服力。

3. **避免 Strawman 稻草人谬误：用「最强对手」而非「最弱靶子」证明天花板**：
   * `Constable`（ISCA 2024）在动机段对比的是 **Ideal Stable LVP**（理想值预测器）而非某个简陋旧版 LVP；`Swarm`（MICRO 2015）对比的是**零通信延迟的理想 TLS**；`Whisper`（MICRO 2022）的基线是 **64KB TAGE-SC-L** 加上 **Unlimited-BranchNet**（无限容量版！）。只有把「理想化的竞争范式」击败，新架构范式的必要性才真正成立。

### 4.2 反面教材：AI 模板化批评与空洞修辞的爆炸

对比 `exemplar` 与 `contrast_post2023`，表 1 已给出触目惊心的量化证据：`contrast_post2023` 的 `"However, existing/prior..."` 频率是 `exemplar` 的 **8.3 倍**（0.50 vs. 0.06），AI 营销词密度是 `exemplar` 的 **14.3 倍**（8.71 vs. 0.61）。逐页细读揭示了三种极易触发审稿人「AI 警报」的修辞病灶：

1. **「三局限 → 三挑战 → 三协同优化」的对称八股模板**：
   * **`PICACHU`（ASPLOS 2025, p. 2–3）**：第 2 页用 `"Firstly... Secondly... Thirdly..."` 列出三挑战，紧接着 `"Consequently, the nonlinear acceleration solutions proposed in prior works [49, 75, 136] face significant limitations... These distinct challenges call for a holistic approach..."`，第 3 页再对称用 `"First... Second... Third..."` 列出三机遇。
   * **`FastTTS`（ASPLOS 2026, `conf__asplos__ChenML0MLF26`, p. 2）**：尽管其实证测量本身扎实，但导言与动机架构严格套用对称三段式：`Challenge-1 / Challenge-2 / Challenge-3` → *"a serving system that integrates three synergistic optimizations"* → 贡献列表中再次重复 *"three novel and synergistic optimizations"* `(FastTTS, ASPLOS 2026, conf__asplos__ChenML0MLF26, p. 2)`，并夹杂 `"realizing democratized agentic AI"`、`"intelligently partitions"` 等明显带 LLM 润色腔的措辞。
2. **「宏大叙事 + 形容词通胀」的空洞开篇（零信息增量）**：
   * **`Hestia`（MICRO 2024, `contrast_post2023`, 营销词密度 19.65/万词）**：多个章节开篇连续出现毫无技术实质的 ChatGPT 经典句式：
     > *"In the intricate realm of HLS, where high-level descriptions evolve into complex hardware designs through a sequence of transformation passes, the need for a comprehensive debugging mechanism is paramount. The multi-level interpreter in Hestia transcends conventional debugging methods..."* `(Hestia, MICRO 2024, conf__micro__XuLZLW0024, p. 5)`
     > *"Serving as a linchpin, this interpreter empowers debugging at various levels."* `(Hestia, MICRO 2024, conf__micro__XuLZLW0024, p. 4)` / *"It empowers designers by providing the capacity to seamlessly switch..."* `(Hestia, MICRO 2024, conf__micro__XuLZLW0024, p. 6)`
   * **`QPlacer`（ISCA 2025, `contrast_post2023`, 营销词密度 8.90/万词）**：
     > *"In this study, we systematically investigate and address the multifaceted challenges... Recognizing the complexity of these issues, our solution pivots on a meticulously designed physical layout... This initiative marks a pivotal advancement in quantum chip design, harmonizing the delicate balance between component isolation and integration in sophisticated quantum systems."* `(QPlacer, ISCA 2025, conf__isca__Zhang0D0AO0B0025, p. 2)`
   * **诊断**：删掉上述整段文字，读者损失的技术信息量严格等于 **0**。在资深体系结构审稿人眼中，`"meticulously designed"`、`"pivotal advancement"`、`"intricate realm"`、`"transcends conventional"` 不仅不能提升说服力，反而会强烈暗示「底层技术含金量不足，需要靠华丽空话掩饰」。

### 4.3 范例 vs. 劣作：背景与批评段落逐字对照

| 对比维度 | 顶级范例写法（克制、精确、机制驱动） | 反面写法（注水、情绪化或 AI 模板化） | 差距本质 |
| :--- | :--- | :--- | :--- |
| **背景范围界定** | *"Due to space constraints and our intended audience, we intentionally do not delve deeply into the theoretical foundations of PV."* `(PVCoherence, HPCA 2014, conf__hpca__ZhangBES14, p. 2)` | *"DNN accelerators based on systolic array architecture have revolutionized the efficiency of deep learning computations... Data flows rhythmically through the array..."* `(PICACHU, ASPLOS 2025, conf__asplos__QinXT0Z25, p. 4)` | 前者尊重读者专业度、精准切割知识边界；后者用百科赞美体浪费版面。 |
| **前人方案批评** | *"Direct segments are only suitable for big-memory workloads and require application changes."* `(RMM, ISCA 2015, conf__isca__KarakostasGACHM15, p. 3)` | *"Consequently, the nonlinear acceleration solutions proposed in prior works [49, 75, 136] face significant limitations... These distinct challenges call for a holistic approach..."* `(PICACHU, ASPLOS 2025, conf__asplos__QinXT0Z25, p. 2)` | 前者一句指出适用边界与改造成本；后者全靠 `"significant limitations"` + `"holistic approach"` 空转。 |
| **反驳潜在质疑** | 放出 `541.leela_r` 的真实 GCC `-O3` 反汇编，指出 `mov rax, QWORD PTR [rip+0x1f4ac5]` 为何不能被编译器外提 `(Constable, ISCA 2024, conf__isca__BeraRRMNGOKSSM24, p. 4–5)` | *"although some data structures (e.g., arrays) can be accessed in different ways, it is unnatural to access the same data using strided and random accesses... This implies that SPM accesses almost never alias..."* `(Alvarez15, ISCA 2015, conf__isca__AlvarezVMCGMNAV15, p. 4)` | 前者用硬反例堵死退路；后者用 `"it is unnatural"` 蒙混过关。 |

---

## 5. 从动机到设计的平滑交接（Motivation-to-Design Handoff）

动机节的末尾与设计节的开篇之间，是一篇体系结构论文最容易「断层」或「泄底」的接缝处。做得太弱，读者不知道为什么突然冒出这几个硬件模块；做得太早，动机节还没写完就开始剧透具体电路与参数，导致后面 Design 节被迫重复叙述。

### 5.1 四种干净无泄漏的交接范式

1. **逻辑三段论桥接节（Pure Syllogism Bridge）——最高雅的无剧透交接**
   * **`Elastic Cuckoo`（ASPLOS 2020）**：在 2,173 词的 Background 之后、进入算法与硬件设计之前，专门设置一个仅 **298 词**的独立小节 `3 Rethinking Page Tables`（p. 4）。全文不含任何一句具体电路或 bit-width 剧透，全凭一气呵成的逻辑推演把所有前路逼到唯一出口：
     > *"As indicated in Section 2.1.1, radix page tables are not scalable. Further, as shown in Section 2.2.2, having a single global hashed page table is not a good solution either. We want to provide process-private hashed page tables... However, a default-sized hashed page table cannot be very large, lest we waste too much memory in some processes. Hence, we are forced to have modest-sized hashed page tables, which will suffer collisions. One promising approach to deal with collisions is to use cuckoo hashing (Section 2.3). Unfortunately, any default-sized cuckoo hash table will eventually suffer insertion failures due to insufficient capacity. Hence, it will be inevitable to resize the cuckoo hash table. Sadly, resizing cuckoo hash tables is especially expensive."* `(Elastic Cuckoo, ASPLOS 2020, conf__asplos__SkarlatosKXT20, p. 4)`
   * **效果**：六步递进（`However → Hence → One promising approach → Unfortunately → Hence → Sadly`），没有一个粗体框、没有一句吹捧、没有提前剧透 Section 4 的弹性哈希机制，却让读者迫不及待地翻向 Section 4 去找「怎么低开销扩容 cuckoo hash table」的答案。

2. **实证发现 → 设计目标契约（Empirical Observations → Concise Design Goals）**
   * **`Pond`（ASPLOS 2023, p. 4–5）**：在 100 集群遥测结尾用极简 `Summary and implications` 收束核心数字与两大挑战，紧接着在 Section 4 `POND DESIGN` 第一段将它们转化为五条高度凝练、可验证的 Design Goals（`G1 Performance comparable to NUMA-local DRAM`、`G2 Compatibility with virtualization accelerators` 等，p. 5），每条仅 5–8 词，清晰划定设计的验收契约而不剧透具体机制。

3. **问题-局限-对策对照矩阵（Requirement-Limitation-Approach Matrix）**
   * **`SIGMA`（HPCA 2020, `conf__hpca__QinSKNS0KK20`, p. 5–6）**：在 Section III 末尾用一张 `Table I`（*"Desired features for a GEMM accelerator, limitations of systolic arrays, and SIGMA’s approach"*，`(SIGMA, HPCA 2020, conf__hpca__QinSKNS0KK20, p. 5)`）做单表映射，正文仅用两句收束：*"Summary. Table I summarizes the sources of inefficiency in systolic arrays and how SIGMA addresses each. Architectural details are provided next."* `(SIGMA, HPCA 2020, conf__hpca__QinSKNS0KK20, p. 6)`——用表格做高阶路标，正文零剧透、零冗长复述。

4. **两行核心不变量作为衔接锚点（Core Invariant Bridge）**
   * **`Constable`（ISCA 2024 Best Paper, p. 5）**：在完成 Section 4（Performance Headroom）后，用极短的 Section 5 `Constable: Key Insight`（仅 **343 词**，p. 5–6）提炼出整个设计的两条必要充分条件（`Condition 1`: 源寄存器未被改写；`Condition 2`: 目标内存地址未被改写），把纯实证观察瞬间升华为数学化/架构化的设计不变量，再由 Section 6 逐一用硬件结构落实这两条条件。

### 5.2 两种必须规避的交接失败模式

1. **失败模式一：动机节前向泄漏（Premature Design Spoilers & Self-Pitching）**
   * **严重反例**：`PICACHU`（ASPLOS 2025, `conf__asplos__QinXT0Z25`, p. 5）在 Section 3.2 `Why CGRA?` 中直接写入 *"To support this, PICACHU enables adaptive approximation algorithms in Section 4.1... incorporates a precision-aware design, as discussed in Section 5.3.3"* `(PICACHU, ASPLOS 2025, conf__asplos__QinXT0Z25, p. 5)`，且在图 3(b) 中就把自家方案结果放进动机图；`PF-LLM`（ASPLOS 2026 Best Paper, `conf__asplos__XuSLBWLX026`, p. 4）在 Section 3 动机中直接抛出 `95% accuracy` 和 `18.9% IPC` 评估结果。
   * **轻微反例（获奖论文中的小瑕疵）**：`DynamoLLM`（HPCA 2025 Best Paper, p. 4–5）在 Section III 动机分析每小节末尾习惯性插入 `"In DynamoLLM, we will use historical data to set the number of pools..."`（p. 4）、`"In DynamoLLM, we will propose techniques to efficiently scale..."`（p. 5）——虽简短，但已轻微跨越「问题域 → 方案域」的边界，不如将其统一收束到设计总览首段。

2. **失败模式二：机械粗体 `Observation / Takeaway` 框的样板化泛滥**
   * 量化数据（表 1）显示，显式 `Observation / Takeaway / Insight` 标签从 2011–2015 年的 **12.8%** 飙升到 2023–2026 年的 **45.0%**（篇均 1.48 次）。
   * **什么时候有效？** 当单节包含 4 张以上独立遥测/剖析图表（如 `Pond`、`Contiguitas`、`Constable`），适度用 2–4 句高度凝练的实证结论帮读者定位重点，确实有益。
   * **什么时候变成灾难？** ① 在**没有定量图支撑**的定性段落后强行贴 `Takeaway 2 / Takeaway 3`（如 `M-ANT`, HPCA 2025：*"Takeaway 2. Enhancing the data-type-based adaptive method for group quantization is challenging and requires a careful balance for the computation and decoding efficiency."* `(M-ANT, HPCA 2025, conf__hpca__HuZ00GH00GL25, p. 4)` — 读完等于没说，纯属水话）；② 连续每个自然段都用同一句型收尾（即使是 **ISCA 2024 Best Paper `Constable`**，在 Section 3–4 也出现多处高频重复的 `"We make two/four key observations... The key takeaway is... We conclude that..."` 模板节奏，p. 3–5——在强数据支撑下尚可接受，但若被普通论文机械照搬，极易滑向八股文）。

---

## 6. 15 年演变趋势、获奖论文避坑警示与 Phase 2 硬性规则

### 6.1 2011–2026 年三大演变趋势总结
1. **背景节两极分化与「常识基准线」上移**：2011–2016 年（如 `SALP` 2012、`Eyeriss` 2016）还需花 1–1.5 页仔细界定 DRAM 子阵列或 CNN 卷积维度；进入 2023–2026 年，Transformer 注意力、prefill/decode、脉动阵列、DRAM bank/rank 已成绝对常识，优秀论文（如 `DynamoLLM` 2025、`HFI` 2023）将背景极限压缩到 0.5–1 栏，而落伍论文却仍在重抄 2017 年教材。
2. **「表征/遥测型动机（Characterization-Driven Motivation）」成为主流**：Oracle/Headroom 实验占比翻了 2.5 倍（23.4% → 57.5%），ISCA/ASPLOS 顶流论文（`Pond`、`Contiguitas`、`Whisper`、`Constable`）甚至把动机实证做成了可独立引用的领域测量贡献。
3. **2023 年后 AI 润色污染显著拉大文风鸿沟**：表 1 显示 AI 营销词密度在 2023 年出现断崖式跳升（0.26 → 2.07 /万词），`contrast_post2023` 更达 8.71 /万词。审稿人对此类语言已产生明显疲劳与反感。

### 6.2 批判性警示：哪怕在 Best Paper 中也**不要照抄**的写法
践行「不要认为只要是获奖论文就应该学习」，以下三处来自 Best Paper 的真实缺陷必须在 Phase 2 写作规则中列为禁区：
1. **`PF-LLM`（ASPLOS 2026 Best Paper, `conf__asplos__XuSLBWLX026`, p. 4）的零实证动机节与结果剧透**：Section 3 `Why an LLM is a Good Choice for Prefetching?` 全节 664 词竟无任何实验数据或定量对比图，仅凭四段定性推演+提前贴出 `95% accuracy` / `18.9% IPC` 评估结果来充当动机（甚至同期还留有 `"LMHint Prefetcher prefetcher"` 的笔误，p. 4 & p. 7）。它获奖是因为「用离线 LLM 为硬件预取器生成指令级静态提示」的跨界思路新颖且实验扎实，**绝不是因为其 Section 3 写得好**；普通选题若效仿这种「定性宣言替代实证动机」，必死于审稿。
2. **`Constable`（ISCA 2024 Best Paper, `conf__isca__BeraRRMNGOKSSM24`, p. 3–5）的偏高密度套路化小结句式**：SAFARI 组风格偏好在每张图后固定输出 `"We make X key observations... The key takeaway is..."`（全篇出现 11 次 `obs_any`）。其背后有极扎实的硬数据和汇编反例兜底，故未显空洞；但普通作者若无同等密度的新发现而盲目套用，会立刻呈现出机械模板感。
3. **`DynamoLLM`（HPCA 2025 Best Paper, `conf__hpca__StojkovicZGTC25`, p. 4–5）在动机节反复前向剧透**：多次在问题分析中途插入 `"In DynamoLLM, we will..."`，略微打断了「先把问题讲透，再揭晓方案」的叙事张力。

### 6.3 面向 Phase 2 写作规范的硬性规则（Actionable Rules）

| 编号 | 规则名称 | 硬性可执行标准（Do / Don't） | 核心标杆范例 |
| :---: | :--- | :--- | :--- |
| **R3.1** | **背景「零闲笔」审计** | Background 节中出现的每一个概念、公式或硬件结构，**必须**在后文 Motivation 或 Design 中被显式调用；凡未被调用的教科书科普（如 2025 年重写 Self-Attention 公式、脉动阵列工作原理、DRAM bank/rank 定义）**一律删除**。建议将纯 Background 控制在 **300–900 词（0.5–1.2 页）**内，除非是交叉领域新物理机制（此时须作显式受众校准）。 | `InvisiSpec` (281w), `RMM` (614w), `DynamoLLM` (<1 col), `PVCoherence` (受众校准) |
| **R3.2** | **即时背景（Just-in-Time）延迟原则** | 仅服务于单一设计子模块的底层细节（如 Linux 伙伴分配器、特定页表位布局、特定硬件计数器），**禁止**堆砌在 Section 2，须延迟至对应设计小节前用 1 段话即时引入。 | `RMM` (§5.2 buddy allocator), `Swarm` (Motivation before Background) |
| **R3.3** | **实证动机「三件套」门槛** | 除非纯理论/形式化安全证明，Motivation 节**必须**至少包含以下两项定量证据：（1）瓶颈拆解或分布特征图；（2）**理想上界/Oracle Headroom 实验**（或理想化的竞争范式对比）；（3）针对审稿人第一质疑（如「为何编译器/OS/现成算法不行」）的受控实证或代码/反汇编反例。严禁纯定性断言（`"it is unnatural"`）充当动机。 | `Whisper`, `Constable`, `Swarm`, `Contiguitas`, `Pond`, `Graphicionado` |
| **R3.4** | **允许并鼓励「负结果」动机消融** | 当设计刻意舍弃某类看似自然的机制（如视频编解码中的帧间预测、缓存中的写回追踪）时，应在 Motivation 中直接展示其失效的定量证据，把「克制的减法」变成设计必然性的核心论据。 | `LLM.265` (Fig. 2b 标红 `+0.5 bit Not Working!`) |
| **R3.5** | **零模板、零营销词的前人工作批评** | 批评前人工作时必须**隔离具体架构权衡**（最好压缩进一张客观属性对照表），并公平承认其在原假设下的适用性；**严禁**使用 `"However, existing works suffer from three critical limitations"` 机械三段式，以及 `intricate / paramount / linchpin / meticulously / pivotal / transcends / seamlessly / holistic / synergistic / unleash / multifaceted` 等 AI 营销空词（目标密度：**0 次/万词**）。 | `Eyeriss` (Table III), `RMM` (Table 1), `Whisper`, `InvisiSpec` |
| **R3.6** | **动机-设计「清洁交接」原则** | Motivation 节**禁止**提前塞入自家系统的 Evaluation 加速比/准确率数字（留给 Intro 和 Evaluation），也**禁止**把自家方案结果画进动机图；改用「逻辑三段论桥接短节」（250–400 词）、「极简 Design Goals 契约」或「需求-局限-思路单表映射」完成交接。`Observation / Takeaway` 显式标签全节最多 **2–4 条**，且每条必须含具体量化数字或反直觉机制结论，严禁输出空洞的「需要仔细权衡（requires a careful balance）」类水话。 | `Elastic Cuckoo` (§3 298w 逻辑桥), `SIGMA` (Table I), `Pond` (G1–G5), `Constable` (§5 两条不变量) |
| **R3.7** | **严禁 Intro→Motivation 逐字复制** | Introduction 给出问题轮廓与核心数字，Motivation 给出证据链、实验设置与根因诊断；两节之间**不得出现连续两句以上的逐字复写**。 | 反例警钟：`M-ANT` (p. 2 vs. p. 4 整段抄袭) |

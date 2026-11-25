# 维度二分析报告：标题、摘要与引言“黄金前两页”写作工艺（ISCA / MICRO / HPCA / ASPLOS, 2011–2026）

> **实证基础说明**：本报告基于 `corpus/manifest.json` 与 `corpus/macro_cache/` 中 **152 篇 `macro_pool` 论文**的定量统计（标题全量 N=152，干净摘要 N=148，干净引言 N=145；严守零接触 `held_out_test`）以及对 **35+ 篇 `deep_read` 论文**（覆盖全部 4 会议、3 时代、`exemplar` / `contrast_ordinary` / `contrast_post2023` 三层级）的逐句精读与人工复核。所有英文引文、字数、句数与页码均直接核验自 `corpus/macro_cache/<paper_id>.json`。

---

## 1. 标题工艺（Title Craft：152 篇定量扫描 + 48 篇定性审计）

### 1.1 标题句型分类、词长分布与 15 年演变

**表 1：全语料（N=152）标题结构类型、长度与修饰词密度分布**

| 维度分组 | 样本数 | 词数中位（均值 / 区间） | 含冒号比例 | `Name: Subtitle` | `Phrase/Action: Subtitle` | 无冒号描述型 | `A Case for...` / 问句 | 连字符复合词均值 | 含高频宣传形容词比例 |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| **ALL (N=152)** | 152 | **9.0** (9.0 / 2–14) | **66.4%** (101) | **55.3%** (84) | 11.2% (17) | 32.9% (50) | 0.7% (1) / **0%** | 0.70 | 30.3% (46) |
| **2011–2015** | 47 | **8.0** (8.2 / 2–14) | **55.3%** (26) | 44.7% (21) | 10.6% (5) | **42.6%** (20) | 2.1% (1) / 0% | **0.55** | 36.2% (17) |
| **2016–2022** | 65 | **9.0** (9.2 / 2–14) | **64.6%** (42) | 52.3% (34) | 12.3% (8) | 35.4% (23) | 0% / 0% | 0.69 | **20.0%** (13) |
| **2023–2026** | 40 | **9.0** (9.4 / 4–14) | **82.5%** (33) | **72.5%** (29) | 10.0% (4) | **17.5%** (7) | 0% / 0% | **0.90** | **40.0%** (16) |
| **ISCA** | 38 | 9.0 (9.2 / 2–14) | 65.8% | 47.4% (18) | **18.4%** (7) | 31.6% (12) | 2.6% (1) | 0.76 | 31.6% |
| **MICRO** | 38 | 9.0 (8.7 / 3–14) | 68.4% | **63.2%** (24) | 5.3% (2) | 31.6% (12) | 0% | **0.97** | 28.9% |
| **HPCA** | 38 | 9.0 (9.3 / 6–13) | 63.2% | 52.6% (20) | 10.5% (4) | 36.8% (14) | 0% | 0.66 | 31.6% |
| **ASPLOS** | 38 | 9.0 (8.7 / 2–14) | 68.4% | 57.9% (22) | 10.5% (4) | 31.6% (12) | 0% | **0.42** | 28.9% |
| **`exemplar`** | 32 | 9.0 (9.4 / 2–14) | 78.1% (25) | 56.3% (18) | **21.9%** (7) | 18.8% (6) | 3.1% (1) | 0.62 | 28.1% |
| **`contrast_ordinary`** | 10 | 8.0 (8.9 / 7–13) | 70.0% (7) | 70.0% (7) | 0% | 30.0% (3) | 0% | 0.40 | 20.0% |
| **`contrast_post2023`** | 6 | 8.5 (9.0 / 8–12) | **100.0%** (6) | **100.0%** (6) | 0% | 0% | 0% | **1.17** | 33.3% |

#### 标题实证五大规律：
1. **词长黄金甜区为 6–10 词（占全语料 65.1%，99/152）**：完整词数分布为 `≤5 词` 14 篇（9.2%）、`6–10 词` 99 篇（65.1%，其中 8–10 词高达 77 篇）、`11–12 词` 26 篇（17.1%）、`13–14 词` 仅 13 篇（8.6%），没有任何一篇超过 14 词。
2. **冒号命名制全面统治（55.3% → 82.5%，2026 年 100%）**：`Name: Subtitle` 已成为现代体系结构论文的“品牌标配”，2011–2015 仍有 42.6% 的无冒号描述性标题，到 2023–2026 降至仅 17.5%。与此同时，**问句标题在 152 篇中为 0 篇**——与部分社科/AI 论文不同，体系结构顶会极度偏好陈述式、机制导向的肯定标题。
3. **获奖论文独爱“意象/动作短语 + 冒号”变体（21.9% vs 普通论文 0%）**：真正令人过目不忘的顶级标题往往不是生硬的缩写，而是自带叙事张力的动词短语或意象隐喻，如：
   - `"Flipping Bits in Memory Without Accessing Them: An Experimental Study of DRAM Disturbance Errors"` (`RowHammer`, ISCA 2014, `conf__isca__KimDKFLLWLM14`, p. 1)
   - `"Clearing the Clouds: A Study of Emerging Scale-out Workloads on Modern Hardware"` (`CloudSuite`, ASPLOS 2012, `conf__asplos__FerdmanAKVAJKPAF12`, p. 1)
   - `"Chasing Carbon: The Elusive Environmental Footprint of Computing"` (`Chasing Carbon`, HPCA 2021, `conf__hpca__GuptaKLTLW0W21`, p. 1)
   - `"Amdahl's Law in the Datacenter Era: A Market for Fair Processor Allocation"` (`Amdahl's Law`, HPCA 2018, `conf__hpca__ZahediLL18`, p. 1)
   - `"Elastic Cuckoo Page Tables: Rethinking Virtual Memory Translation for Parallelism"` (`Elastic Cuckoo`, ASPLOS 2020, `conf__asplos__SkarlatosKXT20`, p. 1)
4. **连字符复合修饰链与空洞形容词在 2023–2026 显著反弹**：全语料最高频的标题空洞修饰词前五位为 `Efficient` (16)、`Fast` (7)、`Scalable` (7)、`Secure` (5)、`Energy-Efficient` (4)。`2016–2022` 纯人类黄金期曾压低至 20.0%，但 `2023–2026` 反弹至 **40.0%**，且连字符复合词密度从 0.55 升至 **0.90**（`contrast_post2023` 达 **1.17**，MICRO 2023–2026 出现大量 3–4 连字符堆叠标题）。
5. **无冒号极简宗师体（2–4 词）仅属于开创性概念**：当概念本身极具辨识度时，极致克制反而最有力量——如 `"Vector Runahead"` (2w, ISCA 2021, `conf__isca__NaithaniA0E21`)、`"Autonomous NIC Offloads"` (3w, ASPLOS 2021, `conf__asplos__PismennyEYL0T21`)、`"DaDianNao: A Machine-Learning Supercomputer"` (4w, MICRO 2014, `conf__micro__ChenLLZHWLCXST14`)。

### 1.2 标题好坏对照与反模式解剖

| 类型 | 真实范例与来源 | 诊断评价 |
|---|---|---|
| **极简宗师型** | `Vector Runahead` (ISCA 2021, `conf__isca__NaithaniA0E21`) / `Autonomous NIC Offloads` (ASPLOS 2021, `conf__asplos__PismennyEYL0T21`) | 2–3 词直指机制本质，零废话、零形容词、极高记忆度。 |
| **锐利主张/反常识型** | `LLM.265: Video Codecs are Secretly Tensor Codecs` (MICRO 2025, `conf__micro__XuW0CLZW25`) | 8 词；巧妙嫁接 H.265 命名，副标题用一句反常识命题直接钩住审稿人好奇心。 |
| **干净系统名+机制副标题** | `InvisiSpec: Making Speculative Execution Invisible in the Cache Hierarchy` (MICRO 2018, `conf__micro__YanCS0FT18`) / `Pond: CXL-Based Memory Pooling Systems for Cloud Platforms` (ASPLOS 2023, `conf__asplos__LiBHEZNSRLAHFB23`) | 系统名可发音且贴合语义（InvisiSpec=隐形推测，Pond=小池），副标题精确交代“做什么 + 在哪层做”，零空洞宣传词。 |
| **反模式 A：强行首字母拼词（Forced Backronym）** | `PICACHU: Plug-In CGRA Handling Upcoming Nonlinear Operations in LLMs` (ASPLOS 2025, `contrast_post2023`, `conf__asplos__QinXT0Z25`, p. 1, 3) | 为硬凑宝可梦名字，正文 p. 3 竟展开为 `Plug-In Coarse-grAined-reConfigurable-accelerator Handling Upcoming`，从词中强抠大写字母 `A`、`C`，并用生硬的 `Handling Upcoming` 凑字，徒增廉价感。 |
| **反模式 B：连字符修饰词链堆砌** | `FLUTE: A LUT-Based Floating-Point Engine for Efficient LLM Acceleration Exploiting Core-Tail Hierarchical Alignment` (MICRO 2026, `macro_pool`, 13w / 3 hyphens) & `M-ANT: Efficient Low-bit Group Quantization for LLMs via Mathematically Adaptive Numerical Type` (HPCA 2025, `contrast_post2023`, `conf__hpca__HuZ00GH00GL25`) | 一口气塞入 `Efficient` + `Low-bit Group` + `Mathematically Adaptive Numerical Type` 等多层嵌套修饰语，读起来像把整个摘要压缩进标题。 |
| **反模式 C：无锚点干瘪长句** | `Coherence protocol for transparent management of scratchpad memories in shared memory manycore architectures` (ISCA 2015, `contrast_ordinary`, `conf__isca__AlvarezVMCGMNAV15`, 14w) | 14 词冗长平铺、缺乏可引用系统名、连 Title Case 大小写都不规范，读者合上论文便完全记不住名字。 |
| **获奖论文标题小疵（慎学）** | `Darwin: A Genomics Co-processor Provides up to 15,000X Acceleration on Long Read Assembly` (ASPLOS 2018, `conf__asplos__TurakhiaBD18`, 14w) & `Scalable and Secure Row-Swap: Efficient and Safe Row Hammer Mitigation in Memory Systems` (HPCA 2023, `conf__hpca__WooSN23`, 13w) | 前者在标题放 `"Provides up to 15,000X"` 带有过强广告推销味（在全语料 152 篇中仅此 1 例在标题放加速比）；后者在同一标题里叠放 `Scalable / Secure / Efficient / Safe` 四个形容词（`Secure` 与 `Safe` 近义重复）。 |

---

## 2. 摘要解剖学（Abstract Anatomy：N=148 定量 + 逐句动作编排）

### 2.1 篇幅、句数、句长与定量克制统计

**表 2：全语料干净摘要（N=148）的篇幅、句法与定量密度统计**

| 维度分组 | 样本数 | 词数中位（均值） | 句数中位（均值） | 句均词长 | 含任何定量指标 | 含 `%` 或 `×` 头条数 | `%`/`×` 数量中位（均值 / 最大） | `%`/`×` 分布：`0` / `1–2` / `3–5` / `6+` |
|---|---:|---:|---:|---:|---:|---:|---:|---|
| **ALL clean_abs** | 148 | **212** (211) | **9.0** (9.4) | **23.2** | **71.6%** (106) | **70.3%** (104) | **2.0** (1.8 / 10) | 44 / **64** / 33 / **7** |
| **2011–2015** | 47 | 214 (210) | 10.0 (9.3) | 23.2 | 80.9% (38) | 76.6% (36) | 2.0 (2.3 / 8) | 11 / 20 / 13 / 3 |
| **2016–2022** | 63 | **200** (205) | 9.0 (9.2) | 23.0 | 66.7% (42) | 66.7% (42) | **1.0** (1.5 / 7) | 21 / **31** / 8 / 3 |
| **2023–2026** | 38 | **228** (220) | 9.0 (9.7) | 23.3 | 68.4% (26) | 68.4% (26) | 2.0 (1.8 / 10) | 12 / 13 / 12 / 1 |
| **ISCA** | 37 | 225 (217) | 10.0 (9.4) | 23.7 | 70.3% | 64.9% | 1.0 (1.7 / 7) | 13 / 13 / 9 / 2 |
| **MICRO** | 37 | 223 (219) | 9.0 (9.4) | 24.2 | 75.7% | 75.7% | 2.0 (2.3 / 10) | 9 / 16 / 8 / 4 |
| **HPCA** | 38 | 204 (202) | 10.0 (9.5) | **21.5** | **76.3%** | **76.3%** | 2.0 (2.1 / 8) | 9 / 15 / 13 / 1 |
| **ASPLOS** | 36 | **190** (203) | 9.0 (9.1) | 23.3 | 63.9% | 63.9% | **1.0** (1.3 / 5) | 13 / **20** / 3 / **0** |
| **`exemplar`** | 31 | 215 (210) | 9.0 (9.3) | 23.4 | 71.0% | 67.7% | **2.0** (1.6 / 7) | 10 / **14** / 6 / 1 |
| **`contrast_ordinary`** | 10 | 176 (203) | 8.5 (8.7) | 24.6 | 80.0% | 80.0% | 2.0 (2.1 / 6) | 2 / 5 / 2 / 1 |
| **`contrast_post2023`** | 6 | 220 (223) | 10.0 (10.5) | 21.9 | 66.7% | 66.7% | 1.5 (1.7 / 4) | 2 / 2 / 2 / 0 |

#### 摘要统计核心发现：
- **长度分布与黄金区间**：全语料摘要词数 `Q1=175w, median=212w, Q3=247w`（150–280 词占 **77.7%**，115/148）；超过 280 词的摘要仅占 **8.8%**（13/148）。人工精确核验显示，顶尖纯人类大师经常写出惊人凝练的“钻石型短摘要”：`Amdahl's Law` (**83 词 / 5 句**, HPCA 2018)、`PVCoherence` (**89 词 / 4 句**, HPCA 2014)、`HFI` (**100 词 / 5 句**, ASPLOS 2023)、`MorphCore` (**112 词 / 4 句**, MICRO 2012)、`Swarm` (**129 词 / 6 句**, MICRO 2015)、`Pond` (**164 词 / 10 句**, 句均仅 **16.4 词**!, ASPLOS 2023)。
- **定量克制铁律**：虽然 **70.3%** 的摘要包含 `%` 或 `×` 头条结果，但 **1–2 个核心数字是最主流、最克制的甜区（43.2%，`exemplar` 达 45.2%，ASPLOS 高达 55.6% 且 0 篇超过 5 个）**；一次性在摘要塞入 **6 个以上 `%`/`×` 数字**的论文仅占 **4.7%**（7/148），极易引发审稿人数字疲劳（如 `Alvarez15` 在最后一句话硬塞 `4% / 8% / 9% / 1.14x / 29% / 17%` 六个数；即使是 MICRO 2022 Best Paper `Whisper` 也因塞入 `3.0 (0.5-7.2) / 2.8% (0.4%-4.6%) / 16.8% (1.7%-32.4%) / 7.9%` 而略显拥挤）。

### 2.2 顶级摘要的五步逐句动作编排（Five-Move Choreography）

顶级纯人类摘要几乎严格遵循一条紧凑的五步逻辑弧线（或“机制前置”变体）：
**Move 1 领域事实/瓶颈（1–2 句）→ Move 2 核心张力/现有失灵根因（1–2 句）→ Move 3 关键洞见（1–2 句）→ Move 4 具体机制（2–3 句）→ Move 5 克制的头条结果（1–2 句）**。

#### 黄金范例逐句拆解：`Pond` (ASPLOS 2023 Distinguished Paper, `conf__asplos__LiBHEZNSRLAHFB23`, p. 1 — 164 词 / 10 句 / 句均 16.4 词)
- **[S1–S2 | Move 1 领域事实]** `"Public cloud providers seek to meet stringent performance requirements and low hardware cost. A key driver of performance and cost is main memory."`（两句分别仅 12 词和 11 词！干净利落立定舞台。）
- **[S3–S4 | Move 2 张力急转]** `"Memory pooling promises to improve DRAM utilization and thereby reduce costs. However, pooling is challenging under cloud performance requirements."`（用 `However,` 精准切出“成本 vs 云性能 SLA”矛盾。）
- **[S5–S6 | Move 4 系统定位+基座]** `"This paper proposes Pond, the first memory pooling system that both meets cloud performance goals and significantly reduces DRAM cost. Pond builds on the Compute Express Link (CXL) standard for load/store access to pool memory and two key insights."`
- **[S7–S9 | Move 3 双重核心洞见+机制落地]** `"First, our analysis of cloud production traces shows that pooling across 8-16 sockets is enough to achieve most of the benefits. This enables a small-pool design with low access latency. Second, it is possible to create machine learning models that can accurately predict how much local and pool memory to allocate to a virtual machine (VM) to resemble same-NUMA-node memory performance."`（每条洞见直接对应一个具体设计决策。）
- **[S10 | Move 5 克制的头条实证]** `"Our evaluation with 158 workloads shows that Pond reduces DRAM costs by 7% with performance within 1-5% of same-NUMA-node VM allocations."`（仅给出 **2 组**最核心的代价-收益平衡数字 `7%` 与 `1-5%`，绝不堆砌次要指标！）

#### 变体：机制前置型摘要（适合工具/基础架构/清晰框架类）
`Swarm` (MICRO 2015, `conf__micro__JeffreySYES15`, p. 1)、`FireSim` (ISCA 2018, `conf__isca__KarandikarMKBAL18`, p. 1)、`Amdahl's Law` (HPCA 2018, `conf__hpca__ZahediLL18`, p. 1)、`HFI` (ASPLOS 2023, `conf__asplos__NarayanGTRM0FVL23`, p. 1) 干脆省略 Move 1 铺垫，**第一句话直奔系统本身**：
> `"We introduce Hardware-assisted Fault Isolation (HFI), a simple extension to existing processors to support secure, flexible, and efficient in-process isolation."` (`HFI`, ASPLOS 2023, `conf__asplos__NarayanGTRM0FVL23`, p. 1)

### 2.3 首句工艺：锋利物理切入 vs 廉价 AI/教科书清嗓子

对比 48 篇 `deep_read` 论文的摘要首句，纯人类大师与后 2023 AI 污染样本的差距在**第一句话的前 15 个词**就已彻底拉开：

- **纯人类宗师首句（直击物理事实、不变量或核心瓶颈，通常 10–18 词）**：
  - `"Modern DRAMs have multiple banks to serve multiple memory requests in parallel."` (`SALP`, ISCA 2012, `conf__isca__KimSLLM12`, p. 1 — 12 词)
  - `"Memory isolation is a key property of a reliable and secure computing system — an access to one memory address should not have unintended side effects on data stored in other addresses."` (`RowHammer`, ISCA 2014, `conf__isca__KimDKFLLWLM14`, p. 1 — 直接给出即将被推翻的安全不变量！)
  - `"Hardware speculation offers a major surface for micro-architectural covert and side channel attacks."` (`InvisiSpec`, MICRO 2018, `conf__micro__YanCS0FT18`, p. 1 — 13 词)
  - `"The memory wall places a significant limit on performance for many modern workloads."` (`Vector Runahead`, ISCA 2021, `conf__isca__NaithaniA0E21`, p. 1 — 13 词)
  - `"CPUs routinely offload to NICs network-related processing tasks like packet segmentation and checksum."` (`Autonomous NIC Offloads`, ASPLOS 2021, `conf__asplos__PismennyEYL0T21`, p. 1 — 13 词)
  - `"Processing-in-memory (PIM) has been explored for decades by computer architects, yet it has never seen the light of day in real-world products due to its high design overheads and lack of a killer application."` (`Pathfinding Future PIM`, HPCA 2024, `conf__hpca__HyunKLR24`, p. 1 — 用 `yet` 一句道尽数十年历史张力！)
- **反面教材 A — 乏味的人类套话（`contrast_ordinary`）**：
  - `"Hardware-assisted security is emerging as a promising avenue for protecting computer systems."` (`Authenticache`, MICRO 2015, `conf__micro__BachaT15`, p. 1 — 泛泛而谈，完全可贴在任意一篇安全论文上)
  - `"The increasing number of cores in manycore architectures causes important power and scalability problems in the memory subsystem."` (`Alvarez15`, ISCA 2015, `conf__isca__AlvarezVMCGMNAV15`, p. 1 — 空洞形容词 `important`)
- **反面教材 B — 典型后 2023 AI 腔清嗓子（`contrast_post2023` 与 2025 受污染获奖论文）**：
  - `"Large language models (LLMs) have revolutionized natural language processing (NLP) domain by achieving state-of-the-art performance across a range of benchmarks."` (`PICACHU`, ASPLOS 2025, `conf__asplos__QinXT0Z25`, p. 1 — `revolutionized` 夸大 + 缺冠词语法伤)
  - `"Recent advances in reasoning Large Language Models (LLMs) are driving the emergence of agentic AI systems."` (`FastTTS`, ASPLOS 2026, `conf__asplos__ChenML0MLF26`, p. 1 — 经典 GPT 模板 `"Recent advances in X are driving the emergence of Y"`)
  - `"Large language models (LLMs) are one of the most important killer computer applications."` (`M-ANT`, HPCA 2025, `conf__hpca__HuZ00GH00GL25`, p. 1 — 夸张口语 `killer`)
  - **【警惕：获奖论文也已受污染】** `"The rapid evolution and widespread adoption of generative large language models (LLMs) have made them a pivotal workload in various applications."` (`DynamoLLM`, HPCA 2025 Best Paper, `conf__hpca__StojkovicZGTC25`, p. 1 — `rapid evolution and widespread adoption` + `pivotal workload`，典型的后 2023 LLM 润色腔，绝不可因它是 Best Paper 就去模仿！)

---

## 3. 引言编排学（Introduction Choreography：“黄金前 1.5–2 页”）

### 3.1 “黄金前两页”的实证边界、Figure 1 占位与导读段消亡曲线

**表 3：全语料干净引言（N=145）的长度、首图占位、贡献列表与导读段 15 年演变**

| 维度分组 | 样本数 | 引言页宽中位（均值） | 引言结束页中位 | 引言词数中位 | Fig. 1 在 p.1 | Fig. 1 在 p.2 | Fig. 1 在 p.1–2 合计 | 引言引用 Fig. 1 | 含贡献列表 | 贡献条数中位（众数） | 含传统论文导读段 |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| **ALL clean_intro** | 145 | **1.12p** (1.19p) | **p.1.74** | **968w** | 16.6% | 49.0% | **65.5%** | 57.9% | **65.5%** | **3.0** (3–4) | 23.4% (34) |
| **2011–2015** | 44 | 0.99p (1.13p) | p.1.63 | 872w | **11.4%** | 63.6% | 75.0% | 59.1% | 61.4% | 3.0 | **43.2%** (19) |
| **2016–2022** | 61 | 1.10p (1.18p) | p.1.72 | 943w | 13.1% | 44.3% | 57.4% | 50.8% | 59.0% | 3.0 | **19.7%** (12) |
| **2023–2026** | 40 | **1.22p** (1.26p) | **p.1.91** | **1,038w** | **27.5%** | 40.0% | **67.5%** | **67.5%** | **80.0%** | **4.0** | **7.5%** (3) |
| **ISCA** | 37 | 1.05p (1.08p) | p.1.60 | 896w | 13.5% | 54.1% | 67.6% | 54.1% | 62.2% | 3.0 | 21.6% |
| **MICRO** | 38 | **0.95p** (1.06p) | p.1.72 | 926w | 18.4% | 47.4% | 65.8% | 57.9% | **73.7%** | 4.0 | **13.2%** |
| **HPCA** | 35 | 1.20p (1.24p) | p.1.64 | 982w | **25.7%** | 37.1% | 62.9% | 51.4% | 65.7% | 3.5 | **40.0%** |
| **ASPLOS** | 35 | **1.29p** (1.38p) | **p.1.90** | **1,086w** | 8.6% | **57.1%** | 65.7% | **68.6%** | 60.0% | 4.0 | 20.0% |
| **`exemplar`** | 30 | 1.08p (1.08p) | p.1.63 | 927w | 16.7% | 50.0% | 66.7% | 53.3% | 60.0% | 4.0 | **13.3%** |
| **`contrast_ordinary`** | 10 | 1.04p (1.07p) | p.1.61 | 862w | 10.0% | 60.0% | 70.0% | 60.0% | 90.0% | 4.0 | 20.0% |
| **`contrast_post2023`** | 6 | 1.24p (1.26p) | **p.1.93** | 1,057w | 16.7% | 50.0% | 66.7% | 66.7% | 83.3% | 3.5 | **0.0%** |

#### 三大颠覆性定量发现：
1. **82.8% 的论文在 Page 2 结束前完成 Introduction**：精确分布显示，`ends_at_page` 的 `Q1=p.1.44, median=p.1.74, Q3=p.1.93`，高达 **120/145 (82.8%)** 在第 2 页末尾之前结束引言，**136/145 (93.8%)** 在第 2.5 页之前结束！审稿人翻完第 2 页还没看到 Section 2 往往就会产生“冗长失焦”的负印象（仅少数含大幅生产激励图/多作者抬头的 ASPLOS/ISCA 系统论文如 `Pond` p.2.43、`Contiguitas` p.2.37、`LLM.265` p.2.39 延伸至第 3 页顶部）。
2. **Figure 1 正在大举前移至 Page 1（11.4% → 27.5%，翻倍有余！）**：在全语料中，**65.5%** 将 Fig. 1 锚定在前两页；2023–2026 年超过四分之一（**27.5%**）的论文直接在 **Page 1 右上角或底部**安放高信息密度首图，且 **67.5%** 在 Intro 中直接引用 Fig. 1！顶级首图绝非空洞的“卡通概念画”，而是四类硬核视觉锚点之一：
   - **逻辑 vs 物理真相揭示图**：`SALP` (`conf__isca__KimSLLM12`, p. 2 Fig. 1 对比 Bank 的逻辑抽象与 64 个 Subarray 的物理真实)；
   - **瓶颈量化/胜利预览图**：`Vector Runahead` (`conf__isca__NaithaniA0E21`, p. 2 Fig. 1 CPI 堆叠图直接对比 OoO / PRE / VR)、`Row-Swap` (`conf__hpca__WooSN23`, p. 1 Fig. 1 双子图直接画目标箭头 `GOAL`)、`Chasing Carbon` (`conf__hpca__GuptaKLTLW0W21`, p. 1–2 Fig. 1–2 能源与碳排放剪刀差)；
   - **代码/微案例锚定图**：`InvisiSpec` (`conf__micro__YanCS0FT18`, p. 1 Fig. 1 直接贴出 15 行 Spectre v1 攻击代码)、`PF-LLM` (`conf__asplos__XuSLBWLX026`, p. 2 Fig. 1 用 C 语言银行账户代码一眼展示 4 种访存模式)；
   - **带章节指针的对比矩阵/分类树**：`RMM` (`conf__isca__KarakostasGACHM15`, p. 2 Table 1 + Fig. 1)、`Autonomous NIC Offloads` (`conf__asplos__PismennyEYL0T21`, p. 2 Fig. 1 在树叶节点直接标注 `§2.1 / §2.2 / §2.3 / §2.4 / §3`)。
3. **“The rest of this paper is organized as follows...” 导读段已彻底消亡！**
   逐年统计（N=145）画出了计算机体系结构写作史上最陡峭的规范迁移曲线：
   - `2011–2015`：**43.2%**（2011: 50%, 2012: 33%, 2013: 62%, 2014: 40%, 2015: 33%）
   - `2016–2022`：**19.7%**（2016: 44% → 2019: 12% → 2021: 10% → 2022: 11%）
   - `2023–2026`：**7.5%**（2023: 10%, 2024: 20%, **2025: 0% [0/12], 2026: 0% [0/8]**！）
   - **替代方案**：顶尖现代作者已彻底弃用浪费 5–8 行的机械导读段，改为将 `(§2)`、`（Section IV）` 等括号指针自然编织进 Intro 叙述句或贡献清单末尾（如 `Amdahl's Law` HPCA 2018 p. 1、`Eyeriss` ISCA 2016 p. 2、`HFI` ASPLOS 2023 p. 2、`Constable` ISCA 2024 p. 2）。**凡在 2025+ 年仍手写 `"The rest of this paper is organized as follows. Section 2 presents background..."`，不仅白白浪费宝贵前两页版面，还会瞬间散发“过时/新手/低级模板”气息。**

---

### 3.2 顶级纯人类引言的逐段编排蓝图（6–8 段“黄金前两页”剧本）

精读 `SALP`、`MorphCore`、`RMM`、`PVCoherence`、`Vector Runahead`、`Whisper`、`Pond`、`Contiguitas`、`Row-Swap`、`HFI`、`Pathfinding PIM` 等标杆范本后，可提炼出一套高度一致的 **7 段式纯人类引言剧本**（通常 850–1,250 词，跨 1.0–1.5 页）：

| 段落位次 | 叙事功能（Move） | 黄金写法与范本示范（核验自原文） | 禁忌反模式 |
|---|---|---|---|
| **P1（~80–120w）** | **冷峻领域定锚（Opening Hook）** | **绝不复制 Abstract 首句！**用极短一句交代核心不变量、系统现实或业界原话：<br>• `PVCoherence` (HPCA 2014, `conf__hpca__ZhangBES14`, p. 1): `"There is a tension in cache coherence protocol design between performance and verification difficulty."`（14 词定调！）<br>• `Contiguitas` (ISCA 2023, `conf__isca__ZhaoXWSYMWRST023`, p. 2): `"Memory capacity has increased dramatically over the last decades, yet modern operating systems have throughout stuck with a small base page size."`<br>• `Pathfinding PIM` (HPCA 2024, `conf__hpca__HyunKLR24`, p. 1): 直接用斜体引述 Facebook 2021 论文原话（`"Perhaps the biggest challenge of PIM is its programmability..."`）开篇！<br>• `Whisper` (MICRO 2022, `conf__micro__KhanUNSLJK22`, p. 1): 直切商业痛点 `"incurring performance losses worth millions of dollars [1, 2, 3, 4, 5, 6, 7]."` | 严禁 `"In recent years..."`、`"In the ever-evolving realm of..."`、`"In the past decade, the landscape of artificial intelligence (AI) has undergone a profound transformation..."`（`QPlacer`, ISCA 2025, `conf__isca__Zhang0D0AO0B0025`, p. 1; `PICACHU`, ASPLOS 2025, `conf__asplos__QinXT0Z25`, p. 1）。 |
| **P2（~100–150w）** | **量化痛点与现实张力（Concrete Bottleneck）** | 用具体硬件物理机制 + 1–2 个权威实测数字坐实问题严重性：如 `RMM` (ISCA15, p. 1) 指出页表遍历占高达 **50%** 执行时间；`Pond` (ASPLOS23, p. 1–2) 引 Azure DRAM 占服务器成本 **50%**、Meta 占 **40%**，并抛出自身实测 **25%** 搁浅内存。 | 切忌仅用形容词渲染（`"substantial challenges"`, `"severe degradation"`, `"paramount"`）而无真实物理/数据支撑。 |
| **P3–P4（~200–280w）** | **为什么现有路线从根源上失灵（Root-Cause Gap）** | 按**逻辑维度归类**（通常 2–3 类）逐一拆穿根源缺陷，而非逐篇报流水账：<br>• `SALP` (ISCA12, p. 1) 精准排除增加 Bank 数的三条路：芯片内增 Bank（面积代价）、通道插多 DIMM（降频）、增内存通道（封装引脚昂贵，脚注给出 Sandy Bridge 264 pins / POWER7 640 pins）；<br>• `MorphCore` (MICRO12, p. 1) 先排 ACMP（设计期固定配比），再排 CoreFusion（关键回路延迟 + 切模式刷缓存迁移数据）；<br>• `RMM` (ISCA15, p. 1) 用编号 1/2/3 拆解 Multipage / Huge Pages / Direct Segments 三代方案，并与 p. 2 Table 1 呼应。 | 忌写成无主线的相关工作堆砌（如 `Authenticache` p. 1 花整整一大段逐篇讲 Lee et al.、环振器、上电状态）；忌用机械 `Challenge-1 / Challenge-2 / Challenge-3` AI 套壳（`FastTTS` p. 2）。 |
| **P5（~120–180w）** | **核心洞见 / 中心命题（Key Insight / Central Question）** | **整篇论文的灵魂拐点！**把“为什么以前做不到而我们能做到”浓缩成 1–2 个反直觉物理/系统观察：<br>• `Vector Runahead` (ISCA21, p. 1): 打破“runahead 遇缺失就跳过”的固有前提——只要一次能同时为多条链停顿并向量化，就可以预取整条依赖链；<br>• `Constable` (ISCA24, p. 1): 显式给出 `Condition 1`（源寄存器未写）与 `Condition 2`（地址无 store/snoop）两条充要安全条件；<br>• `PF-LLM` (ASPLOS26, p. 2): 提出斜体中心问题 `"If an experienced developer can identify these memory access patterns from code, can a modern large language model (LLM) perform the same task automatically?"` | 忌跳过洞见直接抛出“我们提出了一个包含三模块的高效框架”，让审稿人看不出**为什么你的设计不是堆工程**。 |
| **P6（~150–220w）** | **系统与关键机制综述（Concrete System Summary）** | 用具名硬件/软件机制说明如何落地洞见（例如 `MorphCore` 复用的 PRF/RS、`Autonomous NIC Offloads` 的“跳过-补齐-失序回退与魔数重同步”三原则、`Pond` 的 zNUMA + 预测模型 + 误判兜底迁移）。可配极简粗体引导词（如 `Pond` 的 `Our work.`、`Constable` 的 `Key mechanism.`）。 | 忌陷入底层位宽/状态机细枝末节（留给 Section 3/4），也忌用空洞 AI 宣传语（`"meticulously designed"`, `"synergistic optimizations"`, `"seamlessly integrates"`）。 |
| **P7（~80–130w）** | **评估配置与头条结果（Empirical Headline）** | 给出比 Abstract 更清晰的验证语境：原型/仿真器类型（Linux kernel / gem5 / FPGA / 真实集群）、工作负载规模、对比基线、核心性能/能耗收益 + **诚实报告代价/开销**（如 `Whisper` p. 2 主动披露 `11.4%` 代码膨胀与 `9.8%` 额外动态指令；`Vector Runahead` p. 2 报 `1.3 KB` 额外状态）。 | 忌与 Abstract 末段逐字复制（如 `Elastic Cuckoo` p. 1–2）；忌只报最好值隐瞒开销。 |
| **P8（~120–180w，可选）** | **贡献清单（Contributions）** | 3–4 条精炼、互斥、具体、可核验的贡献条目（强烈建议末尾附 `(§X)` 章节锚点），**直接替代传统导读段**。 | 忌超长 6–7 条（`Constable`）、忌用 `"To our knowledge, this is the first..."` 充数、忌末尾再加 80 词的 `"The rest of this paper is organized..."`。 |

> **高阶结构变体提示**：
> - **分段小标题法**：`Pond` (`conf__asplos__LiBHEZNSRLAHFB23`, p. 1–2) 在长达 1.83 页的引言中使用 `Motivation.` / `Limitations of the state of the art.` / `Our work.` / `Artifacts.` / `Contributions.` 五个粗体段首引导词，`Contiguitas` (`conf__isca__ZhaoXWSYMWRST023`, p. 2) 设立 `1.1 This Paper: Ample Physical Memory Contiguity by Design.`，大幅提升了大篇幅系统引言的可扫描性。
> - **无贡献清单的纯散文大师体**：若引言控制在 0.8–1.1 页内且逻辑极其顺滑（如 `Vector Runahead`, `Elastic Cuckoo`, `Autonomous NIC Offloads`, `Amdahl's Law`, `HFI`, `Pathfinding PIM`），完全可以省略项目符号清单——`exemplar` 中 **40%** 都不使用贡献列表！

---

## 4. 贡献条目清单（Contribution Bullet Lists）专项剖析

### 4.1 定量分布与动词图谱（N=145）

1. **普及率攀升**：显式贡献列表出现率从 `2011–2015` 的 **61.4%** 与 `2016–2022` 的 **59.0%** 跃升至 `2023–2026` 的 **80.0%**（2025 年 92%，2026 年 88%）。
2. **条数黄金规律（3–4 条占 72.9%）**：在 85 篇干净项目符号/编号贡献清单中，分布高度集中：`3 条` 33 篇（38.8%）、`4 条` 29 篇（34.1%）、`2 条` 10 篇（11.8%）、`5 条` 10 篇（11.8%）、`6 条` 2 篇（2.4%）、`7 条` 1 篇（1.2%，即 `Constable`）；中位 **3.0 条**、均值 **3.58 条**。
3. **句法与动词偏好**：
   - `We + 动词` 占压倒性优势（155 次），其次是纯名词短语（87 次，如 `Whisper`、`"• An extensive investigation..."`）、带粗体小标题引出（22 次），以及无主语第三人称动词（6 次，如 `Authenticache` `"• Presents..."`——略显生硬，不推荐）。
   - **纯人类高频实词 Top 12**：`propose` (43)、`show` (18)、`present` (14)、`design` (11)、`develop` (10)、`demonstrate` (10)、`evaluate` (7)、`identify` (7)、`introduce` (6)、`describe` (5)、`conduct` (4)、`implement/open-source` (4)。注意：**真实架构顶会极少在贡献首动词使用 `leverage`、`facilitate`、`unveil`、`spearhead`、`craft`、`harness`、`delve` 等 AI 高频空泛动词！**

### 4.2 优秀贡献清单 vs 差劲/AI 膨胀贡献清单逐字对照

#### 正面典范 1：`Row-Swap` (HPCA 2023 Best Paper, `conf__hpca__WooSN23`, p. 2 — 3 条，攻-防-扩展闭环，具体且无废话)
> `1) We develop a new targeted attack pattern, Juggernaut, that breaks RRS by exploiting the mitigative action of row swaps (and unswap operations) in under 1 day.`
> `2) We propose Secure Row-Swap (SRS), an RH mitigation that prevents unswap-swap operations and defends against the Juggernaut attack pattern. Moreover, SRS also includes attack detection to detect future attack patterns against row-swap-based RH defenses.`
> `3) We propose Scale-SRS, a scalable solution that can securely reduce the swap rate by combining outlier-based attack detection and LLC-pinning of outlier rows as mitigation. This improves the performance, storage costs, and scalability of row-swap-based RH defenses at lower TRH values.`
- **精妙处**：每一条都有**专属命名实体**（`Juggernaut`、`SRS`、`Scale-SRS`）+ **具体技术动作**（`prevents unswap-swap`、`LLC-pinning of outlier rows`）+ **明确量化/安全目标**（`in under 1 day`、`lower TRH values`），三条之间层层递进、互不重叠。

#### 正面典范 2：`Eyeriss` (ISCA 2016 Top Picks, `conf__isca__ChenES16`, p. 2 — 4 条，名词短语 + 精准章节锚点)
> `• A taxonomy that classifies existing CNN dataflows from previous research. (Section IV)`
> `• A spatial architecture based on a new CNN dataflow, called row stationary, which is optimized for throughput and energy efficiency. ... This dataflow has also been demonstrated on a fabricated chip. (Section V)`
> `• An analysis framework that can quantify the energy efficiency of different CNN dataflows under the same hardware constraints. ... (Section VI-C)`
> `• For a variety of CNN dataflows, we present a comparative analysis of the energy costs associated with data movement and the impact of different types of data reuse. (Section VII)`
- **精妙处**：直接用 `(Section IV / V / VI-C / VII)` 替代了传统导读段，且将“分类法 → 新架构/流片 → 分析框架 → 对比评估”切分得极其干净。

#### 反面教材 1（Class A 差劲人类写法）：`PREMA` (HPCA 2020, `contrast_ordinary`, `conf__hpca__ChoiR20`, p. 2) & `TimeCache` (ISCA 2021, `contrast_ordinary`, `conf__isca__OjhaD21`, p. 2)
- `PREMA` 前两条连续抢“第一”且空泛：
  > `• To the best of our knowledge, our work is the first to explore multi-tasked DNNs, an important and emerging problem space that has not been addressed by prior work.`
  > `• This paper is the first to provide an in-depth, quantitative analysis on the architectural support required for enabling preemption on NPUs.`
  （注：连同 `Pond` 的三连 `"The first..."` 和 `PF-LLM` 第 4 条 `"To our knowledge, this is the first work..."`，**把“我是第一个”当成独立贡献条目是体系结构审稿人最反感的习惯之一**——如果真是首创，用具体机制本身说话，而非靠声明抢功。）
- `TimeCache` 把一个简单核心想法硬拆成 5 条碎片化名词短语（第 1 条 `"Preventing reuse attack..."` 与第 2 条 `"The insight that disallowing the first access..."` 实质重复）。

#### 反面教材 2（Class B 后 2023 AI 膨胀写法）：`QPlacer` (ISCA 2025, `contrast_post2023`, `conf__isca__Zhang0D0AO0B0025`, p. 2) & `FastTTS` (ASPLOS 2026, `contrast_post2023`, `conf__asplos__ChenML0MLF26`, p. 2–3)
- `QPlacer` 5 条中充斥虚浮 AI 修饰语与自吹：
  > `• We propose Qplacer, a framework designed to meticulously craft the physical layout of superconducting QCs effectively mitigating various crosstalk impacts while optimizing for a compact substrate size.`
  > `• To achieve this, Qplacer designs Frequency-Aware Electrostatic-based Placement Engine, which envisions quantum components as particles...`
  （`meticulously craft`、`envisions`、`facilitating the placement process`、`addressing the unique challenges`——花哨空转，且把框架与框架里的引擎强拆两条，甚至有语法漏洞 `"Qplacer proposes padding technique"` 漏冠词。）
- `FastTTS` 3 条全是最典型的 LLM 通用空壳模板：
  > `• We systematically analyze the common execution patterns of modern verifier-guided TTS methods and identify their core system-level bottlenecks with a comprehensive performance profiling.`
  > `• We design and implement FastTTS, a high-performance serving system for TTS that incorporates three novel and synergistic optimizations: ...`
  > `• We conduct a comprehensive evaluation on representative edge hardware, demonstrating that FastTTS achieves ...`
  （`systematically analyze` + `comprehensive performance profiling` + `three novel and synergistic optimizations` + `conduct a comprehensive evaluation`——几乎套用在任何系统论文上都一字不差，是典型的“零信息密度 AI 模板”！）

---

## 5. 三方逐字对比实验室：Gold Pure-Human vs Bad Human vs Post-2023 AI-Tainted

为了给 Phase 2 写作技能提供最直观的“品味标尺”，下面精选三组横跨同主题/同位置的逐字原文对照：

### 对比组 1：引言第一段开篇（Opening Hook）

| 类别与来源 | 逐字原文（核验自 `macro_cache`） | 逐词诊断 |
|---|---|---|
| **[GOLD-HUMAN]**<br>`Vector Runahead`<br>(ISCA 2021 Top Picks, `conf__isca__NaithaniA0E21`, p. 1) | `"Modern-day workloads are poorly served by current out-of-order superscalar cores. From databases [40], to graph workloads [49, 67], to HPC codes [11, 30], many workloads feature sparse, indirect memory accesses [9] characterized by high-latency cache misses that are unpredictable by today’s stride prefetchers [1, 19]. For these workloads, even out-of-order superscalar processors spend the majority of their time stalled, since their ample reorder buffer and issue queue resources are still insufficient to capture the memory-level parallelism necessary to hide today’s DRAM latencies."` | **三句 83 词，刀刀见骨**：S1 仅 11 词直接抛出核心论断；S2 立刻锁定 3 类具体负载与具体微架构失效点（stride prefetcher 无法预测间接访存）；S3 直指具体硬件结构（ROB、issue queue、MLP、DRAM 延迟）。零废话、零宏大口号。 |
| **[BAD-HUMAN]**<br>`Alvarez15`<br>(ISCA 2015 `contrast_ordinary`, `conf__isca__AlvarezVMCGMNAV15`, p. 1) | `"Future generations of multicore and manycore architectures are expected to include a significant number of cores. As an immediate consequence, the memory system that connects these computing elements needs to be revisited in order to satisfy the inherent requirements of future chips and, at the same time, avoid the inefficiencies of current schemes when cores are replicated beyond certain levels [31, 35, 39]."` | **教科书废话 + 臃肿被动语态**：`"expected to include a significant number of cores"` 毫无信息量；`"needs to be revisited in order to satisfy the inherent requirements"` 抽象空转，读完 66 词仍不知本文到底要解决什么具体硬件问题。 |
| **[AI-TAINTED]**<br>`PICACHU`<br>(ASPLOS 2025 `contrast_post2023`, `conf__asplos__QinXT0Z25`, p. 1) | `"In the past decade, the landscape of artificial intelligence (AI) has undergone a profound transformation, with Transformer-based Large Language Models (LLMs) redefining the capabilities of AI. These models have emerged as powerful tools across various domains, including natural language processing (NLP) [...] and computer vision (CV) [...], reshaping both industry and human life. ... This underscores the growing demand for hardware acceleration."` | **AI 腔词典全中**：`In the past decade`、`the landscape of`、`undergone a profound transformation`、`redefining the capabilities`、`emerged as powerful tools`、`reshaping both industry and human life`、`underscores the growing demand`。整段读起来像科普公众号导语，而非顶会架构论文。 |

### 对比组 2：引言“亮出方案与核心价值”转折段

| 类别与来源 | 逐字原文（核验自 `macro_cache`） | 逐词诊断 |
|---|---|---|
| **[GOLD-HUMAN]**<br>`Autonomous NIC Offloads`<br>(ASPLOS 2021 Distinguished Paper, `conf__asplos__PismennyEYL0T21`, p. 2) | `"The idea underlying autonomous offloads is for the L5P and NIC to jointly process L5P messages (which may consist of multiple TCP segments) in a manner that is transparent to the intermediating TCP/IP stack. When sending a message, the L5P code “skips” performing the offloaded operation, thereby passing the “wrong” bytes down the stack to the NIC. The NIC then performs the said skipped operation, resulting in a correct message being sent on the wire."` | **画面感极强的纯机制解释**：用 `"skips"` 和 `"wrong" bytes` 两个极其平实生动的人类词汇，三句话就让读者彻底看懂整个软硬件交互魔术，不炫耀任何大词。 |
| **[BAD-HUMAN]**<br>`Turnpike`<br>(MICRO 2021 `contrast_ordinary`, `conf__micro__ZengKLJ21`, p. 1–2) | `"To address the problems, this paper presents Turnpike, a compiler/architecture co-design scheme that can achieve a lightweight yet guaranteed soft error resilience for in-order cores. Turnpike leverages 3 key insights to minimize the pipeline stalls with lowering the store buffer pressure."` | **语法瑕疵 + 机械列表感**：`"with lowering the store buffer pressure"` 明显非母语介词误用；前一段还塞入 `"spying drones [10, 49, 50] and bionic birds [12, 80]"` 等令人出戏的举例。 |
| **[AI-TAINTED]**<br>`QPlacer`<br>(ISCA 2025 `contrast_post2023`, `conf__isca__Zhang0D0AO0B0025`, p. 2) | `"In this study, we systematically investigate and address the multifaceted challenges associated with spatial and frequency constraints in inter-qubit and resonator crosstalk, as well as keeping a compact substrate size to suppress substrate crosstalk. Recognizing the complexity of these issues, our solution pivots on a meticulously designed physical layout that not only scales up QCs but also preserves system fidelity amid these multifaceted interactions. This initiative marks a pivotal advancement in quantum chip design, harmonizing the delicate balance between component isolation and integration in sophisticated quantum systems."` | **教科书级 GPT 浮夸腔标本**：短短 90 词内连爆 `systematically investigate`、`multifaceted challenges`、`Recognizing the complexity`、`meticulously designed`、`not only ... but also ...`、`multifaceted interactions`、`marks a pivotal advancement`、`harmonizing the delicate balance`、`sophisticated`——整段自我吹嘘却几乎没有交代任何具体算法机制！ |

### 对比组 3：2025–2026 顶会内部对照——同样写 LLM，干净人类腔 vs AI 污染腔（甚至发生在 Best Paper 内部！）

- **干净纯人类 LLM 论文范例** — `PF-LLM` (ASPLOS 2026 Best Paper, `conf__asplos__XuSLBWLX026`, p. 1 Abstract):
  > `"Hardware data prefetching is a critical technique for mitigating memory latency in modern processors. While sophisticated hardware prefetching algorithms exist, their exclusive reliance on runtime information limits their ability to adapt quickly and comprehend broader program context. Our key insight is that the optimal prefetching strategy for a load instruction is often discernible from its static code context—a task at which experienced developers excel. This motivates our central question: can a Large Language Model (LLM) be trained to perform this analysis automatically?"`
  （直接从体系结构本体——硬件预取器仅靠运行时信息的局限——自然引出 LLM，零一句 `"LLMs have revolutionized..."` 废话！）
- **受 LLM 润色污染的 2025 获奖论文警示** — `DynamoLLM` (HPCA 2025 Best Paper, `conf__hpca__StojkovicZGTC25`, p. 1 Intro) & `LLM.265` (MICRO 2025 Best Paper, `conf__micro__XuW0CLZW25`, p. 1 Intro):
  - `DynamoLLM`: `"The exponential growth in the adoption of generative large language models (LLMs) has positioned them at the core of numerous technological advancements and applications."`（紧接着首页还出现 `pivotal`、`paramount`、`underscores`、`pave the way towards`！）
  - `LLM.265`: `"Recently, Large language models (LLMs) have achieved significant success, showcasing remarkable proficiency in various applications, such as virtual assistants [60], chatbots [60], and automated customer service platforms [63]."`（甚至把同一条文献 `[60]` 在同一句里连引两次、且 `Large` 大小写失误！）
  - **关键教训**：2024–2026 年的顶会（哪怕 Best Paper）也已有相当比例作者在写 Abstract/Intro 首段时经由 LLM 润色，留下了明显的“AI 塑料壳”。**Phase 2 写作技能必须将 `2011–2022` 纯人类宗师范本（辅以 `PF-LLM` 等干净 2023–2026 段落）作为语言金标准，明确过滤掉 2024–2026 获奖论文里的 AI 润色杂质。**

---

## 6. Phase 2 写作技能（Skill）可直接落地的 12 条“黄金前两页”硬规则

### A. 标题规则（3 条）
1. **【T1-词长与结构锚点】** 严格控制在 **6–10 词**（最高不超过 12 词）；优先采用 **`SystemName: 干净机制副标题`**（如 `Pond: CXL-Based Memory Pooling Systems for Cloud Platforms`）或 **动作/意象短语 + 冒号**（如 `Flipping Bits in Memory Without Accessing Them: ...`）；绝不用问句，除非开创全新原语否则慎用 2–3 词无冒号体。
2. **【T2-命名卫生与禁用强行拼词】** 系统名必须是 1–2 个音节、易发音、贴合语义的真词或自然缩略词（如 `Pond`, `Whisper`, `Constable`, `InvisiSpec`, `Swarm`）；**严禁强行从词中抠字母拼凑可爱缩写（Forced Backronym，如 `PICACHU`）**，且标题中系统名必须与正文 100% 一致。
3. **【T3-修饰词限额】** 全标题连字符复合词 **≤ 2 个**，通用宣传形容词（`Efficient / Scalable / Fast / Secure / Lightweight / High-Performance / Holistic / Novel`）**≤ 1 个**；绝不把具体加速比数字（如 `15,000X`）塞进标题。

### B. 摘要规则（4 条）
4. **【A1-篇幅与句长控制】** 目标 **160–240 词、8–10 句**，句均词长控制在 **18–24 词**（单句绝对禁止超过 45 词，避免 `FireSim` 式 67 词超级长尾句）；单段或双段均可（双段结构：段 1 问题+根因，段 2 方案+结果，极具可读性）。
5. **【A2-五步逐句编排】** 严格执行 `领域事实/瓶颈 (1–2句) → 根因张力 (1–2句) → 核心洞见 (1–2句) → 具体机制 (2–3句) → 头条结果 (1–2句)`；工具/基础设施类可采用“首句直出 `We present X...`”的机制前置变体。
6. **【A3-首句禁令】** 摘要第一句**严禁**以 `"In recent years"`、`"In the past decade"`、`"Recent advances in"`、`"With the rapid growth/evolution of"`、`"X has revolutionized / reshaped / become a pivotal..."` 开头；必须用 10–20 词直接落脚于**具体硬件机制、系统不变量或真实物理瓶颈**。
7. **【A4-定量克制（1–3 个核心数）】** 除纯理论/定性框架外，摘要末尾必给 **1–2 组（最多 3 组）**最具代表性的头条数字（主收益 + 关键开销/对比基线，如 `7% DRAM cost reduction within 1-5% latency`）；严禁无数字空话（`Hestia` 反例），也严禁一口气倾倒 6+ 个指标（`Alvarez15` 反例），且禁止 `"oracle-level / always optimal"` 式过度宣称（`PF-LLM` 瑕疵）。

### C. 引言“黄金前两页”规则（5 条）
8. **【I1-两页铁律与零复读】** Introduction 必须控制在 **1.0–1.5 页（850–1,250 词）**，并在 **Page 2 结束前完成**（最迟不超过 p.2.2）；Intro 首句与末段**严禁复制粘贴 Abstract 原句**（反例：`Elastic Cuckoo` p. 1–2、`Constable` p. 1–2、`FastTTS` p. 1–2），须呈现递进的增量信息。
9. **【I2-首图/首表前两页强锚定】** 强烈建议在 **Page 1（27.5% 现代趋势）或 Page 2（40%–49%）** 安放 **Figure 1（或对比 Table 1）**并在 Intro 正文显式引用；首图必须是**逻辑 vs 物理对比、瓶颈实测、具体代码/微案例、或带章节号的分类树**，绝不放空洞装饰图。
10. **【I3-七段流与中心洞见高亮】** 按 `领域钩子 → 量化瓶颈 → 分类排除现有路线（2–3类） → 核心洞见/中心问题 → 机制落地 → 实证摘要（含诚实开销） → 贡献清单` 推进；若引言超过 1.3 页，使用简洁粗体段首引导词（如 `Motivation.`、`Limitations of prior work.`、`Key insight.`、`Key results.`）增强可读性，但**严禁 AI 模板化的 `Challenge-1 / Challenge-2 / Challenge-3` 套壳**。
11. **【I4-贡献清单克制规范（3–4 条）】** 若使用贡献列表，严格控制在 **3–4 条**（绝不超过 5 条，反例：`Constable` 7 条）；以 `We propose / design / show / identify / evaluate` 等朴实动词引导，每条必须指向**具体具名机制或可验证实证发现**，末尾附 `(§X)` 章节锚点；**禁止以 `"To our knowledge, this is the first..."` 独立充数，禁止使用 `meticulously`、`synergistic`、`comprehensive evaluation` 等空洞 AI 修饰语**。
12. **【I5-彻底废除传统导读段】** **禁止**在引言末尾撰写 `"The rest of this paper is organized as follows. Section 2 describes..."`（2025–2026 顶会已彻底归零为 0%）；改用贡献条目末尾的 `(§2)` / `(Section 3)` 内嵌指针或带章节号的 Fig. 1 分类树完成全文导航。

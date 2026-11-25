# 维度一分析报告：计算机体系结构顶会论文的宏观结构、叙事弧线与篇幅预算（ISCA / MICRO / HPCA / ASPLOS, 2011–2026）

> **实证基础说明**：本报告基于 `corpus/manifest.json` 与 `corpus/macro_cache/` 中全部 **152 篇 `macro_pool` 论文**（ISCA / MICRO / HPCA / ASPLOS 各 38 篇，横跨 2011–2026 共 16 年、三个时代：`2011-2015` 47 篇、`2016-2022` 65 篇、`2023-2026` 40 篇；严格零接触 `held_out_test`）的 Python 全文结构解析（150/152 篇获完整章节树解析，148/152 篇获干净摘要解析，145/152 篇获干净引言解析），并结合对 **35+ 篇 `deep_read` 论文**（覆盖全部 4 会议、3 时代、3 层级：`exemplar` 获奖/顶组范本、`contrast_ordinary` 普通录用人类基准、`contrast_post2023` 后 2023 AI 痕迹对照样本，以及 4 大体系结构研究原型）的逐页原文精读。所有英文引文与页码均直接核验自 `corpus/macro_cache/<paper_id>.json`。

---

## 1. 宏观章节分类体系与篇幅预算（Macro Section Taxonomy & Page/Word Budgets）

### 1.1 总页数膨胀的真相：正文“12 页铁律”与参考文献/Artifact 扩张

过去 15 年间，体系结构四大顶会论文的 PDF 总页数显著拉长，但**真正决定写作节奏的正文预算（从 Section 1 到 Conclusion 结束）高度稳定在 11.3–12.4 页、约 9,600–10,300 词之间**。总页数中位数从 `2011-2015` 的 **12.0 页**升至 `2023-2026` 的 **15.0 页**，主要驱动力并非正文变啰嗦，而是：（1）约 2015–2016 年起四大顶会全面实行“参考文献不计入页数限制”，导致 References 中位篇幅从 **0.9 页**暴涨至 **2.5 页**（几乎翻三倍）；（2）2021 年后 **Artifact Appendix** 的制度化普及（2011–2015 为 0%，2023–2026 达 **17.5%**，2026 年样本高达 **38%**）。

**表 1：全语料（N=152）按时代、会议与层级的总体篇幅与章节数统计**

| 维度分组 | 样本数 | 总页数中位（均值） | 正文页数中位（均值） | References 中位页数 | 正文字数中位 | 顶层章节数中位 |
|---|---:|---:|---:|---:|---:|---:|
| **全语料 ALL** | 152 | **14.0** (13.8) | **11.9** (11.9) | 1.8 | 9,934 | 8.0 |
| **时代 2011–2015** | 47 | 12.0 (12.5) | 11.3 (11.4) | **0.9** | 9,622 | 7.0 |
| **时代 2016–2022** | 65 | 14.0 (13.9) | 11.9 (12.0) | **1.9** | 10,039 | 8.0 |
| **时代 2023–2026** | 40 | **15.0** (15.3) | **12.4** (12.4) | **2.5** | 10,308 | 8.0 |
| **会议 ISCA** | 38 | 14.0 (13.5) | 11.8 (11.7) | 1.5 | 9,996 | 8.0 |
| **会议 MICRO** | 38 | 14.0 (13.8) | 11.9 (11.9) | 1.8 | 9,916 | 8.0 |
| **会议 HPCA** | 38 | 13.0 (13.5) | 11.6 (11.7) | 1.3 | 9,673 | 8.0 |
| **会议 ASPLOS** | 38 | **15.0** (14.6) | **12.4** (12.4) | **2.0** | **10,267** | 8.0 |
| **层级 `exemplar`** | 32 | 14.0 (14.3) | **12.2** (12.2) | 1.9 | **10,299** | 8.0 |
| **层级 `contrast_ordinary`** | 10 | 13.0 (13.6) | 11.4 (11.6) | 2.0 | 10,058 | 8.0 |
| **层级 `contrast_post2023`** | 6 | 15.0 (15.5) | 12.0 (11.8) | **3.0** | 9,639 | 8.5 |

> **关键观察**：`contrast_post2023` 样本尽管总页数最高（中位 15.0p，References 高达 3.0p），其正文字数反而是三层中最低的（9,639 词 vs `exemplar` 的 10,299 词）——更多空间被大号示意图、密集柱状图以及冗余的文献综述/参考文献占据，而深度机制阐述的“含金量密度”反而下降。

---

### 1.2 细粒度章节与功能块篇幅预算（N=150 干净章节解析）

将所有顶层章节归入 14 个细粒度标准类目（并汇总为 7 个核心功能块），可得到四大顶会最真实的“版面经济学”账本：

**表 2：14 类标准章节出现率与条件篇幅预算（N=150；条件统计指“在该论文存在此节时的中位篇幅”）**

| 标准章节类别 | 出现率（占 150 篇） | 条件中位页数（均值） | 条件中位词数 | 占正文页数中位比例 | 典型功能定位 |
|---|---:|---:|---:|---:|---|
| **Introduction** | 150/150 (100.0%) | **1.14p** (1.31p) | 976w | **9.3%** | 黄金前两页定调（与 Title/Abstract 共同在 p.1.74 结束） |
| **Background（独立）** | 71/150 (47.3%) | 1.21p (1.46p) | 1,047w | 10.1% | 领域机制/基线硬件预备知识 |
| **Motivation（独立）** | 38/150 (25.3%) | 1.60p (1.61p) | 1,382w | 12.8% | 实证剖析痛点、量化 headroom 或暴露基线缺陷 |
| **Background & Motivation（合并）** | 18/150 (12.0%) | 1.95p (1.86p) | 1,662w | 16.3% | 一体化背景+痛点论证（微架构论文极常见） |
| **Background & Related Work（合并）** | 8/150 (5.3%) | 1.10p (1.13p) | 1,008w | 9.1% | 将强相关工作前置并融入背景（多见于 HPCA/定量化主题） |
| **Overview（独立顶层节）** | 16/150 (10.7%) | 1.08p (1.14p) | 986w | 9.1% | 多机制/多层级系统的鸟瞰图（如 SALP §4, Graphicionado §3） |
| **Design / Core Architecture** | 134/150 (89.3%) | **4.20p** (4.57p) | **3,700w** | **35.5%** | 全文绝对核心（常拆分为 2–3 个并列设计节） |
| **Implementation & Overhead** | 35/150 (23.3%) | 1.30p (1.65p) | 1,242w | 10.8% | RTL/综合面积功耗、OS 内核集成或硬件开销核算 |
| **Methodology / Setup（独立）** | 72/150 (48.0%) | **0.88p** (1.19p) | 800w | **7.2%** | 模拟器参数、工作负载表、对比基线定义 |
| **Evaluation / Results** | 135/150 (90.0%) | **2.64p** (2.76p) | **2,184w** | **22.9%** | 端到端性能/能耗、消融、敏感性与案例分析 |
| **Discussion & Limitations** | 32/150 (21.3%) | 0.67p (0.98p) | 666w | 5.8% | 边界条件、适用性讨论、工程局限与未来扩展 |
| **Security / Correctness Analysis** | 5/150 (3.3%) | 0.75p (1.27p) | 676w | 6.7% | 形式化/系统性安全证明与侧信道穷举分析（另有大量作为 Eval 子节） |
| **Related Work（独立）** | 123/150 (82.0%) | **0.60p** (0.67p) | 537w | **5.2%** | 文献定位与差异化切割（半页到一页为黄金甜区） |
| **Conclusion** | 130/150 (86.7%) | **0.17p** (0.25p) | **161w** | **1.5%** | 极简收束（通常仅 1 段、约 120–180 词） |

> **注**：少数非设计类论文（如纯表征/测量类论文 `Clearing the Clouds`、`Chasing Carbon`）没有传统 `Design` 节，而是将 4–6 页用于多维度实证测量结果；另有极少数 2025 年 ML/EDA 风格论文（如 `PICACHU`, ASPLOS 2025, `conf__asplos__QinXT0Z25`）把核心设计节命名为 `4 Methodology`（3.26p），我们在下文跨节契约与层级分析中将对此现象作出专项批判。

---

### 1.3 跨时代、跨会议与跨层级的七大功能块预算演变

将细粒度章节合并为 7 大功能块后，**四大会议的“隐性风格偏好”、15 年演进轨迹，以及获奖范本与普通/AI 污染论文的资源分配差异**暴露无遗：

**表 3：七大功能块占正文页数均值比例（% body）与存在时的中位页数（括号内）**

| 分组 | Intro | Bg+Mot（全口径） | Design+Overview+Impl | Meth+Eval | Disc+Lim+SecAnal | Related Work | Conclusion |
|---|---|---|---|---|---|---|---|
| **ALL (n=150)** | 11.0% (1.14p) | 11.6% (1.82p) | **38.4% (4.61p)** | **25.7% (3.24p)** | 2.1% (0.68p) | 4.6% (0.60p) | 1.8% (0.17p) |
| **2011–2015 (n=45)** | 11.5% (1.00p) | **9.3% (1.29p)** | 36.0% (4.29p) | **29.9% (3.35p)** | 1.5% (1.02p) | 5.2% (0.68p) | 2.0% (0.21p) |
| **2016–2022 (n=65)** | 11.2% (1.10p) | 11.0% (1.85p) | 39.9% (5.02p) | 23.9% (3.10p) | 2.8% (0.70p) | 4.8% (0.57p) | 1.7% (0.17p) |
| **2023–2026 (n=40)** | 10.1% (1.22p) | **15.2% (1.99p)** | 38.7% (4.78p) | 24.0% (3.28p) | 1.6% (0.47p) | **3.7% (0.53p)** | **1.7% (0.14p)** |
| **ISCA (n=38)** | 9.2% (1.04p) | 10.8% (1.23p) | 38.3% (4.60p) | 27.4% (2.80p) | 2.4% (0.68p) | **5.4% (0.64p)** | 1.5% (0.17p) |
| **MICRO (n=38)** | **8.9% (0.95p)** | 11.5% (1.80p) | **44.3% (4.99p)** | 22.2% (3.61p) | 2.1% (0.61p) | 4.1% (0.52p) | 1.6% (0.18p) |
| **HPCA (n=36)** | 11.3% (1.21p) | 12.7% (2.02p) | 41.1% (4.56p) | 24.2% (3.23p) | **1.1% (0.75p)** | 3.9% (0.54p) | 2.1% (0.17p) |
| **ASPLOS (n=38)** | **14.6% (1.31p)** | 11.4% (1.99p) | 30.2% (4.21p) | **28.9% (3.30p)** | **2.8% (0.67p)** | 5.1% (0.60p) | 2.0% (0.18p) |
| **`exemplar` (n=31)** | 11.1% (1.11p) | **10.1% (1.65p)** | **42.0% (5.17p)** | 23.0% (3.12p) | **2.8% (0.73p)** | 4.8% (0.59p) | 1.7% (0.17p) |
| **`contrast_ordinary` (n=10)** | 9.3% (1.04p) | 16.9% (1.97p) | 36.9% (4.25p) | 22.1% (2.83p) | 4.8% (1.22p) | 5.0% (0.59p) | **0.6% (0.12p)** |
| **`contrast_post2023` (n=6)** | 10.7% (1.24p) | **17.9% (2.27p)** | 30.2%*(3.25p*) | 31.5%*(3.09p*) | **0.6% (0.40p)** | **2.8% (0.53p)** | 1.3% (0.13p) |

> `*` 提示：`contrast_post2023` 中 `PICACHU` (`conf__asplos__QinXT0Z25`) 将 3.26 页的硬件/编译器设计节命名为 `4 Methodology`，若将该节归回 Design，则 `contrast_post2023` 的 Design 均值约 35%、Eval 约 27%——即便如此，其 **Bg+Mot 占比高达 17.9%（中位 2.27 页）** 仍远高于 `exemplar` 的 **10.1%（中位 1.65 页）**，体现出后 2023 论文普遍“前戏过长、设计纵深偏浅、Discussion/Limitations 缺失（仅 1/6 设有，显式 Limitations 为 0/6）”的结构失衡。

#### 四大版面预算核心发现：
1. **“40-25-20-15” 黄金版面分配律**：一篇标准的 12 页正文体系结构顶会范本，其经验预算锚点为：**设计/机制与实现约 40%–45%（4.5–5.5 页）**，**实验方法与评估约 25%–30%（3.0–3.5 页）**，**引言+背景/动机合计约 20%–25%（Intro ~1.1p + Bg/Mot ~1.5–2.0p）**，**讨论/相关工作/结论收尾合计约 8%–12%（Disc ~0.5p + RW ~0.6p + Conc ~0.15p）**。
2. **四大会议的鲜明“气质指纹”**：
   - **MICRO** 最崇尚“硬核微架构深度”：`Intro` 最短（中位 0.95p），`Design+Overview+Impl` 占比冠绝四会（**44.3%**，中位 4.99p），评审人最看重微架构框图、状态机与边界微操细节。
   - **ASPLOS** 最重“跨层系统叙事与完整实证”：`Intro` 最长（中位 1.31p / 1,113w），`Meth+Eval` 最重（28.9%，中位 3.30p），`Artifact Appendix` 比例最高（13.2%），`Discussion/Limitations` 意识最强（显式 Limitations 标题 15.8%）。
   - **ISCA** 最均衡且包容度广：`Meth+Eval` 出现率 100%，`Discussion/Limitations` 出现率 26.3% 与 ASPLOS 并列最高，同时容纳纯硬件微架构与数据中心/云系统论文。
   - **HPCA** 最偏重工程性能实测与背景铺垫：`Bg+Mot` 中位达 2.02p，但 `Discussion/Limitations` 出现率显著低于其他三会（仅 11.1%，显式 Limitations 仅 2.8%）。
3. **15 年来最大的结构迁移——“前置实证动机化”与“尾部极限压缩”**：
   - 2011–2015 年，仅 57.8% 的论文有显式 `Background/Motivation` 节（中位 1.29p）；到 2023–2026 年飙升至 **92.5%**（中位 1.99p，占正文 15.2%）。评审标准已从早期的“直觉合理即可进设计”全面转向“必须先用真实系统/生产 Trace 量化痛点与上界 headroom”。
   - 与此同时，**Related Work** 从中位 0.68p（613 词）压缩至 0.53p（426 词），**Conclusion** 从 0.21p（186 词）压缩至 **0.14p（121 词）**——现代顶会极度厌恶冗长的套话式总结。
4. **获奖范本的“坦诚边界感”**：`exemplar` 论文中 **32.3%** 设有独立 `Discussion/Limitations` 节、**16.1%** 设有显式 `Limitations` 标题（如 `Pathfinding Future PIM` HPCA 2024 的 `VI. SIMULATOR LIMITATIONS`、`PF-LLM` ASPLOS 2026 的 `7. Limitations`、`Autonomous NIC Offloads` ASPLOS 2021 的 `7 APPLICABILITY`），而在 `contrast_ordinary`（0/10）与 `contrast_post2023`（0/6）中显式 `Limitations` 标题的出现率均为 **0%**！

---

## 2. 章节排序变体与权衡取舍（Ordering Variants & Trade-offs）

**表 4：核心结构变体按时代、会议与层级的实证分布（N=150）**

| 维度分组 | RW 后置（Conclusion 前） | RW 前置（Sec 2/3 或 Bg&RW） | RW 融入/无独立节 | 拆分 Bg + Mot | 合并 Bg&Mot | 仅 Bg / 无显式 BgMot | 顶层 Overview 节 | `X.1` 首子节 Overview | 独立 Meth 节 | Disc/Lim 节 | 显式 Limitations 标题 | Artifact Appendix |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| **ALL (150)** | **76.7%** (115) | 10.7% (16) | 11.3% (17) | 18.7% (28) | 12.0% (18) | 62.7% (94) | 10.7% (16) | 15.3% (23) | 48.7% | 21.3% | 10.7% | 6.7% |
| **2011–2015 (45)** | 77.8% (35) | 13.3% (6) | 6.7% (3) | **13.3%** (6) | 8.9% (4) | 77.8% (35) | 13.3% (6) | **6.7%** (3) | 40.0% | 17.8% | **6.7%** | **0.0%** |
| **2016–2022 (65)** | 75.4% (49) | 10.8% (7) | 13.8% (9) | **9.2%** (6) | 12.3% (8) | 69.2% (45) | 9.2% (6) | 10.8% (7) | 47.7% | 20.0% | 9.2% | 4.6% |
| **2023–2026 (40)** | 77.5% (31) | 7.5% (3) | 12.5% (5) | **40.0%** (16) | 15.0% (6) | 35.0% (14) | 10.0% (4) | **32.5%** (13) | **60.0%** | **27.5%** | **17.5%** | **17.5%** |
| **ISCA (38)** | 78.9% | 7.9% | 7.9% | 15.8% | 13.2% | 65.8% | **21.1%** | 18.4% | 52.6% | **26.3%** | 13.2% | 7.9% |
| **MICRO (38)** | 76.3% | 10.5% | 13.2% | **26.3%** | 15.8% | 55.3% | 7.9% | **21.1%** | 42.1% | 21.1% | 10.5% | 5.3% |
| **HPCA (36)** | 69.4% | **16.7%** | 13.9% | 22.2% | 11.1% | 55.6% | **0.0%** | 19.4% | 52.8% | **11.1%** | **2.8%** | 0.0% |
| **ASPLOS (38)** | **81.6%** | 7.9% | 10.5% | 10.5% | 7.9% | 73.7% | 13.2% | 2.6% | 47.4% | **26.3%** | **15.8%** | **13.2%** |
| **`exemplar` (31)** | 74.2% (23) | 3.2% (1) | 16.1% (5) | 12.9% (4) | 19.4% (6) | 54.8% (17) | 9.7% (3) | 12.9% (4) | **58.1%** | **32.3%** | **16.1%** | 3.2% |
| **`contrast_ordinary` (10)** | 80.0% (8) | 10.0% (1) | 10.0% (1) | 20.0% (2) | 30.0% (3) | 50.0% (5) | 20.0% (2) | 0.0% (0) | 40.0% | 20.0% | **0.0%** | 0.0% |
| **`contrast_post2023` (6)** | 66.7% (4) | **33.3%** (2) | 0.0% (0) | **83.3%** (5) | 0.0% (0) | 16.7% (1) | 16.7% (1) | **50.0%** (3) | 50.0% | 16.7% | **0.0%** | 16.7% |

### 2.1 Related Work 放置策略：何时后置、何时前置、何时绝对不要中置？

1. **后置在 Evaluation 之后、Conclusion 之前（76.7% 主流铁律）**：
   - **原因**：体系结构论文的核心创新往往依赖具体的微架构术语（如 Range TLB、Speculative Buffer、Flex-DPE、zNUMA）。只有在读者看懂你的设计并信服你的评估后，才能精准理解你与前作的“本质结构差异”，而不是空洞的形容词对比。
   - **最佳切分实践（前轻后重、绝不重复）**：在 `RMM` (ISCA 2015, `conf__isca__KarakostasGACHM15`, p. 2) 中，Section 2 开篇第一句直接立下清晰分工：
     > `"This section and Table 1 overview the closely related approaches to reducing paging overheads and compare them to RMM. Section 9 discusses related work more generally."`
     同样，`Swarm` (MICRO 2015, `conf__micro__JeffreySYES15`, p. 11) 与 `Elastic Cuckoo Page Tables` (ASPLOS 2020, `conf__asplos__SkarlatosKXT20`, p. 14) 将末尾相关工作精准命名为 **`Other Related Work`** / **`Additional Related Work`**，避免把已在 Sec 2 对比过的直接竞争对手再复述一遍。
2. **前置或合并为 `Background & Related Work`（10.7%；HPCA 占 16.7%，`contrast_post2023` 占 33.3%）**：
   - **适用条件**：仅当你的工作建立在一个高度成熟、前人路线界限极其清晰的细分赛道（如 LLM 量化 `M-ANT` HPCA 2025、SRAM 纠错 `Duwe15` HPCA 2015），且必须借助前人分类树才能导出你的问题定义时。
   - **典型风险**：在 `PICACHU` (ASPLOS 2025, `conf__asplos__QinXT0Z25`, p. 3) 与 `M-ANT` (HPCA 2025, `conf__hpca__HuZ00GH00GL25`, p. 2) 中，将 Related Work 前置塞进 Section 2 后，读者还没见到作者的方案就被迫阅读长达 1–1.2 页的前人列表，导致直到第 4–5 页才看到核心设计，叙事拖沓。
3. **中置（Design 之后、Evaluation 之前，极罕见，全语料仅 2/150 = 1.3%）**：
   - 代表样本是 Mutlu 组的两篇获奖论文：`SALP` (ISCA 2012, `conf__isca__KimSLLM12`, p. 8 设 `7. Related Work`，后接 `8. Evaluation Methodology` 和 `9. Results`) 与 `Constable` (ISCA 2024, `conf__isca__BeraRRMNGOKSSM24`, p. 9 设 `7. Differences from Related Prior Works`，p. 13 又补一段 7 行的 `10. Other Related Works`)。
   - **批判性评估**：虽然出自顶组，但将 Related Work 夹在 Design 与 Evaluation 之间会打断“机制设计 → 实证兑现”的张力曲线；`Constable` 更因把相关工作一分为二导致 Section 10 萎缩成仅 7 行的孤立碎段。除非你是极其熟悉该套路的特定学派，否则**不建议模仿中置或分裂式 Related Work**。

### 2.2 `Background` 与 `Motivation` 的合并、拆分与“命题化命名”

数据揭示了一个高度值得警惕的现代趋势：`2023-2026` 时代“机械拆分 `2. Background` + `3. Motivation`”的比例飙升至 **40.0%**（在 6 篇 `contrast_post2023` 样本中更是高达 **83.3%，5/6**！如 `Hestia`, `M-ANT`, `PICACHU`, `FastTTS`, `QPlacer`），而顶级 `exemplar` 中这一比例仅为 **12.9%（4/31）**！

为什么顶刊/获奖纯人类作者很少死板地写出 `2. Background` + `3. Motivation` 的两件套？因为他们有**三种更紧绷、更有张力的组织法**：
1. **命题化取代泛称（最佳做法）**：不用空洞的 `Background`/`Motivation`，而是直接用**问题命题或实证主题**命名第 2 节：
   - `Whisper` (MICRO 2022 Best Paper, `conf__micro__KhanUNSLJK22`, p. 2): `II. BRANCH PREDICTION CHALLENGES FOR DATA CENTER APPLICATIONS`（2.6p 直接上 12 个生产应用实测！）
   - `SIGMA` (HPCA 2020 Best Paper, `conf__hpca__QinSKNS0KK20`, p. 2–3): `II. DL TRAINING CHARACTERIZATION` + `III. INEFFICIENCY OF GPUS AND TPUS`
   - `HFI` (ASPLOS 2023 Distinguished Paper, `conf__asplos__NarayanGTRM0FVL23`, p. 2): `2 LIMITATIONS OF SFI`（仅 1.0p，刀刀见血直切 SFI 软肋，零教科书废话！）
   - `Contiguitas` (ISCA 2023 Best Paper, `conf__isca__ZhaoXWSYMWRST023`, p. 3): `2 MEMORY CONTIGUITY CHALLENGES AND FRAGMENTATION AT SCALE`
   - `Pond` (ASPLOS 2023 Distinguished Paper, `conf__asplos__LiBHEZNSRLAHFB23`, p. 3): `2 BACKGROUND`（极简 0.3p 讲清 CXL.mem）→ `3 MEMORY STRANDING & WORKLOAD CHARACTERIZATION`（2.2p 放 Azure 100 集群生产数据）。
2. **紧凑合并式 `Background and Motivation`（19.4% `exemplar` 采用，中位 1.95p）**：当背景概念本身就是瓶颈的物理根源时合并最自然。例如 `Vector Runahead` (ISCA 2021, `conf__isca__NaithaniA0E21`, p. 2) 在 `II. BACKGROUND AND MOTIVATION` 中，用 3 个递进子节（`A. Memory Stalls in Out-of-Order Cores` → `B. Limitations of Runahead Techniques` → `C. Vector Runahead Execution for Dependent Loads`）在 2.2 页内丝滑完成从“问题”到“洞见”的起跳；`Row-Swap` (HPCA 2023 Best Paper, `conf__hpca__WooSN23`, p. 2) 则在 `II. BACKGROUND AND MOTIVATION` 中顺次安放 Threat Model、DRAM 组织、TRH 演化与 RRS 漏洞。
3. **高阶“去背景化”直接进题**：如果核心问题已在 1 页引言中讲透（如 `MorphCore` 的 OOO vs In-Order 权衡），只需极短的 1.3p 合并节，绝不把大学本科教材级别的常识（如 `M-ANT` p. 2 写出标准 Attention 矩阵公式、`QPlacer` p. 2 科普什么是 `|0⟩`/`|1⟩` 量子叠加态）硬凑成一整个 `Background` 节。

### 2.3 独立顶层 `Overview` 节 vs `Section 3.1 / 4.1 Overview` 首子节

- **顶层 `Overview` 节（全语料 10.7% 稳定存在）**：仅在系统包含**多套并列机制**或**横跨软硬件多个独立顶层节**时成立。例如 `SALP` (ISCA 2012, `conf__isca__KimSLLM12`, p. 5) 设有 `4. Overview of Proposed Mechanisms`（1.2p），先从概念上统一鸟瞰 SALP-1/SALP-2/MASA 三级阶梯，再进 `5. Implementation`（1.8p）展开电路与时序；`Graphicionado` (MICRO 2016 Best Paper, `conf__micro__HamWSSM16`, p. 3) 设 `III. GRAPHICIONADO OVERVIEW`（1.4p），再拆出 `IV. OPTIMIZATIONS` 与 `V. PARALLELISM`。
- **`X.1 Overview` 首子节（2011–2015 仅 6.7% → 2023–2026 飙升至 32.5%）**：现代顶会绝对主流的“先总后分”解法。它在不增加额外章节层级、不稀释核心设计节权重的条件下，用 0.5–0.8 页配一张全系统架构总图（System Overview Diagram）建立心智地图，如 `RMM` §3.1 Overview (`conf__isca__KarakostasGACHM15`, p. 3)、`Vector Runahead` §III-A Microarchitecture Overview (`conf__isca__NaithaniA0E21`, p. 4)、`Contiguitas` §3.1 Overview (`conf__isca__ZhaoXWSYMWRST023`, p. 5)、`Constable` §6.1 Design Overview (`conf__isca__BeraRRMNGOKSSM24`, p. 6)、`ρHammer` §4.1 Overview (`conf__micro__ChenTTLZQ25`, p. 6)。
- **避坑**：若一个系统本身只在单个设计节内展开，强行单列一个 0.5 页的顶层 `Overview` 节（如 `StreamBox-HBM` ASPLOS 2019 的 `3. Overview of StreamBox-HBM` 仅 0.5p，或 `Hestia` MICRO 2024 的 `IV. OVERVIEW` 0.8p）往往会造成内容碎片化，与前文 Intro 重复。

### 2.4 2020–2026 新兴章节的崛起：`Limitations`、`Security/Applicability` 与 `Artifact Appendix`

1. **显式 `Limitations` / `Applicability` / `Discussion` 的硬通货化**：显式 `Limitations` 标题比例从 `2011-2015` 的 **6.7%** 跃升至 `2023-2026` 的 **17.5%**；`Discussion/Limitations` 顶层节比例升至 **27.5%**。顶级范本绝不把 Limitations 写成“例行公事的自我吹捧”，而是做**外科手术式的边界划定**：
   - `Autonomous NIC Offloads` (ASPLOS 2021, `conf__asplos__PismennyEYL0T21`, p. 14) 在 `7 APPLICABILITY` 中直接划出哪些工作**不算**贡献：
     > `"Autonomously offloading this type of L5Ps is trivial and does not merit an academic publication (we indeed do not consider it part of our contribution)."`
   - `Pond` (ASPLOS 2023, `conf__asplos__LiBHEZNSRLAHFB23`, p. 12) 在 `7 DISCUSSION` 中直面 ML 预测对抗性滥用（`"Robustness of ML. Similar to other oversubscribed resources (CPU [76] and disks [13]), customers may overuse resources to get local memory."`）。
   - `Pathfinding Future PIM` (HPCA 2024 Best Paper, `conf__hpca__HyunKLR24`, p. 13) 专设 `VI. SIMULATOR LIMITATIONS`，坦承 uPIMulator 建模边界。
   - `PF-LLM` (ASPLOS 2026 Best Paper, `conf__asplos__XuSLBWLX026`, p. 11–12) 在 `7. Discussion` 之后紧跟 `Limitations`，诚实披露离线 LLM 分析对自修改代码/JIT 与动态输入漂移的约束。
2. **`Threat Model` + `Security Analysis` + `Responsible Disclosure` 制度化**：在安全类论文中，`Threat Model` 几乎 100% 前置于设计节之前（如 `InvisiSpec` §III、`Row-Swap` §II-A、`TimeCache` §4），`Security Analysis` 成为核心验证环节（`InvisiSpec` §VII、`Row-Swap` §IV-E、`HFI` §6.5），而面向真实商业硬件的攻击论文（如 `ρHammer` MICRO 2025, `conf__micro__ChenTTLZQ25`, p. 2）在引言末尾新增 **`Responsible Disclosure.`** 独立段落（披露向 Intel/MSI/Samsung PSIRT 报告的闭环）。
3. **`Artifact Appendix` 成为现代系统/架构顶会新标配**：从 `2011-2015` 的 **0%** 升至 `2023-2026` 的 **17.5%**（ASPLOS 达 **13.2%**，2026 样本达 **38%**），且统一放在正文之后（紧邻或晚于 References），内含标准化 `Abstract / Artifact Check-List / Description / Installation / Experiment Workflow`，如 `Autonomous NIC Offloads` (p. 14–15)、`Row-Swap` (p. 13–14)、`Hestia` (p. 13)、`FastTTS` (p. 16–17)。

---

## 3. 四大经典论文原型的叙事弧线（Four Canonical Narrative Arcs）

通过对 35+ 篇 `deep_read` 论文的逐节测绘，四大研究原型对应着四套截然不同的“说服拐点（Persuasive Turning Points）”与章节骨架：

### 3.1 原型 A：微架构 / 缓存 / 预取 / 内存机制类（Microarchitecture / Cache / Prefetch / Memory）

- **典型范本**：`SALP` (ISCA 2012)、`MorphCore` (MICRO 2012)、`Swarm` (MICRO 2015)、`Vector Runahead` (ISCA 2021)、`Whisper` (MICRO 2022)、`Constable` (ISCA 2024)、`PF-LLM` (ASPLOS 2026)。
- **标准章节弧线**：
  `Intro (~1.1p)` → `Background & Bottleneck / Headroom Characterization (~1.8–2.5p)` → `Key Insight & Mechanism Ladder / Microarchitecture Design (~3.5–4.5p)` → `[Optional: Cycle-Level Walkthrough Example & Storage/Power Overhead (~0.5–1.0p)]` → `Experimental Setup (~0.8p)` → `Evaluation: Overall + Breakdown + Sensitivity (~2.5–3.5p)` → `Related Work (~0.6p)` → `Conclusion (~0.15p)`
- **三大核心说服拐点**：
  1. **拐点 1 — 量化痛点与理想上界（Headroom / CPI-Stack Proof）**：在提出任何硬件改动之前，先用硬数据证明“基线还有多大空间，且现有 SOTA 为什么拿不到”。例如 `Vector Runahead` (`conf__isca__NaithaniA0E21`, p. 2) 用 Fig. 1 的 CPI 堆叠图证明：即便上了 SOTA 的 PRE，处理器仍有 **51.2%**（最高 76.5%）的时间停顿在间接依赖加载上；`Constable` (`conf__isca__BeraRRMNGOKSSM24`, p. 3–5) 专设 `4. Performance Headroom of Constable`（2.2p），实测证明 **34.2%** 动态 Load 为全局稳定加载，且消除资源依赖的理想收益（9.1%）是仅破除数据依赖的理想 LVP（4.3%）的 **2 倍以上**！
  2. **拐点 2 — 清晰机制阶梯或微型流水线走查（Mechanism Ladder / Walkthrough）**：顶组从不一次性抛出庞大硬件框图，而是构造递增阶梯或逐周期指令走查。`SALP` (`conf__isca__KimSLLM12`, p. 5–7) 构造了经典的零硬件改动 `SALP-1` → 加锁存器 `SALP-2` → 多子阵激活 `MASA` 三级阶梯；`Vector Runahead` (`conf__isca__NaithaniA0E21`, p. 8) 甚至单独设立 `IV. REPRESENTATIVE CODE EXAMPLE`（0.5p），带读者逐条跟踪 28 行 x86 汇编如何被向量化；`Constable` (§6.8 `An Illustrative Example`, p. 8–9) 与 `MorphCore` (§4 `MorphCore Discussion`, p. 6–7) 均在设计末尾主动拆解最棘手的正确性边界（访存乱序消歧、多核一致性、模式切换代价）。
  3. **拐点 3 — 严格开销核算 + 因果归因评估**：微架构评审极看重硬件开销（字节数、关键路径周期、功耗面积）与“收益为何发生”的机理归因（而不只给 speedup 柱状图）。如 `Vector Runahead` 强调仅增 `1.3 KB` 状态并展示 MLP 与缓存覆盖率变化；`Constable` 在 §8.5 跑了 **3,400 条 trace 的逐指令功能等价性验证**，在 §9.4–9.5 将 3.4% 功耗下降精准归因到 RS 分配减少 8.8% 与 L1-D 访问减少 26%。

### 3.2 原型 B：软硬件协同 / 虚拟内存 / OS-架构 / CXL 系统类（SW-HW Co-design / VM / OS-Arch / CXL）

- **典型范本**：`RMM` (ISCA 2015)、`FireSim` (ISCA 2018)、`Elastic Cuckoo Page Tables` (ASPLOS 2020)、`Autonomous NIC Offloads` (ASPLOS 2021)、`Contiguitas` (ISCA 2023)、`Pond` (ASPLOS 2023)。
- **标准章节弧线**：
  `Intro (~1.2–1.8p)` → `Brief Background + Production/Fleet Characterization (~2.0–2.5p)` → `Design Split: Hardware Substrate + OS/Software/ML Control Plane (~3.5–4.5p)` → `Implementation / Kernel Integration / Emulation Validation (~0.8–1.5p)` → `End-to-End Evaluation (Real System + Simulation) (~2.5–4.5p)` → `Discussion / Applicability (~0.6–0.8p)` → `Related Work (~0.6p)` → `Conclusion (~0.15p)`
- **三大核心说服拐点**：
  1. **拐点 1 — 打破跨层“死锁假设”的生产级证据**：SW-HW 论文的核心说服力来自揭示“纯硬件做不到、纯软件代价太高”的跨层错配。`Pond` (`conf__asplos__LiBHEZNSRLAHFB23`, p. 3–5) 在 §3 用 Azure 100 个生产集群的实测抛出两个颠覆性事实——高达 **25%** DRAM 搁浅（stranding）且 **~50%** VM 触碰不足一半内存，但 8–16 Socket 的小池即可吃掉绝大部分收益；`Contiguitas` (`conf__isca__ZhaoXWSYMWRST023`, p. 3–5) 用 Meta 机群实测打破“只有老机器才碎片化”的迷思（开机 1 小时即严重碎片化，23% 服务器连一个 2MB 大页都分不出来，73% 不可移动页来自网络缓冲）。
  2. **拐点 2 — 清晰划定“硬件边界 vs 软件策略”的职责切分**：顶尖 SW-HW 论文在章节结构上就把两层拆得泾渭分明：`RMM` (`conf__isca__KarakostasGACHM15`) 严格分为 `4. Architectural Support`（Range TLB/Table，1.8p）与 `5. Operating System Support`（Eager Paging，1.4p）；`Pond` 将 §4 `POND DESIGN` 明确切为 `4.1 Hardware Layer`（CXL 拓扑与延迟）与 `4.2 System Software Layer`（zNUMA + 预测 ML 模型 + QoS 兜底迁移）；`Autonomous NIC Offloads` (`conf__asplos__PismennyEYL0T21`) 先在 §3 提炼可自主卸载的协议抽象性质，再在 §4 给出通用软硬接口、§5 落地 Linux 内核与 ConnectX ASIC 的 NVMe-TCP 与 TLS 双实现。
  3. **拐点 3 — “真实内核/生产实测 + 硬件仿真”双轨交叉验证**：因为新硬件尚未流片或刚起步，顶尖范本必须解决“如何同时证明软件可部署且硬件模型可信”。`Contiguitas` 在 Meta 真实生产环境实测 OS 部分（Web 等 3 大服务提升 2–9% / 7–18%），用全系统仿真测 LLC 迁移扩展；`HFI` (`conf__asplos__NarayanGTRM0FVL23`, p. 2, 9–10) 与 `Pond` 均采用“先用 gem5 / 硬件实测校准仿真/模拟层，再用模拟层跑大规模真实应用（Firefox / NGINX / 158 个云工作负载）”的闭环。

### 3.3 原型 C：加速器 / ML / GPU 架构类（Accelerators / ML / GPU Architecture）

- **典型范本**：`DaDianNao` (MICRO 2014)、`Eyeriss` (ISCA 2016)、`Graphicionado` (MICRO 2016)、`Darwin` (ASPLOS 2018)、`SIGMA` (HPCA 2020)、`DynamoLLM` (HPCA 2025)、`LLM.265` (MICRO 2025)。
- **标准章节弧线**：
  `Intro (~0.8–1.5p)` → `Workload / Kernel / Dataflow Characterization & Baseline Inefficiency (~2.0–3.5p)` → `Algorithm / Dataflow Co-design (~1.5–2.0p)` → `Accelerator Microarchitecture & NoC/Memory Hierarchy (~2.5–3.5p)` → `Physical Implementation (RTL Synthesis / P&R Area & Power) (~0.8–1.2p)` → `Evaluation (Iso-Area / Iso-Power / Accuracy-Speedup Trade-off) (~2.0–3.0p)` → `Related Work (~0.5–0.9p)` → `Conclusion (~0.15–0.4p)`
- **三大核心说服拐点**：
  1. **拐点 1 — 从算法特征直推“数据搬运/利用率瓶颈”**：加速器论文若只讲“模型很大所以要加速”必然被拒；范本必在前半段精准定位计算与访存的失配点。`Eyeriss` (`conf__isca__ChenES16`, p. 2–5) 用 3 个紧凑节（`II. Spatial Architecture` → `III. CNN Background` → `IV. Existing CNN Dataflows`）建立“四级存储能耗账本”，直接导出 Row-Stationary 数据流的必然性；`SIGMA` (`conf__hpca__QinSKNS0KK20`, p. 2–5) 先在 §II 量化训练中 GEMM 占 70% 且稀疏度 10%–90% 动态剧变，再在 §III 剖析 V100 Tensor Core 与 TPU 128×128 脉动阵列的刚性利用率崩塌；`DynamoLLM` (`conf__hpca__StojkovicZGTC25`, p. 2–3) 在 §III 用 Table I 的 9 桶（SS 到 LL）× TP2/4/8 × GPU 频率能耗热力图，一眼展示出异构重配的巨额节能空间。
  2. **拐点 2 — “算法/数据流 + 硬件微架构”协同闭环**：`Darwin` (`conf__asplos__TurakhiaBD18`, p. 2) 严格遵循“先算法后硬件”的镜像章节：`3. D-SOFT Filtering Algorithm` + `4. GACT Alignment Algorithm` → `5. System Integration` → `6. D-SOFT Hardware` + `7. GACT Hardware`；`LLM.265` (`conf__micro__XuW0CLZW25`, p. 4–11) 则采用极富探索张力的“现象揭示 → 复用现成 GPU 硬件编解码器（NVENC/NVDEC）实证 → 剖析现成硬件局限 → 定制低成本三合一张量编解码器”四阶递进弧线。
  3. **拐点 3 — 物理后端落盘（Synthesis / Place-and-Route）与同面积/同精度公平对比**：顶级加速器范本绝不只给周期级仿真数字，而必给 28nm/40nm/65nm/ASAP-7 的 RTL 综合或布局布线（P&R）面积与功耗（如 `DaDianNao` 28nm 67.73 mm²/节点、`Eyeriss` 65nm 流片验证、`Darwin` TSMC 40nm P&R 412 mm²/15W、`SIGMA` 28nm 65.10 mm²/22.33W、`LLM.265` ASAP-7 P&R 并在固定 50,000 mm² 芯片总面积预算下画 Pareto 前沿）。

### 3.4 原型 D：安全攻防与实证表征/测量类（Security / Characterization / Measurement）

该原型内部存在两个截然不同但同样高频的子弧线：

#### 子型 D1：硬件安全攻防类（`RowHammer` ISCA14、`InvisiSpec` MICRO18、`Row-Swap` HPCA23、`HFI` ASPLOS23、`ρHammer` MICRO25）
- **标准章节弧线**：
  `Intro (~1.0–1.3p)` → `Background & Formal Threat Model (~1.0–2.0p)` → `[Attack Discovery / Root Cause / Breaking SOTA (~1.5–2.5p)]` → `Defense Architecture & Microarchitecture (~3.0–4.5p)` → `Security Analysis (Systematic Proof / PoC Verification) (~0.8–1.5p)` → `Performance/Storage/Power Evaluation (~1.5–2.5p)` → `Discussion + Related Work + Conclusion (~1.2p)`
- **关键拐点**：
  - **“破立一体”双幕剧最出彩**：`Row-Swap` (`conf__hpca__WooSN23`, p. 4–9) 先在 §III 构造 `Juggernaut` 攻击在 **<1 天**内击穿 SOTA 防御 RRS（利用 RRS 自身的 swap/unswap 动作反向增加激活次数），再在 §IV 推出 `SRS` 封堵漏洞、§V 推出 `Scale-SRS` 降开销，形成“破 SOTA → 补安全 → 降开销”的三连击；`RowHammer` (`conf__isca__KimDKFLLWLM14`) 则是“真实商用芯片大规模实证翻位（110/129 条 DIMM）→ 物理根因（wordline 耦合漏电）→ FPGA 全面表征 → 对比 6 种朴素方案后推出无状态低开销第 7 方案 PARA”。
  - **Threat Model 与 Security Analysis 必须成对闭环**：如 `InvisiSpec` (`conf__micro__YanCS0FT18`) 在 §III 严格定义保护信道与排除信道（显式声明 NoC/DRAM 留作未来工作），再在 §VII `SECURITY ANALYSIS` 中逐一对应证明防御成立，并在 Appendix 给出 TSO 内存一致性数学证明。

#### 子型 D2：体系结构表征与测量类（`Clearing the Clouds` ASPLOS12、`Chasing Carbon` HPCA21、`Pathfinding Future PIM` HPCA24）
- **标准章节弧线（无传统单点“Design”节！）**：
  `Intro (~1.0–1.5p)` → `Domain Context / Accounting or Platform Primer (~1.5–2.3p)` → `Measurement Methodology / Validated Tooling (~1.5–2.1p)` → `Multi-Axis Empirical Findings (3–4 个独立剖析节，占 4.5–6.5p)` → `Design Implications / Pathfinding Future Architectures (~0.5–5.2p)` → `Limitations & Related Work & Conclusion (~1.0p)`
- **关键拐点**：
  - 表征论文最大的死穴是沦为“无聊的柱状图流水账”。顶级范本靠**“颠覆常识的中心论点 + 每节强制输出 Architectural Implication”**撑起叙事张力：
    - `Clearing the Clouds` (`conf__asplos__FerdmanAKVAJKPAF12`, p. 5–9) 的 §4 按微架构子系统切为 4 块（Frontend / Core / Data-access / Bandwidth），每块末尾均以加粗 **`Implications`** 段落给出面向未来服务器芯片的直接重构处方；
    - `Chasing Carbon` (`conf__hpca__GuptaKLTLW0W21`, p. 2–11) 以“碳排放重心正从 Opex 转向 Capex/制造”为单一红线，贯穿个人设备（§III）、数据中心（§IV）、半导体制造（§V），最后在 §VI 按软件/编译器/体系结构/电路四层绘制减碳路线图；
    - `Pathfinding Future PIM` (`conf__hpca__HyunKLR24`, p. 2–13) 更是把“商业 UPMEM-PIM 硬件解构（§II）→ 跨验证开源模拟器 uPIMulator（§III）→ 实证表征（§IV）→ 面向未来 PIM 架构的探索性硬件改进评估（§V，高达 5.2p！）”融为一体，把测量论文升维为“实证驱动的架构探路”。

---

## 4. 跨节契约（Cross-Section Contracts）与违约诊断

顶会论文是一份严格的**逻辑履约合同**：Title 提出核心预期 → Abstract 压缩全貌 → Intro 给出具体承诺清单（Contributions）→ Motivation 证伪现有基线并量化空间 → Design 逐一兑现每个机制部件 → Evaluation 用实测验证每一项核心宣称 → Conclusion 精准回收且不新增承诺。

### 4.1 顶级范本的“严丝合缝履约”示范

1. **显式章节回链契约**：`Constable` (`conf__isca__BeraRRMNGOKSSM24`, p. 2) 的贡献列表每一条末尾都标明履约章节号（`see §4.1`、`§4.4`、`§5`、`§6`、`§8.5`、`§9.1.1`、`§9.5`、`§4.2`）；`Eyeriss` (`conf__isca__ChenES16`, p. 2) 的 4 条贡献分别一一对应 `(Section IV)`、`(Section V)`、`(Section VI-C)`、`(Section VII)`；`Pond` (`conf__asplos__LiBHEZNSRLAHFB23`, p. 2–12) 甚至在每一张图注里标注归属章节（`Figure 1: CXL Request Flow (§2)`、`Figure 2: Memory stranding (§3.1)`），并在评估节中用编号 **`Finding #1`–`Finding #10` + `Implication.`** 逐条回收引言提出的 4 个洞见。
2. **摘要—引言—正文“信息分层不复读”契约**：`Contiguitas` (`conf__isca__ZhaoXWSYMWRST023`, p. 1–3) 是极佳范本——Abstract 只给最高层结论（不可移动 2MB 块从 31% 降至 7%，生产服务提速 2–9% / 7–18%）；Intro §1.1 进一步释放机群诊断细节（23% 服务器无单块 2MB 连续页，73% 不可移动页来自网络缓冲，并解锁 Meta Web 服务 1GB 大页带来 7.5% 增益）；Section 2–5 再逐步展开完整曲线与硬件细节。每一层都比上一层多提供增量信息，绝不机械复制。
3. **结论的“零新宣称”克制契约**：`RMM` (`conf__isca__KarakostasGACHM15`, p. 12 `10. Summary`, 88 词)、`PVCoherence` (`conf__hpca__ZhangBES14`, p. 12 `8. Conclusions`, 59 词)、`Pond` (`conf__asplos__LiBHEZNSRLAHFB23`, p. 13 `9 CONCLUSION`, 107 词) 均在一小段内精准回收最初目标与核心数字，不引入任何正文未验证的新口号。

### 4.2 常见“跨节违约”反模式（普通人类论文与后 2023 AI 污染论文实录）

| 违约类型 | 真实反面案例与精准定位 | 具体症状与危害 |
|---|---|---|
| **1. 摘要—引言定量契约断裂** | `Hestia` (MICRO 2024, `contrast_post2023`, `conf__micro__XuLZLW0024`, p. 1–2) | Abstract 只写空洞定性句 `"achieves significant simulation speedup"`、`"helps find and localize bugs easily"`（零数字！），而翻到第 2 页 Intro 末尾却突然放出 `174.18×`、`18.51×`、`8.92×` 三组实测加速比。审稿人读完摘要以为没有硬核数据。 |
| **2. 章节位置错乱 / 提前剧透** | `Turnpike` (MICRO 2021, `contrast_ordinary`, `conf__micro__ZengKLJ21`, p. 4, 8) | 把 `5 DISCUSSION` 放在 `6 IMPLEMENTATION AND EVALUATION` 之前（还没看实验数据就开始讨论边界与延伸），且设计主节标题竟写作口语化的 `"4 TURNPIKE FOR SOLVING THE PROBLEMS"`。 |
| **3. 章节命名违背领域惯例** | `PICACHU` (ASPLOS 2025, `contrast_post2023`, `conf__asplos__QinXT0Z25`, p. 4–8) | 将长达 3.26 页的 CGRA 硬件架构与 MLIR 编译器设计主节命名为 **`4 Methodology`**（受 ML 顶会习惯污染）。在体系结构四大顶会中，`Methodology` 默认指代 `Experimental/Simulation Methodology`（实验方法学），误用会直接打乱审稿人的心智预期。 |
| **4. 摘要/引言/贡献/结论“四连复读”** | `FastTTS` (ASPLOS 2026, `contrast_post2023`, `conf__asplos__ChenML0MLF26`, p. 1, 2, 13) | 同一套“三挑战 ↔ 三协同优化（Speculative Beam Extension, Dynamic Prefix-Aware Scheduling, Asymmetric Multi-Model Memory Allocation）”+ 宏大口号 `"democratizing agentic AI"` 在 Abstract、Intro 正文、Intro 贡献列表、Conclusion 中**四次高度雷同地复读**，挤占了本应用于阐释机制权衡的宝贵篇幅。 |
| **5. 标题/正文系统名契约失守** | `Turnpike` (MICRO 2021, `conf__micro__ZengKLJ21`, p. 1) & `TimeCache` (ISCA 2021, `conf__isca__OjhaD21`, p. 1) | 两篇 `contrast_ordinary` 论文在 arXiv/PDF 首页标题均隐去了系统名（分别写作 `"Lightweight Soft Error Resilience for In-Order Cores"` 与 `"Timing Cache Accesses to Eliminate Side Channels in Shared Software"`），而正式会议/摘要中却高频使用 `Turnpike` 与 `TimeCache`，导致读者首屏建立不起命名锚点。 |
| **6. 过早泄露未兑现或夸大的抽象宣称** | `QPlacer` (ISCA 2025, `contrast_post2023`, `conf__isca__Zhang0D0AO0B0025`, p. 2, 11) | Intro 用宏大 AI 辞藻宣称 `"This initiative marks a pivotal advancement in quantum chip design, harmonizing the delicate balance..."`，Conclusion 又突然发散承诺可缓解正文并未评估的 `"decoherence"` 问题，形成典型的“孤儿宣称（orphaned claim）”。 |

---

## 5. 15 年结构演进总结、获奖论文批判性审计与 Phase 2 可执行规则

### 5.1 15 年宏观结构演进脉络（2011 → 2026）

1. **纸面总长扩张但正文守恒**：总页数 12.0p → 15.0p（+25%），但正文仅 11.3p → 12.4p（+9.7%）；真正膨胀的是 References（0.9p → 2.5p）与 Artifact Appendix（0% → 17.5%，2026 达 38%）。
2. **前置实证化**：显式背景/动机块覆盖率从 57.8% 跃升至 92.5%，但 2023–2026 年出现过度套路化的 `2. Background` + `3. Motivation` 机械二分（40.0%，`contrast_post2023` 达 83.3%），挤压核心设计篇幅。
3. **设计节内部导航精细化**：`X.1 Overview` 首子节从 6.7% 暴增至 32.5%，成为大型系统的标配入口；同时独立 `Methodology` 节从 40.0% 稳步增至 60.0%。
4. **“诚实边界”上升为顶会加分项**：`Discussion/Limitations` 从 17.8% 升至 27.5%，显式 `Limitations` 标题从 6.7% 升至 17.5%。
5. **尾部彻底去水化**：引言末尾传统论文结构导读段（`"The rest of this paper is organized as follows..."`）近乎消亡（43.2% → 7.5%，2025–2026 为 **0%**，详见维度二报告），Conclusion 压缩至仅 0.14 页（约 120 词）。

### 5.2 批判性审计：即使是 Best Paper / Top Picks 也不应照抄的 6 类结构瑕疵

“不要认为只要是获奖论文，其每一个结构决策都值得学习。”精读 32 篇 `exemplar` 后，我们明确标出以下 **6 类必须剔除的获奖论文特例/瑕疵**：

1. **不要照抄 `Constable` (ISCA 2024 Best Paper, `conf__isca__BeraRRMNGOKSSM24`, p. 2, 9, 13) 的“7 条超长贡献 + 分裂式 Related Work + 三次数字复读”**：该文凭硬核微架构与 3,400 条 trace 严格验证拿奖，但其 Intro 列出多达 7 条占近半页的贡献清单，将 5.1%/3.4%/12.4KB 在前两页重复三次，且把相关工作拆成 Eval 前的 `7. Differences from Related Prior Works` 和 Eval 后仅 7 行的 `10. Other Related Works`——结构臃肿且割裂。
2. **不要照抄 `Elastic Cuckoo Page Tables` (ASPLOS 2020 Best Paper, `conf__asplos__SkarlatosKXT20`, p. 1–2) 的“Abstract 末段整段粘贴进 Intro 末段”**：该文 Abstract 末三句与 Intro 末三句几乎一字不差（仅把 `using a set` 改为 `running a set`）。顶级作者赶截止日期时的偷懒习惯不应成为写作规范。
3. **不要照抄 `SALP` (ISCA 2012 Top Picks, `conf__isca__KimSLLM12`, p. 1, 8) 的“摘要漏报核心性能数字 + Related Work 中置”**：该文 Abstract 只写了 `< 0.15%` 面积开销，对性能仅模糊称 `"significantly improve performance"`（把 `7%/13%/17%` 留到了 p. 2 贡献清单）；且把 `7. Related Work` 插在 `6. Overhead` 与 `8. Methodology` 之间，打断了从设计到实验的阅读连贯性。
4. **不要照抄 `FireSim` (ISCA 2018 Top Picks, `conf__isca__KarandikarMKBAL18`, p. 1–3) 的“140 词机械导读段 + p. 3 才出首图 + 67 词超长摘要尾句”**：作为影响力巨大的开源工具，它凭借工程震撼力入选 Top Picks，但其 Intro 缺少凝练贡献清单、用长达 140 词的 `"Section II describes... Finally, Section VIII outlines..."` 收尾，且到第 3 页才出现第一张图。
5. **不要照抄 `DynamoLLM` (HPCA 2025 Best Paper, `conf__hpca__StojkovicZGTC25`, p. 1) 与 `LLM.265` (MICRO 2025 Best Paper, `conf__micro__XuW0CLZW25`, p. 1) 的“后 2023 LLM 润色开篇”**：即便在 2025 年获奖论文中，也已出现明显的 AI 腔开篇渗透（如 `DynamoLLM` 首页密集堆砌 `pivotal`、`exponential growth in the adoption`、`paramount`、`underscores`、`pave the way towards`；`LLM.265` 引言首句写 `"showcasing remarkable proficiency in various applications, such as virtual assistants [60], chatbots [60], and automated customer service platforms [63]."`）。应学它们的实证深度与设计巧思，**严禁效仿其 AI 味开篇**。
6. **不要照抄 `PF-LLM` (ASPLOS 2026 Best Paper, `conf__asplos__XuSLBWLX026`, p. 1–3) 的“摘要过度宣称 + 优先权充数贡献”**：该文核心问题设计极佳，但在 Abstract 宣称 `"turns the on-chip prefetcher into a zero-latency, oracle-level system that always follows the best prefetching policy for every single load instruction"` 明显言过其实（实测并非 oracle，对所有 load 均最优也不成立），且第 4 条贡献以 `"To our knowledge, this is the first work..."` 充数而非实质技术交付。

---

### 5.3 Phase 2 写作技能（Skill）可直接落地的 10 条宏观结构硬规则

1. **【R1-正文预算锚点】** 目标正文（Sec 1 至 Conclusion）严格控制在 **11.5–12.5 页（~9,500–10,500 词）**，遵守 **40–25–20–15 分配律**：核心设计与实现 **38%–45%（4.5–5.5p）**，实验方法与评估 **25%–30%（3.0–3.5p）**，引言+背景/动机 **18%–24%（Intro 1.0–1.5p，Bg+Mot ≤2.0p）**，讨论/相关工作/结论 **8%–12%**。
2. **【R2-会议自适应微调】** 投 **MICRO** 时将 Intro 压在 1.0p 内、把设计节扩至 42%–45% 并强化微架构细节与周期级走查；投 **ASPLOS** 时给足跨层动机、真实系统原型与 Artifact Appendix；投 **ISCA/HPCA** 时确保独立 `Methodology` 节与清晰的对比基线表。
3. **【R3-按原型选弧线】** 动笔前先锁定四类原型之一：（a）微架构机制类必须包含**量化 headroom 节 + 机制阶梯/走查 + 精确硬件开销**；（b）SW-HW 系统类必须**物理分离硬件层与 OS/软件层**并尽量采用双轨验证；（c）加速器类必须含 **数据流/能耗账本 + RTL/综合面积功耗 + 同面积/同精度公平对比**；（d）安全类必配 **前置 Threat Model + 后置 Security Analysis**，表征测量类必在每节评估后输出显式 **Architectural Implications**。
4. **【R4-拒绝机械 `Background` + `Motivation` 教科书两件套】** 禁止在 Section 2 科普本领域常识公式或本科生概念；优先采用**命题化 Section 2 标题**（如 `Limitations of X`、`Memory Contiguity Challenges at Scale`、`Workload Characterization`）或紧凑合并式 `Background and Motivation`（总长严格 ≤ 2.0 页，除非是生产级大规模表征研究）。
5. **【R5-Overview 优先下沉为 `X.1` 首子节】** 默认使用 `Section 3.1 / 4.1 Overview`（0.5–0.8p + 全系统总图）引导复杂设计；仅当提出多个并列机制或设计横跨 2 个以上顶层章节时，才设独立顶层 `Overview` 节。
6. **【R6-设计主节严禁命名为 `Methodology`】** 在体系结构顶会中，`Methodology` 专指实验仿真与评估方法学（约 0.8–1.0p）；核心方案节必须以系统名或具体架构机制命名（如 `SIGMA Architecture`、`Elastic Cuckoo Page Table Design`、`Pond Design`）。
7. **【R7-Related Work 默认后置且严控 0.5–0.8 页】** 将 `Related Work` 放在 `Evaluation` 之后、`Conclusion` 之前；若在 Sec 2 已与直接竞争基线作对比，末尾标题明确写作 `Other Related Work` 或在 Sec 2 首段声明分工，杜绝前后重复。
8. **【R8-强制设置 `Discussion / Limitations` 边界讨论】** 用 0.4–0.7 页坦诚界定方法适用边界、负面场景、工程部署假设或安全/一致性边界（如 `Applicability`、`Limitations`）；绝不以空洞展望敷衍，也不留给审稿人自行挑刺。
9. **【R9-Conclusion 极限克制（0.15–0.20 页，120–180 词）】** 单段收束，仅回扣最初的核心瓶颈、关键机制与 1–2 个已被正文证实的头条结果；**严禁引入正文未验证的新宣称或宏大 AI 愿景口号**（如 `"democratizing..."`、`"paving the way..."`）。
10. **【R10-全链路跨节契约核验】** 完稿前执行四项一对一核验：（a）Abstract 中的每个核心量化宣称均在 Intro 展开、在 Evaluation 中有对应图表支撑；（b）Intro 中每一条 Contribution 都能映射到具体章节号且不越界；（c）Intro 与 Abstract **绝不整句/整段复制粘贴**；（d）系统命名在 Title、Abstract、Intro、设计节标题与图注中 100% 锁定一致。

# Gold Human Excerpts (Annotated Top-Venue Prose)

Twelve verbatim excerpts from clean, pre-LLM top-venue computer architecture papers spanning Abstract, Introduction, Motivation/Background, Design, Evaluation, Related Work, and Conclusion. Study the **sentence-role progressions (`S1 -> S2 -> ...`)**, **Given-New subject chaining**, **word-count contours**, and **concrete hardware verbs**—not surface decoration.

---

## 1. Abstract — Short-Pivot Reframing (`SK-4`)
**Source**: *Vector Runahead* (ISCA 2021, p. 1)

> The memory wall places a significant limit on performance for many modern workloads. These applications feature complex chains of dependent, indirect memory accesses, which cannot be picked up by even the most advanced microarchitectural prefetchers. The result is that current out-of-order superscalar processors spend the majority of their time stalled. While it is possible to build special-purpose architectures to exploit the fundamental memory-level parallelism, a microarchitectural technique to automatically improve their performance in conventional processors has remained elusive. Runahead execution is a tempting proposition for hiding latency in program execution. However, to achieve high memory-level parallelism, a standard runahead execution skips ahead of cache misses. In modern workloads, this means it only prefetches the first cache-missing load in each dependent chain. We argue that this is not a fundamental limitation.

- **Progression & Given-New Chain** (`[13, 22, 15, 28, 12, 15, 16, 9]`):
  - `S1 (13w)` `[Claim]`: Introduces `memory wall` -> `modern workloads`.
  - `S2 (22w)` `[Mechanism]`: Lead-2 `These applications` chains S1's `workloads` -> `dependent, indirect memory accesses` defeating prefetchers.
  - `S3 (15w)` `[Consequence]`: `The result` -> `out-of-order superscalar processors spend the majority of their time stalled`.
  - `S4 (28w)` `[Boundary]`: Separates special-purpose hardware from conventional microarchitectural techniques.
  - `S5 (12w)` `[Elimination setup]`: Introduces `Runahead execution` as a tempting latency-hiding candidate.
  - `S6 (15w)` `[Contrast Pivot + Mechanism]`: `However,` chains `standard runahead execution` -> `skips ahead of cache misses`.
  - `S7 (16w)` `[Consequence]`: `this means` pins down the workload impact -> `only prefetches the first cache-missing load in each dependent chain`.
  - `S8 (9w)` `[Contrast Pivot]`: **9-word dagger** (`We argue that this is not a fundamental limitation.`) resets tension and sets up the core contribution.
- **Craft Takeaway**: Zero macro throat-clearing; concrete pipeline verbs (`stalled`, `skips ahead`, `prefetches`); sharp `9w` pivot breaking medium-length setup sentences.

---

## 2. Abstract — Empirical Discovery & Understated Authority (`SK-2`)
**Source**: *RowHammer* (ISCA 2014, p. 1)

> Memory isolation is a key property of a reliable and secure computing system — an access to one memory address should not have unintended side effects on data stored in other addresses. However, as DRAM process technology scales down to smaller dimensions, it becomes more difficult to prevent DRAM cells from electrically interacting with each other. In this paper, we expose the vulnerability of commodity DRAM chips to disturbance errors. By reading from the same address in DRAM, we show that it is possible to corrupt data in nearby addresses. More specifically, activating the same row in DRAM corrupts data in nearby rows. We demonstrate this phenomenon on Intel and AMD systems using a malicious program that generates many DRAM accesses. We induce errors in most DRAM modules (110 out of 129) from three major DRAM manufacturers. From this we conclude that many deployed systems are likely to be at risk. We identify the root cause of disturbance errors as the repeated toggling of a DRAM row's wordline, which stresses inter-cell coupling effects that accelerate charge leakage from nearby rows.

- **Progression & Given-New Chain** (`[32, 24, 14, 20, 13, 18, 16, 14, 29]`):
  - `S1 (32w)` `[Claim]`: Defines `Memory isolation` via an authentic em-dash invariant.
  - `S2 (24w)` `[Contrast Pivot + Physical Cause]`: `However,` links technology scaling -> electrical cell interaction.
  - `S3 (14w)` `[Claim]`: Active verb `expose` names `disturbance errors`.
  - `S4 (20w)` -> `S5 (13w)` `[Mechanism Zoom-in]`: Narrows from `reading from the same address` to `activating the same row`.
  - `S6 (18w)` -> `S7 (16w)` `[Quantitative Anchor]`: Names real platforms (`Intel and AMD`) and stark empirical scale (`110 out of 129` modules, `three major DRAM manufacturers`).
  - `S8 (14w)` `[Boundary / Restraint]`: Understated conclusion (`likely to be at risk`) despite overwhelming error rates—zero hype.
  - `S9 (29w)` `[Physical Cause]`: Closes on circuit physics (`repeated toggling of a DRAM row's wordline` -> `inter-cell coupling` -> `accelerate charge leakage`).
- **Craft Takeaway**: The more dramatic the empirical finding, the calmer the prose. Concrete physical verbs (`expose`, `corrupt`, `induce`, `toggling`, `accelerate`) carry the authority.

---

## 3. Introduction — Authentic Em-Dashes & Architectural Causality (`SK-2`)
**Source**: *Clearing the Clouds* (ASPLOS 2012, p. 2)

> The "memory wall"—the gap between the speed at which cores could compute and the speed at which data could be delivered to the cores for computation—mandated that the data working set must fit into the on-chip caches to allow the core to compute at full speed. Modern processors therefore split the die area into two roughly equal parts, with one part dedicated to the cores and tightly-coupled private caches and the other dedicated to a large shared last-level cache. The emergence of multi-core processors offered the possibility to run computationally-intensive multithreaded applications, adding the requirement of fast and high-bandwidth core-to-core communication to allow cores to compute without incurring significant delays when operating on actively shared data. To leverage the increasing number of transistors on chip for higher single-thread performance, cores are engineered to execute independent instructions out of order (OoO), allowing the processor to temporarily bypass instructions that stall due to a cache access.

- **Progression & Given-New Chain** (`[46, 33, 37, 38]`):
  - `S1 (46w)` `[Physical Cause]`: Uses paired em-dashes (`—...—`) to define `"memory wall"` inline between subject and verb, establishing the working-set constraint.
  - `S2 (33w)` `[Consequence]`: Mid-clause `therefore` derives silicon area partitioning (`two roughly equal parts` — plain human quantifier `roughly`).
  - `S3 (37w)` `[Next-Step State]`: Shifts to multi-core processors -> inter-core communication requirement (`without incurring significant delays`).
  - `S4 (38w)` `[Mechanism]`: Connects transistor budget -> out-of-order execution (`bypass instructions that stall due to a cache access`).
- **Craft Takeaway**: Demonstrates that paired em-dashes and occasional 35–46 word causal sentences are native senior-architect style when every clause carries concrete microarchitectural meaning (zero participle fluff).

---

## 4. Introduction — Given-New Chaining & Parallel Mechanisms (`SK-3` -> `SK-1`)
**Source**: *Amdahl's Law Market* (HPCA 2018, p. 1)

> Systems determine users' shares with one of three mechanisms. With reservations, users request and pay for resources. Allocations depend on users' requests but are inefficient when requests are over-sized and resources are under-utilized [4], [5]. With priorities, allocations depend on users' computation and relative importance, exposing users to interference and non-deterministic performance [6], [2]. Finally, with entitlements, each user is guaranteed a minimum allocation and under-utilized resources are redistributed [6], [1], [7], [3]. Entitlements, unlike alternatives, provide isolation and efficiency. Entitlements for datacenters differ from those for a server. Within a server, proportional share schedulers allocate divisible resources [6], [7]. In theory, the datacenter provides a similar abstraction—a warehouse-scale machine with logically divisible resources. In practice, however, resources are physically distributed across servers in ways that constrain allocation.

- **Progression & Given-New Chain** (`[9, 8, 18, 19, 19, 7, 9, 11, 14, 14]`):
  - `S1 (9w)` `[Claim / Split-Topic Announcement]`: Announces exact branch count (`one of three mechanisms`).
  - `S2 (8w)` + `S3 (18w)` `[Branch 1: Mechanism -> Cost]`: `With reservations,` -> inefficiency under over-sized requests.
  - `S4 (19w)` `[Branch 2: Mechanism -> Cost]`: `With priorities,` -> interference and non-deterministic performance.
  - `S5 (19w)` `[Branch 3: Mechanism]`: `Finally, with entitlements,` -> guaranteed minimum + redistribution.
  - `S6 (7w)` `[Claim]`: **7-word synthesis** (`Entitlements, unlike alternatives, provide isolation and efficiency.`).
  - `S7 (9w)` `[Contrast Pivot]`: Chains `Entitlements` directly into lead-1 -> `datacenters differ from those for a server`.
  - `S8 (11w)` `[Mechanism]`: Chains `server` -> `divisible resources`.
  - `S9 (14w)` `[Boundary — Theory]`: Chains `divisible resources` with an em-dash appositive.
  - `S10 (14w)` `[Contrast Pivot — Practice]`: `In practice, however,` breaks the abstraction -> `physically distributed across servers`.
- **Craft Takeaway**: Zero `Moreover/Furthermore/Additionally`. Effortless flow comes from strict parallel branches, lead-1 noun chaining (`Entitlements -> server -> divisible resources`), and punchy `7–11w` pivots.

---

## 5. Motivation — Tradeoff Framing with Explicit Causality (`SK-3`)
**Source**: *MorphCore* (MICRO 2012, p. 1)

> Traditional core microarchitectures do not adapt to the thread level parallelism (TLP) available in programs. In general, industry builds two types of cores: large out-of-order cores (e.g., Intel's Sandybridge, IBM's Power 7), and small cores (e.g., Intel's MIC a.k.a Larrabee, Sun's Niagara, ARM's A15). Large out-of-order (OOO) cores provide high single thread performance by exploiting Instruction-Level Parallelism (ILP), but they are power-inefficient for multi-threaded programs because they unnecessarily waste energy on exploiting ILP instead of leveraging the available TLP. In contrast, small cores do not waste energy on wide superscalar OOO execution, but rather provide high parallel throughput at the cost of poor single thread performance.

- **Progression & Given-New Chain** (`[15, 29, 35, 27]`):
  - `S1 (15w)` `[Claim]`: States the core mismatch (`do not adapt to TLP`).
  - `S2 (29w)` `[Quantitative / Concrete Anchor]`: Grounds the binary taxonomy (`two types of cores`) in real commercial silicon (`Sandybridge`, `Power 7` vs `Niagara`, `ARM A15`).
  - `S3 (35w)` `[Elimination — Branch 1]`: `Large OOO cores` -> strength (`high single thread performance`) + `because` causal failure (`waste energy on exploiting ILP instead of ... TLP`).
  - `S4 (27w)` `[Elimination — Branch 2]`: `In contrast, small cores` -> symmetric contrast along the exact same axis (`high parallel throughput at the cost of poor single thread performance`).
- **Craft Takeaway**: Uses the classic human causal toolkit (`because`, `instead of`, `In contrast`, `at the cost of`) to expose an architectural dilemma cleanly in 4 sentences.

---

## 6. Background — Taxonomic Family Grouping & Preconditions (`SK-5`)
**Source**: *RMM* (ISCA 2015, p. 2)

> Multipage Mapping approaches, such as sub-blocked TLBs [47], CoLT [39] and Clustered TLBs [38], pack multiple Page Table Entries (PTEs) into a single TLB entry. These designs leverage default OS memory allocators that either (i) assign small blocks of contiguous physical pages to contiguous virtual pages (Sub-blocked TLBs and CoLT), or (ii) map small set of contiguous virtual pages to clustered sets of physical pages (Clustered TLB).

- **Progression & Given-New Chain** (`[25, 42]`):
  - `S1 (25w)` `[Mechanism]`: Groups three prior works under one mechanism family and states their shared action with a concrete verb (`pack multiple PTEs into a single TLB entry`).
  - `S2 (42w)` `[Boundary / Precondition]`: Chains `These designs` directly to their shared OS allocator assumption, cleanly factoring the family into `(i)` and `(ii)` before the next paragraph exposes their scaling limit.
- **Craft Takeaway**: Never narrate background papers one by one (`[47] did X. [39] did Y.`). Group by shared mechanism and isolate the exact hidden precondition.

---

## 7. Design — Invariants, Bounded Hardware & ISA Precision (`SK-6`)
**Source**: *Swarm* (MICRO 2015, p. 5)

> Tasks with the same timestamp may execute in any order, but run atomically—the system lazily selects an order for them. A task can create one or more children tasks with an equal or later timestamp than its own. A child is ordered after its parent, but children with the same timestamp may execute in any order. Because hardware must track parent-child relations, tasks may create a limited number of children (8 in our implementation). Tasks that need more children enqueue a single task that creates them. Swarm adds instructions to enqueue and dequeue tasks. The enqueue_task instruction accepts a task descriptor (held in registers) as its input and queues the task for execution. A thread uses the dequeue_task instruction to start executing a previously-enqueued task. dequeue_task initiates speculative execution at the task's function pointer and makes the task's timestamp and arguments available (in registers).

- **Progression & Given-New Chain** (`[20, 18, 18, 18, 12, 8, 19, 12, 19]`):
  - `S1 (20w)` -> `S2 (18w)` -> `S3 (18w)` `[Invariants]`: Establish ordering semantics first; `S1` uses an em-dash to link atomicity to lazy order selection.
  - `S4 (18w)` `[Physical Cause + Quantitative Anchor]`: `Because hardware must track parent-child relations` -> states the exact implementation bound parenthetically (`(8 in our implementation)`).
  - `S5 (12w)` `[Boundary / Escape Hatch]`: `Tasks that need more children` -> software fallback (`enqueue a single task that creates them`).
  - `S6 (8w)` `[Claim]`: **8-word transition** introducing ISA extensions.
  - `S7 (19w)` -> `S8 (12w)` -> `S9 (19w)` `[Mechanism]`: Crisp subject-verb ISA descriptions (`accepts`, `queues`, `initiates`, `makes ... available`).
- **Craft Takeaway**: State invariants first, tie every hardware cap to a physical reason (`Because hardware must track...`), give the software escape hatch immediately, and map one concrete verb per ISA instruction.

---

## 8. Design — Corner-Case Race & Minimal Hardware Fix (`SK-7`)
**Source**: *InvisiSpec* (MICRO 2018, p. 9)

> First, for security reasons, we do not want the second request to use data loaded in the LLC-SB by a prior, squashed request (Section VII). Hence, InvisiSpec forbids a USL from obtaining data from the LLC-SB; if a USL request misses in the LLC, the request bypasses the LLC-SB and accesses main memory. Second, it is possible that the two USL requests get reordered on their way to the LLC-SB, which would confuse the LLC-SB. Hence, we add an Epoch ID to each core, which is a counter that the hardware increments every time the core squashes instructions. When a core communicates with its LLC-SB, it includes its Epoch ID in the message. With this support, even if two USL requests from different epochs are reordered in transit, the LLC-SB will know that, given two requests with different IDs, the one with the higher ID is the correct one.

- **Progression & Given-New Chain** (`[25, 28, 22, 23, 15, 36]`):
  - `S1 (25w)` -> `S2 (28w)` `[Branch 1: Threat -> Hardware Rule]`: Security constraint -> `Hence, InvisiSpec forbids...` and `bypasses the LLC-SB`.
  - `S3 (22w)` `[Branch 2: Corner-Case Race]`: Plain English hazard (`reordered on their way... which would confuse the LLC-SB`).
  - `S4 (23w)` `[Mechanism]`: `Hence, we add an Epoch ID` — plain functional name, exact increment trigger (`every time the core squashes instructions`).
  - `S5 (15w)` `[Next-Step State]`: Chains `Epoch ID` -> message field.
  - `S6 (36w)` `[Correctness Closure]`: Proves how `higher ID` resolves in-transit reordering unambiguously.
- **Craft Takeaway**: Explain tricky microarchitectural corner cases by naming what breaks in plain English (`would confuse the LLC-SB`), then adding the smallest plain-named counter (`Epoch ID`) with its exact trigger.

---

## 9. Evaluation — Microarchitectural Attribution Without Bar-Chart Narration (`SK-8`)
**Source**: *Vector Runahead* (ISCA 2021, p. 10)

> Figure 8 shows why Vector Runahead is able to achieve higher performance. Its pipelined vectors are able to issue many gathers to memory at once, thus hiding the serialization of dependent loads observed by the out-of-order core and PRE. This also shows us why some workloads are sped up more than others. Although our baseline OoO core features a relatively big ROB, which enables it to achieve high MLP on the simplest workloads, we note that Vector Runahead can extract significantly more MLP. Perhaps unsurprisingly, Vector Runahead achieves the largest speedups when the out-of-order core is comparatively weakest: for Camel, HJ2, HJ8 and Kangaroo, there are many instructions (address-computing or otherwise) executing along with the loads (Table II), which starve the out-of-order core of reorder buffer and issue queue resources [4, 5], limiting its memory-reordering ability. By contrast, Vector Runahead does not rely on the reorder buffer for high memory-level parallelism, as it can achieve the same effect through its vector gathers.

- **Progression & Given-New Chain** (`[12, 27, 13, 31, 53, 26]`):
  - `S1 (12w)` `[Claim]`: Announces causal intent (`shows why`, not "plots bars").
  - `S2 (27w)` `[Physical Cause]`: `issue many gathers to memory at once` -> `hiding the serialization of dependent loads`.
  - `S3 (13w)` `[Contrast Pivot]`: **13-word shift** to cross-workload variance.
  - `S4 (31w)` `[Boundary]`: Fairly credits the strong baseline (`relatively big ROB`, `high MLP on the simplest workloads`) using plain human phrasing (`we note that`).
  - `S5 (53w)` `[Mechanism Attribution]`: Clusters the four highest-gain benchmarks by their microarchitectural regime—intervening instructions `starve the out-of-order core of reorder buffer and issue queue resources`.
  - `S6 (26w)` `[Contrast]`: `By contrast,` links back to `vector gathers` bypassing the ROB bottleneck.
- **Craft Takeaway**: Zero bar-height recitation; credits the baseline fairly; groups workloads by hardware starvation (`ROB` and `IQ` pressure) rather than alphabetical order.

---

## 10. Evaluation — Mechanism Breakdown & Bottleneck Honesty (`SK-8`)
**Source**: *Darwin* (ASPLOS 2018, p. 10)

> First, performing bin updates to on-chip SRAM results in many times fewer random accesses to DRAM. Second, the hardware has longer sequential accesses to DRAM, resulting in higher effective bandwidth. Finally, the hardware accesses multiple DRAM channels in parallel. In our FPGA prototype, D-SOFT throughput is always limited by the DRAM bandwidth and not the on-chip bin updates, which occur at the rate of 5.1 updates/cycle (64% of theoretical maximum).

- **Progression & Given-New Chain** (`[16, 14, 9, 31]`):
  - `S1 (16w)` -> `S2 (14w)` -> `S3 (9w)` `[Split-Topic Attribution]`: Three orthogonal memory-access factors (SRAM filtering, sequential bursts, multi-channel parallelism), ending on a crisp `9w` line.
  - `S4 (31w)` `[Boundary / Honest Ceiling]`: Immediately volunteers the prototype's real physical ceiling (`always limited by the DRAM bandwidth`, `5.1 updates/cycle`, `64% of theoretical maximum`).
- **Craft Takeaway**: Even behind headline multi-thousand-fold speedups, volunteering the real bandwidth bottleneck and exact utilization ceiling (`64%`) wins instant reviewer trust.

---

## 11. Related Work — Evolutionary Synthesis & Orthogonal Positioning
**Source**: *GhostRider* (ASPLOS 2015, p. 13)

> Oblivious RAM was first proposed by Goldreich and Ostrovsky [21]. Since then, the community has made significant advances [20, 22, 23, 30, 53, 54] such that it evolved from a theoretical concept to real-life hardware prototypes [35, 40]. As an alternative to ORAM, active RAM capable of handling programmable logic may also be employed, such that memory addresses must be encrypted when transmitted over the memory bus. One candidate technology is the Hybrid Memory Cube [11]. Our compiler techniques are readily applicable to active RAM as well.

- **Progression & Given-New Chain** (`[10, 28, 29, 9, 11]`):
  - `S1 (10w)` `[Historical Anchor]`: Credits the foundational paper in 10 words.
  - `S2 (28w)` `[Evolutionary Synthesis]`: Compresses 8 citations into one clear arc (`theoretical concept -> real-life hardware prototypes`) instead of writing 8 separate sentences.
  - `S3 (29w)` `[Alternative Axis]`: Pivots cleanly to `active RAM` as an architectural alternative.
  - `S4 (9w)` `[Concrete Instantiation]`: Grounds `active RAM` in `Hybrid Memory Cube [11]`.
  - `S5 (11w)` `[Orthogonal Positioning]`: **11-word generous closing** explaining applicability rather than attacking prior work.
- **Craft Takeaway**: Group citations by developmental arc; mix `9–11w` anchors with `28–29w` syntheses; position work via orthogonality and scope rather than sweeping dismissal.

---

## 12. Conclusion — Crisp Single-Paragraph Verdict with Explicit Assumptions
**Source**: *Pond* (ASPLOS 2023, p. 13 — pre-LLM submission)

> DRAM costs are an increasing cost factor for cloud providers. This paper is motivated by the observation of stranded and untouched memory across 100 production cloud clusters. We proposed Pond, the first full-stack memory pool that satisfies the requirements of cloud providers. Pond consists of contributions at the hardware, system software, and distributed system layers to manage pooled/CXL memory. Our results showed that Pond can reduce the amount of needed DRAM by 7% with a pool size of 16 sockets and assuming CXL increases latency by 222%. This translates into an overall reduction of 3.5% in cloud server cost.

- **Progression & Given-New Chain** (`[10, 17, 15, 17, 28, 12]`):
  - `S1 (10w)` `[Claim]`: States the economic driver in 10 words.
  - `S2 (17w)` `[Quantitative Anchor]`: Recalls empirical motivation (`100 production cloud clusters`).
  - `S3 (15w)` -> `S4 (17w)` `[Past-Tense System Summary]`: `We proposed Pond` + compact stack scope.
  - `S5 (28w)` `[Bounded Quantitative Verdict]`: Reports the verified gain (`7%` DRAM reduction) **paired with its exact operating assumptions** (`16 sockets`, `assuming CXL increases latency by 222%`).
  - `S6 (12w)` `[Final Impact Anchor]`: Translates component savings into end-to-end fleet value (`3.5%` server cost) and stops—zero slogans, zero future-work rambling.
- **Craft Takeaway**: 99 words, 6 sentences, past tense, explicit unfavorable assumption (`222%` latency penalty), zero Abstract copy-paste, and zero `"paves the way"` clichés.

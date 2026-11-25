# Move-by-Move Section Drafting Playbooks

> **Scope**: **Mixed** — rhetorical moves, in-flow continuation, quantitative candor, and anti-patterns are **Universal**; all page/word/paragraph counts, 7-paragraph Intro templates, contribution bullet lists, and standalone section budgets marked *(Full paper)* apply **ONLY to 10–15p conference papers** (for 2–4p Letters, compress per `01-architecture-and-budgets.md §6`).

Use this reference when drafting or restructuring individual sections of a full conference paper (ISCA, MICRO, HPCA, ASPLOS) or adapting those rhetorical moves to short formats and excerpts. Pair with `04-paragraph-logic-and-cohesion.md` and `05-human-voice-and-stylometry.md` for sentence-level execution.

---

## 1. Title Craft

- **Length & Form**: **6–10 words** (hard cap 12). Prefer **`SystemName: Crisp Mechanism Subtitle`** or **`Action/Imagery Phrase: Subtitle`**. Reserve bare 2–4 word titles strictly for foundational primitives (*Vector Runahead*, *Autonomous NIC Offloads*). **Never use question titles.**
- **Naming Hygiene**: Pick a 1–2 syllable, pronounceable name tied to its mechanism (`Pond`, `Swarm`, `Whisper`, `Constable`, `InvisiSpec`). **Never invent forced backronyms** that cherry-pick interior letters. Lock the title system name 100% identically to body prose.
- **Modifier Cap**: **<= 2** hyphenated compounds and **<= 1** generic adjective (`Efficient`, `Fast`, `Scalable`, `Secure`, `Lightweight`). Never stack near-synonyms (`Secure ... Safe`) and **never put speedup numbers (`15,000X`) in the title**.

| Title Pattern | Strong Model | Failure Mode to Reject |
| :--- | :--- | :--- |
| **System + Mechanism** | `InvisiSpec: Making Speculative Execution Invisible in the Cache Hierarchy` | `M-ANT: Efficient Low-bit Group Quantization ... via Mathematically Adaptive Numerical Type` (modifier overload) |
| **Action / Counter-Intuitive** | `Flipping Bits in Memory Without Accessing Them: An Experimental Study of DRAM Disturbance Errors` | `PICACHU: Plug-In CGRA Handling Upcoming Nonlinear Operations...` (forced backronym) |
| **Restraint** | `Pond: CXL-Based Memory Pooling Systems for Cloud Platforms` | `... Provides up to 15,000X Acceleration ...` (promotional number in title) |

---

## 2. Abstract *(Full paper: `160–230w`, `8–10` Sentences)*

- **Target Envelope *(Full paper)***: **160–230 words**, 8–10 sentences, ~18–24w mean (hard cap <=45w per sentence). Single paragraph or crisp two-paragraph split (`Problem + Tension` / `System + Results`). *(For 2–4p Letters such as IEEE CAL, compress to `80–130w`, 4–6 sentences per `01-architecture-and-budgets.md §6`.)*
- **Five-Move Choreography**:
  1. **Move 1 — Domain Fact / Physical Invariant (`S1–S2`, 10–18w each)**: Open on a crisp architectural fact (*"Modern DRAMs have multiple banks to serve multiple memory requests in parallel."*).
  2. **Move 2 — Root-Cause Tension (`S3–S4`)**: Pivot sharply (`However,`, `Yet`) to why current mechanisms fail physically or structurally.
  3. **Move 3 — Key Insight (`S5–S6`)**: State the counter-intuitive observation or invariant that unlocks the solution.
  4. **Move 4 — Concrete System & Mechanism (`S7–S8`)**: Bridge naturally from Move 3's observation or constraint into the proposal (`To exploit this slack, we propose...`, `Based on this observation, we introduce...`—never drop a cold, unbridged `We propose <SystemName>` after a long setup), then summarize 2–3 concrete mechanisms in plain domain nouns.
  5. **Move 5 — Restrained Headline (`S9–S10`)**: Report **1–2 (max 3) quantitative anchors** pairing benefit with overhead or baseline (*"reduces DRAM cost by 7% with performance within 1–5% of same-NUMA-node allocations"*).
  - *Mechanism-First Variant* (tools, ISAs, primitives): Omit Move 1 and open directly with `"We introduce <SystemName>, a ..."` (90–130w).
- **Hard Bans**: Never open with `"In recent years"`, `"In the past decade"`, `"Recent advances in"`, `"With the rapid growth of"`, or `"X has revolutionized..."`. Never submit a zero-number abstract, never dump 6+ `%`/`×` metrics, and never claim `"oracle-level"` or `"always optimal"`.

---

## 3. Introduction: The Golden First 1.5–2 Pages *(Full paper: `1.0–1.5p`, `850–1,250w`)*

- **Hard Boundary *(Full paper)***: **1.0–1.5 pages (`850–1,250w`)**, ending **by Page 2** (latest p. 2.2). Anchor **Figure 1** on Page 1 or Page 2 and cite it explicitly—use a high-signal anchor (logic-vs-physical reality, bottleneck/headroom plot, minimal attack/code snippet, or section-indexed taxonomy), never decorative art.
- **Seven-Paragraph Move Sequence *(Full paper; for 2–4p Letters, merge into `0.4–0.6p` Intro & Motivation without contribution bullets per `01 §6`)***:
  1. **P1 — Sharp Architectural Hook (`~80–120w`)**: Never copy Abstract `S1`. Open with a concrete hardware tension, invariant, or production reality.
  2. **P2 — Quantified Bottleneck (`~100–150w`)**: Anchor severity with 1–2 empirical measurements or production facts—not adjectives (`substantial`, `severe`).
  3. **P3–P4 — Grouped Root-Cause Gaps (`~200–280w`)**: Partition prior approaches along **2–3 orthogonal axes** and expose the physical constraint breaking each (area vs frequency vs pin count). Ban paper-by-paper summaries and `Challenge-1/2/3` templates.
  4. **P5 — Key Insight / Central Question (`~120–180w`)**: State the pivot—why prior assumptions fail and what property your design exploits.
  5. **P6 — Concrete System Overview (`~150–220w`)**: Summarize named mechanisms without spilling bit-widths or FSM minutiae. If Intro >1.3p, add concise bold lead-ins (`Motivation.`, `Key insight.`, `Our work.`).
  6. **P7 — Validation Context & Headline + Cost (`~80–130w`)**: Specify evaluation vehicle (real servers, Linux kernel, RTL synthesis, cycle-accurate sim), workload scale, headline gains, **and honest overhead** (code size, area, storage, frequency penalty). Never copy-paste Abstract's closing lines.
  7. **P8 — Contribution Bullets *(Full paper optional, `~120–180w`; omit on 2p Letters)***: Write **3–4 mutually exclusive, concrete bullets** (max 5; omit bullets if a tight <=1.1p prose Intro flows cleanly). Lead with `We propose / design / show / identify / evaluate` (never `leverage`, `facilitate`, `meticulously craft`, `conduct a comprehensive evaluation`). Name specific mechanisms/findings and append `(§X)` pointers. **Ban `"To our knowledge, this is the first..."` filler bullets and ban `"The rest of this paper is organized..."` roadmaps.**

---

## 4. Background and Motivation *(Full paper: `1.2–2.0p` standalone or merged)*

- **In-Flow Continuation & Prose Discipline *(Universal — Applies to Motivation, Design, and Evaluation across all lengths)***: Mid-paper sections sit inside an ongoing technical argument—never write them as standalone mini-papers.
  - **Never re-expand already-defined acronyms & enforce Use-It-Or-Drop-It**: If Intro or Background already introduced `HBM`, `CSR`, `gVA`, or the system name, use the short term directly. Conversely, **never define an acronym (`(ILP)`, `(MLP)`) unless you reuse it at least once more in the same section or abstract**.
  - **Enter inside the local technical thread**: Never prepend a textbook recap of the whole paper's purpose at the start of Motivation, Design, or Evaluation; resume directly from what the preceding section established.
  - **Bounded Given-New (`35–48%`), Zero Tail Stutter & Zero 3-Hop Stem Chains**: Over half (~55%) of sentence boundaries progress cleanly without repeating a tail word (via next physical step, `However,`, data, or constant subject); `>55%` triggers verbal stuttering. Never repeat `>=3` tail words, mirror `S_i`'s `Subject+Verb` at `S_{i+1}`'s start (`"...shared across multiple cores. Because multiple cores share..."`), or chain one word stem across **3+ consecutive sentences** (`colocate -> colocating -> Such colocation`).
  - **Asymmetric Consecutive Frames & Relaxed Rhythm (`SD 8.5–11.5w`)**: Never clone syntactic openings across adjacent sentences (`"During X, ... / During Y, ..."`, `"On GPUs, ... / On CPUs, ..."`, `"A hit ... / A miss ..."`). Stay relaxed rather than flattening sentences into uniform 16–22w lines—let complex hardware explanations run organically to **26–38w** with plain **8–13w** factual sentences, and keep explicit transition adverbs to `<=1` per 2–3 paragraph excerpt (never insert non-contrastive `However,` between two additive sentences).
  - **No Datapath Verb Cycling, Pleonasms, or Essay-Gloss Idioms**: Repeat 1–2 plain datapath/action verbs (`crosses`, `reaches`, `stores`, `uses`) rather than rotating 4+ synonyms (`traverse/cross/pass through/travel across`), while keeping natural pronouns (`it`, `they`, `its`) and clean ellipsis so clauses never stutter robotically. Cut pleonasms/doublets (`"physical spatial locality"`, `"fixed and provisioned"`, redundant colon restatements `"two register pairs: one register pair for X and one register pair for Y"`) and essay idioms (`"Conventional X wisdom holds"`, `"operate in a very different regime"`, `"underlying hardware substrates"`, `"a surprisingly high payoff"`, `"inevitably"`, `"at its core"`).
  - **Calibrated Modals, No Slogans & Zero Editorial Gloss**: Keep realistic engineering modals (`can`, `may`, `often`, `typically`, `in practice`) rather than upgrading empirical/design statements to universal laws (`prevents`, `guarantees`, `directly produces`, `reaches full`). Keep short openers plain and factual (*"Figure 3 shows this behavior."*, *"We evaluate 14 workloads."*) rather than op-ed punchlines, and stop as soon as the final raw mechanism or measurement lands—never append interpretive editorial gloss telling the reader what a clean number means.
- **Zero-Idle-Term Background Audit *(Full paper: `300–900w`)***: Every concept, equation, or hardware structure defined in Background *must* be invoked in Motivation or Design. Delete field-standard textbook basics (standard Attention math, systolic array primers, DRAM channel/rank/bank basics, 4-level x86 page walks).
- **Just-in-Time Background**: Defer single-module details (e.g., Linux buddy allocator internals, specific ECC bit layouts) to a 1-paragraph setup immediately preceding the Design subsection that uses them. For cross-disciplinary theory (formal methods, device physics), declare the scope cap explicitly (*"A rigorous proof is beyond our scope; we give the intuition needed for protocol design"*).
- **Build Inevitability via Five Empirical Patterns** *(include >=2 quantitative proofs)*:
  1. *Oracle / Ideal Headroom + Drill-Down*: Quantify upside beyond SOTA, then isolate root causes (capacity vs conflict, data vs resource dependence).
  2. *Production Telemetry Debunking Folk Wisdom*: Disprove a field assumption with correlation or fleet distributions (e.g., fragmentation vs server uptime).
  3. *Visual Baseline-vs-Ideal Timeline*: Align baseline bubbles (`❶`, `❷`, `❸`) against ideal execution so Design mechanisms map 1-to-1 to eliminated stalls.
  4. *Negative-Result Motivation Ablation*: Show quantitatively which intuitive mechanism *fails* so your architectural subtraction is forced by data.
  5. *Preempt Reviewer #1's Objection*: Prove with compiler `-O3` disassembly, OS traces, or idealized baselines why software or existing hardware cannot solve the problem.
- **Fair Prior-Work Critique**: Isolate fundamental trade-offs (ideally in an objective feature matrix), credit where prior schemes succeed, and test against the **strongest/idealized** competitor. Ban `"However, existing works suffer from three critical limitations"`.
- **Clean, Spoiler-Free Handoff to Design**: **Never** drop your own evaluation speedups or plot your proposed system inside Motivation figures. Never copy paragraphs from Intro. Cap explicit `Observation / Takeaway` callouts at **2–4 per section**, each carrying a concrete number or counter-intuitive mechanism (never `"requires a careful balance"`).

| Handoff Mechanism | Best Used When... | Concrete Form |
| :--- | :--- | :--- |
| **Syllogism Bridge (`250–400w`)** | Step-by-step elimination leaves one architectural exit. | Short subsection: *However -> Hence -> Unfortunately -> Hence* with zero circuit spoilers. |
| **Terse Design Goals (`G1–G5`)** | Fleet characterization gives clear system requirements. | 4–5 bullets of 5–8 words each setting verifiable acceptance criteria. |
| **Req-Limitation-Approach Table** | Baseline has 3–5 separable structural inefficiencies. | Single table mapping baseline flaw -> requirement -> high-level approach + 2-sentence pointer. |
| **Core Invariants (`Condition 1–2`)** | Design hinges on exact correctness or safety predicates. | Short bridge section formalizing 2–3 necessary/sufficient conditions implemented next. |

---

## 5. Experimental Methodology *(Full paper: `450–900w`, `0.5–1.0p`)*

*(Expand to ~1.5p only for full silicon tape-outs, FPGA platforms, or complex real-cluster builds; compress to a single paragraph plus compact config table on 2–4p Letters per `01 §6`.)*

- **Four Compact Blocks** (bold lead-ins or short subsections):
  1. *Platform & Calibration*: Simulator/hardware/kernel versions, warmup/SimPoint length, BIOS noise controls (HT/Turbo/C-states), and **measured simulator-vs-real error bounds** (e.g., `-6%` to `+10%`).
  2. *Area, Power & Timing Modeling*: Tools (CACTI/McPAT/DSENT/Synopsys DC/Innovus), process node, scaling assumptions, and explicit model disclaimers (*"excludes random logic"*, *"single-cycle allocator"*).
  3. *Workloads & Exclusion Disclosure*: State workload selection criteria and **explicitly justify every excluded benchmark** from standard suites (compiler/simulator incompatibility, non-memory-bound).
  4. *Baselines & Anti-Strawman Proof*: Document how you kept competitors strong (published optimal configs, parameter sweeps under equal budget, verifying custom baselines match published speedups). When orthogonal, evaluate `Baseline + Ours`.
- **Table-First Static Parameters**: Pack all static core/cache/DRAM/cluster specs into `Table X`. Never read table rows aloud in prose—spend prose only on rationale, calibration, and simplifications.

---

## 6. Evaluation *(Full paper: `1,900–2,600w`, `2.0–2.7p`)*

- **Five-Stage Cognitive Arc *(Full paper; select Headline + 1–2 highest-signal plots/tables on 2–4p Letters)***:
  1. *Headline End-to-End*: Answer Intro's central claim first (geomean + range), grouped by workload behavior.
  2. *Causal Attribution / Additive Ablation*: Quantify each component incrementally (`1.00× -> 1.47× -> 1.69× -> 1.79×`) and explain the microarchitectural mechanism behind each step. Ban adjective-only ablations.
  3. *Sensitivity & Scalability Sweeps*: Focus on knees, saturation thresholds, U-shaped optima, or compact empirical scaling laws (`X/2%` vs `X%`).
  4. *Overhead & Cost Accounting*: Area (`mm²` and `%`), static/dynamic power, network/memory traffic, storage KB, and software LoC changes.
  5. *Outliers, Case Studies & Stress Tests*: Dissect worst-case inputs, adversarial workloads, or microarchitectural anomalies.
- **Trend Synthesis Over Bar Narration**: Partition 15–30 benchmarks into **2–3 microarchitectural regimes** (e.g., `>25 MPKI` + `>15 WMPKI` vs low-MPKI compute-bound). **Never narrate bars alphabetically (`"First, Axpy... Second, Blackscholes..."`).** Never triple-report identical numbers across Table, Figure, and Prose.
- **Calibrated Modality, Plain Verbs & Zero Editorial Gloss (Evaluation Discipline)**:
  - **No Evaluation Verb Cycling or Pleonasms**: Repeat 1–2 plain measurement verbs (`is`, `achieves`, `reaches`, `drops to`, `reduces`) cleanly inside a paragraph rather than rotating 4–7 verbs (`reaches/surpasses/climbs to/spends/overtakes/crosses below`), while keeping natural pronouns and clean ellipsis so adjacent clauses never stutter robotically. Ban redundant pleonasms (`"up to X% at maximum"`, `"strongly outperform"`, `"a surprisingly high payoff"`) and unused acronyms.
  - **Calibrated Engineering Modals**: Keep calibrated modals (`can`, `may`, `often`, `typically`, `in practice`) when describing workload behavior or attributing gains—never harden bounded results into universal causal laws (`directly produces`, `guarantees`, `eliminates`, `reaches full utilization`).
  - **Zero Editorial Gloss**: State the measurement and its physical microarchitectural cause plainly and move on—never append editorial-gloss tails instructing the reader how to interpret an obvious number (`"showing why static partitioning falls short"`, `"which confirms the efficiency gain"`).
  - **Asymmetric Framing & Relaxed Rhythm**: Vary consecutive case/regime sentence openings asymmetrically (ban `"On GPUs, ... / On CPUs, ..."`, `"During X, ... / During Y, ..."` clones), avoid 3-hop stem chains and `>=3`-word tail stutters (`Given-New5` `35–48%`), and let complex causal explanations breathe naturally (`26–38w`) with plain short factual sentences (`8–13w`).
- **Five Credible Negative-Result Patterns** *(include >=2–3 per full paper; >=1 on 2–4p Letters)*:
  1. *Local loss to baseline* with architectural trade-off explanation (e.g., `-2.5%` ST clock or `1-core` slowdown offset by `64-core` scaling).
  2. *Worst-case overhead disclosure* naming specific regressing benchmarks and listing exact microarchitectural causes.
  3. *Secondary-metric trade-off* in the same sentence (e.g., P99 latency improves while P50 rises).
  4. *Within-noise null result* explicitly stating marginal gains are not meaningful speedups.
  5. *Reconciling divergence from prior literature* via concrete system mechanics (e.g., packet batching shrinking with connection count).
  Never write `"consistently achieves superior performance"` when any plotted bar loses.
- **Metric & Precision Discipline**:
  - Ratios/speedups -> **Geometric Mean**; multi-programmed throughput -> **Weighted Speedup** or **Harmonic Mean** (never arithmetic mean of ratios); additive quantities -> **Arithmetic Mean**.
  - **Bind `up to Y` or `maximum Y` to the average whenever an average exists in the data**: Write `"by X% on average (geomean), and up to Y% on <regime>"`. However, **factual fidelity takes precedence**: if source measurements only report a worst-case bound or range without a mean, report the exact bound honestly and never fabricate a synthetic average.
  - Use **integer or 1-decimal `%`** (~92% of cases) and **1–2 decimals for `×`** (`1.47×`, `43×`). Ban 4–6 sig-fig simulator noise (`450.65×`, `0.43099 pJ`, `373829.28 s`); allow >=3 decimals *only* for sub-0.1% area/error rates or `99.999%` reliability.
  - Prefer `%` for `< 2×` relative gains, overheads, and reductions (or consistent normalized speedup factors like `1.47×`); always use `×` for `>= 2×` speedups. Write `"150× lower energy"` or `"99.3% energy reduction"`, never `"reduces energy by 150×"`. Lock `×` globally. Vary subsection closings—never clone `"We make X observations... Based on these results, we conclude..."` across >2 consecutive subsections.

---

## 7. Related Work *(Full paper: `450–650w`, `0.5–0.8p`)*

- **Group by Design Axis, Never by Author**: Make architectural mechanisms or assumptions the topic sentences and subheadings. Keep sentence-initial `Author et al. [X]` below 5% and **never stack >2 consecutive author-first sentences**.
- **Explicit Contrast Every Group**: End each group with 1–2 sentences articulating the exact structural difference or orthogonality (`"orthogonal and composable with..."`, `"targets offline traces, whereas..."`). For >=4 multi-axis competitors, include a 4–6 column qualitative matrix and honestly mark any unsupported features (`✗`) for your own system.
- **Generous, Non-Combative Tone**: Credit prior work under its intended assumptions before noting scope differences. Ban sweeping dismissals (`"All prior works suffer from..."`) and hollow `"To our knowledge, first..."` boasts.

---

## 8. Discussion, Limitations, and Conclusion *(Full paper: Disc `0.4–0.7p`; Conc `90–150w`)*

- **Discussion / Limitations *(Full paper: `250–600w`, `0.4–0.7p`; or `150–300w` for a compact Limitations-only subsection)***: Surface 2–3 genuine limits (unsupported runtimes like JIT, concurrency/consistency boundaries, adversarial misuse, simulator fidelity gaps, or OS portability). Skip empty 4-sentence cheerleading `Discussion` blocks.
- **Conclusion *(Full paper: `90–150w`, 1 Paragraph, 4–6 Sentences; 2–4p Letters: `45–75w`, 2–3 Sentences)***:
  - *Four-Beat Blueprint*: (1) Past-tense statement of what we designed/characterized (`We presented...`); (2) Core architectural insight and mechanism; (3) 1–2 verified headline numbers with governing trade-off/bound; (4) Grounded technical implication.
  - Keep **3-gram overlap with Abstract < 12%**—never paraphrase Abstract sentence by sentence.
  - **Hard Bans**: Zero new claims, zero future-work laundry lists, zero promotional closers (`"paves the way"`, `"promising avenue for future research"`, `"democratizing"`, `"this work pioneers"`, `"rocket fuel"`).
- **Pre-Submission Mechanical Sanity Check**: Verify list-count parity (never `"three applications: A, B, C, and D"`), duplicated words (`"and and"`), broken auxiliaries (`"are been"`), unresolved citations (`[?]`), and leaked XML/markup artifacts.

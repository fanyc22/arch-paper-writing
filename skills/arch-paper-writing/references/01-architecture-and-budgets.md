# Macro Architecture, Page Budgets, Archetypes, and Venue Calibration

> **Scope**: **Full Conference Papers (10–15 body pages)** for §§1–5; **Short Formats / 2–4 Page Letters (e.g., IEEE CAL)** use **§6 only** (skip §§1–5 for letters, rebuttals, or single excerpts).

Use this reference when outlining a full manuscript (`§§1–5`), allocating page/word budgets, selecting a narrative arc, calibrating for a target venue (ISCA, MICRO, HPCA, ASPLOS), auditing cross-section contracts, or structuring a 2–4 page short paper or letter (`§6`).

---

## 1. The 40-25-20-15 Body Budget Law

Total PDF length in modern architecture venues (~14–15 pages) reflects References (~2.0–2.5p) and optional Artifact Appendices sitting outside page limits. **Body length from Section 1 through Conclusion remains tightly conserved at 11.5–12.5 pages (~9,500–10,500 layout words; ~7,100–8,600 pure prose words excluding tables/captions).**

| Functional Block | Target Body Share | Target Pages | Target Words | Structural Discipline |
| :--- | :---: | :---: | :---: | :--- |
| **Introduction** | ~9–12% | **1.0–1.5p** | 850–1,250w | Must finish by end of **Page 2** (latest p. 2.2); Fig. 1 anchored on p. 1–2. |
| **Background & Motivation** | ~10–15% | **1.2–2.0p** | 1,000–1,800w | Compact and evidence-driven (up to 2.5p *only* for fleet-scale characterization). |
| **Design, Overview & Impl** | **~38–45%** | **4.5–5.5p** | 3,500–4,800w | Absolute center of gravity; never starve Design to feed textbook Background. |
| **Methodology & Evaluation** | **~25–30%** | **3.0–3.5p** | 2,500–3,400w | Methodology `0.5–1.0p` (`450–900w`) + Evaluation `2.0–2.7p` (`1,900–2,600w`). |
| **Discussion / Limitations** | ~3–6% | **0.4–0.7p** | 250–600w | Candid scope boundaries and deployment trade-offs; skip empty cheerleading. |
| **Related Work** | ~4–6% | **0.5–0.8p** | 450–650w | Default **late** (after Evaluation, before Conclusion). |
| **Conclusion** | ~1.5% | **0.15–0.20p** | **90–150w** | Single terse paragraph; zero Abstract copy-paste, zero hype. |

---

## 2. Section Ordering, Naming & Structural Pitfalls

### Canonical Ordering Rules
1. **Late Related Work Is the Default**: Place Related Work after Evaluation and immediately before Conclusion (~88–96% of top papers). Readers need your microarchitectural vocabulary and results before sharp structural contrasts land.
   - *Two-Tier Split*: When 2–3 direct competitors are required to motivate the problem, compare them concisely in Section 2 (ideally via a compact comparison table), state the division upfront (*"Section 2 compares closely related schemes; Section 8 covers broader work"*), and title the closing section **`Other Related Work`** to prevent repetition.
   - *Forbidden*: Never wedge Related Work between Design and Evaluation (breaks design-to-evidence momentum), and never split Related Work into two disconnected sections leaving a tiny stub at the end.
2. **Reject the Mechanical `2. Background` + `3. Motivation` Split**: Separating textbook `Background` from `Motivation` bloats front-matter (~18% of body) and pushes core Design past Page 4–5. Prefer:
   - **Claim-titled Section 2** (strongest): Name Section 2 after the concrete bottleneck or measurement theme (e.g., `Limitations of SFI`, `Memory Contiguity Challenges at Scale`, `Branch Prediction Challenges for Datacenter Workloads`).
   - **Merged `Background and Motivation`** (`<= 2.0p`): Combine minimal domain terms with empirical bottleneck proof when the baseline structure *is* the root cause.
3. **Keep `Overview` as `X.1` by Default**: Use `Section 3.1 / 4.1 Overview` (`0.5–0.8p` + system diagram) to orient readers without fragmenting top-level hierarchy. Promote `Overview` to a top-level section *only* when the design spans 2+ independent top-level sections (e.g., ISA/Hardware + OS/Compiler, or multi-mechanism ladders).
4. **Never Name Core Design `Methodology`**: In ISCA/MICRO/HPCA/ASPLOS, `Methodology` exclusively means *Experimental/Simulation Methodology*. Name core design sections after your system or mechanism (`<SysName> Architecture`, `<SysName> Design`, `Hardware Support`).
5. **Kill the Introduction Roadmap**: Never write `"The rest of this paper is organized as follows. Section 2 describes..."`. Embed inline `(§X)` or `(Section X)` pointers inside the contribution bullets or Fig. 1 taxonomy instead.
6. **Place `Discussion / Limitations` After Evaluation**: Never discuss limitations or extensions *before* presenting experimental evidence. Place `Artifact Appendix` after References.

### Structural Anti-Patterns to Reject (Even When Seen in Top Venues)
- **7-Bullet Contribution Walls**: Keep contributions to 3–4 bullets; half-page 6–7 bullet lists bloat Intro and repeat numbers three times before Page 3.
- **Abstract-to-Intro Copy-Paste**: Never paste the Abstract's closing sentences verbatim into Intro's final paragraph.
- **Mid-Paper Related Work + Stub Tail**: Do not place a primary Related Work section before Evaluation and follow Evaluation with a 7-line `Other Related Work` fragment.
- **Title Without System Name**: Never omit your system name from the Title if the Abstract and body rely on it as the primary anchor.

---

## 3. Four Canonical Paper Archetype Arcs

Lock your paper into one archetype before outlining. Each archetype requires specific **persuasive turning points**.

### Archetype A: Microarchitecture / Cache / Prefetch / Memory
- **Skeleton**:
  - `§1 Introduction (1.0–1.2p)`
  - `§2 Bottleneck & Headroom Study (1.8–2.5p)`
  - `§3 <SysName> Design & Mechanism Ladder (3.5–4.5p)` *(includes `§3.1 Overview`, Walkthrough, Corner Cases, Storage/BOM)*
  - `§4 Experimental Methodology (0.7–0.9p)`
  - `§5 Evaluation: Headline + Attribution + Sensitivity (2.5–3.2p)`
  - `§6 Discussion / Limitations (0.4p)` -> `§7 Related Work (0.6p)` -> `§8 Conclusion (0.15p)`
- **Persuasive Turning Points**:
  1. *Quantified Headroom*: CPI stack or Oracle upper-bound study proving remaining upside beyond SOTA (not just naive baselines).
  2. *Mechanism Ladder or Cycle Walkthrough*: Build progressive tiers (e.g., zero-HW -> minimal-HW -> full) or walk a concrete instruction trace through the pipeline.
  3. *Exact Hardware Accounting & Causal Attribution*: Byte-exact storage breakdown, critical-path FO4/cycle cost, and microarchitectural causality (MLP, port contention, traffic) explaining every speedup.

### Archetype B: SW-HW Co-Design / VM / OS-Architecture / CXL Systems
- **Skeleton**:
  - `§1 Introduction (1.2–1.6p)`
  - `§2 Minimal Background & Fleet/System Characterization (1.8–2.5p)`
  - `§3 Hardware Substrate & Interface (1.8–2.2p)` + `§4 OS / Software Control Plane (1.8–2.2p)`
  - `§5 Implementation & Emulation Calibration (0.8–1.3p)`
  - `§6 End-to-End Evaluation: Real System + Simulation (2.5–4.0p)`
  - `§7 Discussion / Applicability (0.6p)` -> `§8 Related Work (0.6p)` -> `§9 Conclusion (0.15p)`
- **Persuasive Turning Points**:
  1. *Cross-Layer Mismatch Proof*: Production telemetry or real-system data proving pure-SW is too slow and pure-HW lacks semantic context.
  2. *Physical HW/SW Responsibility Split*: Separate hardware mechanisms/ISA from OS policies/schedulers into distinct sections or subsections with an explicit interface contract.
  3. *Dual-Track Validation*: Calibrate simulation/emulation against real machines/kernels, then evaluate full-scale real workloads with microbenchmarks.

### Archetype C: Accelerator / ML / GPU Architecture
- **Skeleton**:
  - `§1 Introduction (0.9–1.4p)`
  - `§2 Workload / Dataflow Characterization & Baseline Inefficiency (1.8–3.0p)`
  - `§3 Algorithm / Dataflow Co-Design (1.5–2.0p)`
  - `§4 Accelerator Microarchitecture, NoC & Memory Hierarchy (2.5–3.5p)`
  - `§5 Physical Implementation: RTL Synthesis / P&R Area & Power (0.8–1.2p)`
  - `§6 Evaluation: Iso-Area / Iso-Power / Accuracy Trade-offs (2.0–3.0p)`
  - `§7 Related Work (0.5–0.8p)` -> `§8 Conclusion (0.15p)`
- **Persuasive Turning Points**:
  1. *Data-Movement & Utilization Accounting*: Quantify memory-hierarchy energy ratios or spatial underutilization on real GPUs/TPUs before introducing a new array.
  2. *Algorithm-Hardware Closed Loop*: Tie every numerical or algorithmic change directly to the hardware block it removes or simplifies.
  3. *Silicon-Grounded Fairness*: Report synthesized/P&R area, power, and clock at an explicit process node; evaluate against competitors at iso-area, iso-power, or iso-accuracy.

### Archetype D: Hardware Security & Architecture Characterization
- **D1 — Security Attack / Defense**:
  - `§1 Intro (1.0–1.3p)` -> `§2 Background & Formal Threat Model (1.0–1.8p)` -> `§3 [Attack Discovery / Breaking SOTA (1.5–2.2p)]` -> `§4 Defense Architecture (3.0–4.2p)` -> `§5 Security Analysis (0.8–1.4p)` -> `§6 Performance/Cost Evaluation (1.5–2.2p)` -> `§7 Discussion + §8 RW + §9 Conclusion (1.2p)`.
  - *Turning Points*: Pair pre-design **Threat Model** (In-Scope vs Out-of-Scope channels) 1-to-1 with post-design **Security Analysis**; add a brief `Responsible Disclosure.` paragraph in Intro for attacks on commercial silicon.
- **D2 — Characterization / Measurement** *(no single Design section)*:
  - `§1 Intro (1.0–1.5p)` -> `§2 Domain Context / Platform Primer (1.5–2.0p)` -> `§3 Validated Measurement Methodology (1.5–2.0p)` -> `§4–§6 Multi-Axis Empirical Findings (4.5–6.0p)` -> `§7 Design Implications / Pathfinding (1.0–4.5p)` -> `§8 Limitations + §9 RW + §10 Conclusion (1.0p)`.
  - *Turning Points*: Anchor the paper on one counter-intuitive thesis and close **every empirical subsection** with a bold **`Implications.`** paragraph delivering concrete architectural prescriptions.

---

## 4. Four-Venue Calibration Matrix

| Dimension | **ISCA** | **MICRO** | **HPCA** | **ASPLOS** |
| :--- | :--- | :--- | :--- | :--- |
| **Community DNA** | Broad architectural vision + silicon grounding + deep reflection | Deepest microarchitectural mechanics + tight area/power accounting | Accelerators/memory/GPUs + crisp cycle-accurate sweeps | Full-stack SW-HW co-design + real machines/OS kernels |
| **Budget Bias** | Balanced; Intro `~1.0p`, Design `~38–42%`, Discussion in `~30–37%` of papers | Shortest Intro (`<=1.0p`), heaviest Design (`42–45%`), densest Meth (`~950w`) | Compact Meth (`~670w`) & RW (`~460w`), Discussion in `~13%` of papers | Longest Intro (`~1.3p`) & Eval (`~2,600w`), highest Artifact Appendix |
| **Primary Validation Vehicle** | RTL/VLSI synthesis (`53%`), explicit process node (`50%`), FPGA (`32%`) | CACTI/McPAT area & power (`42%`), cycle-accurate simulation (`45%`), EDP | Cycle-accurate (`50%`) & GPU/accel simulation (`34%`), broad parameter sweeps | **Real servers/GPUs (`74%`) & Linux/OS/compiler builds (`42%`)**; pure sim is risky (`11%`) |
| **Numeric & Style Norms** | High candid-flaw disclosure; bold paragraph lead-ins welcome | Highest figure/table density (`15–16` figs, `4` tbls); strictly scrub AI hype | Explicit **Geomean** + consistent 1-decimal `%` (`25%`); pragmatic tone | Prefer clean integer `%` (`78%`), active `We/Our`, P50/P99 tail latency & LoC |
| **Cross-Ref & RW Convention** | `Figure` + `Section`; late RW (`85%`) | `Figure` + `Section`; late RW (`89%`) | `Figure`/`Fig.` + `Section`/`Sec.`; **NEVER use `§` (0%)**; early RW tolerable (`18%`) | Full **`Figure`** (`96%`) + `Section` or **`§`** (`29%`); late RW (`97%`), zero author-list RW |

---

## 5. Cross-Section Contract Checklist

Before finalizing any outline or full manuscript, verify all five contracts hold 1-to-1:

1. **Claim-to-Evidence Closure**: Every headline number in the Abstract is contextualized in the Introduction (without verbatim copying) and backed by a specific figure or table in Evaluation.
2. **Contribution-to-Section Mapping**: Every Introduction bullet maps to an explicit section `(§X)` that delivers the exact mechanism or finding promised—zero orphaned claims and zero late surprise mechanisms.
3. **Zero Verbatim Self-Plagiarism**: Never copy sentences across `Abstract -> Intro`, `Intro -> Motivation`, or `Abstract -> Conclusion`. Each layer must raise resolution (`Abstract` = headline -> `Intro` = scope + insight -> `Motivation` = proof -> `Design` = mechanics -> `Conclusion` = synthesized takeaway).
4. **Macro-Locked Naming**: Lock the system name spelling, hyphenation, and capitalization via one macro (`\sysname`) across Title, Abstract, headings, prose, and figures.
5. **Boundary Honesty**: Threat-model exclusions and Methodology simplifications must align 1-to-1 with Limitations and Conclusion—never claim generality that Methodology ruled out.

---

## 6. Short-Format & 2–4 Page Letter Adaptation (IEEE CAL, Workshop Papers)

Skip `§§1–5` above when drafting a 2–4 page architecture letter (such as IEEE Computer Architecture Letters) or workshop short paper. Keep **one sharp architectural claim** rather than shrinking a 12-page outline into microscopic font.

### Compact Budget & Section Flow (`3–5` Sections)

| Functional Block | **2-Page Letter (IEEE CAL, ~1,400–1,800w)** | **4-Page Short / Workshop Paper (~2,800–3,500w)** | Structural Discipline |
| :--- | :---: | :---: | :--- |
| **Abstract** | **`80–130w`** (4–6 tight sentences) | **`100–150w`** (5–7 tight sentences) | 1-sentence invariant + tension, core mechanism, and 1–2 headline numbers paired with cost or baseline. |
| **1. Introduction & Motivation** | **`0.4–0.6p`** (~350–500w) | **`0.7–1.0p`** (~600–850w) | Merge hook, concrete quantified bottleneck, and 1-sentence thesis directly. **Do NOT include a contribution bullet list on a 2-page letter** (optional max 2–3 tight bullets only on a 4p paper); zero roadmaps. |
| **2. `<SysName>` Design** | **`0.6–0.9p`** (~500–750w) | **`1.3–1.8p`** (~1,100–1,500w) | Compress the 6-layer ladder into **Overview + Core Invariant + Primary Mechanism** synced to one diagram, plus a 2–3 sentence hardware cost summary. Defer secondary optimizations and minor edge cases explicitly. |
| **3. Evaluation** | **`0.5–0.8p`** (~450–650w) | **`1.0–1.4p`** (~850–1,200w) | Open with a 1-paragraph Methodology (or compact inline config table), present **1–2 high-density result plots/tables** synthesized by microarchitectural regime, and include at least one candid trade-off or slowdown. |
| **4. Related Work & Conclusion** | **`0.2–0.3p`** (~120–200w) | **`0.4–0.6p`** (~280–450w) | Either fold 2–3 direct structural contrasts into Sec. 1/3 and close with a **2–3 sentence (`45–75w`) Conclusion**, or pair one compact mechanism-grouped Related Work paragraph with a 2–3 sentence Conclusion. |

### Visual Budget & Universal Rules That Stay 100% Identical
- **Visual Budget (`1–3` Visuals Max)**: Allocate **1–3 high-density figures/tables total**—typically one compact overview/mechanism diagram, one headline evaluation plot, and an optional small configuration or overhead table. Never pack 6 tiny plots or multi-page breakdowns into a 2–4p letter.
- **Universal Core (Unchanged Across All Lengths)**: Every prose, logic, detail, and visual craft rule still applies in full:
  - `03-detail-and-abstraction.md`: Earned-Detail criterion, General-before-Fast-Path, zero RTL inventory dumps, default `0` `Algorithm` blocks, zero fake math.
  - `04-paragraph-logic-and-cohesion.md`: Bounded Given-New (`35–48%`), Paragraph Shuffle, zero tail stutters or 3-hop stem chains, zero mirrored frames, balanced plain-term locking with natural pronouns and clean ellipsis.
  - `05-human-voice-and-stylometry.md`: Plainspoken register, relaxed burstiness (`SD 8.5–11.5w`), calibrated modals, natural pivots (`<=1` per 2–3 paragraph block), rare em-dashes (default `0` in short blocks). Interpret multi-page ratios (e.g., passive `%`) qualitatively on 2-page letters.
  - `06-anti-ai-and-anti-patterns.md`: Zero Tier-1 AI words, 2024+ risers, pleonasms, essay idioms, result participles, or editorial gloss.
  - `07-figures-tables-captions.md (§§2–8)`: Table/Figure/Prose boundary, honest y-axes, grayscale-safe locked palette, >=7pt typography, booktabs tables, 15–35w takeaway captions, and the 6-point visual audit.
  - `08-adversarial-self-audit.md`: Run all seven checks (skipping full-paper page/section budget gates).
- **Rebuttals & Standalone Excerpts**: Skip this file (`01`) completely and apply the Universal Core (`04`, `05`, `06`, `08`, plus `03` for mechanism prose and `07 §§2–8` if referencing figures or tables).

# Figures, Tables, Captions, and Visual-Text Coupling

> **Scope**: **Mixed** — **§1 (12–16 Figure Portfolio & Page 1–2 Anchor)** applies **ONLY to Full Conference Papers (10–15p)** (2–4p Letters use **1–3** high-density visuals); **§§2–8** (Table/Figure/Prose boundary, chart ergonomics, grayscale-safe color, typography, diagram grammar, booktabs tables, captions, 3-beat prose coupling, 6-point visual audit) are **Universal**.

Use this reference when planning a paper's figure/table portfolio, choosing chart types, specifying color/typography/diagram layout, formatting booktabs tables, writing captions, or auditing figure-text integration. *(Pure visual design, layout, and caption guidelines—no plotting scripts.)*

---

## 1. Visual Budget, Mix, and Figure 1 Placement *(Full Conference Papers Only — 10–15p)*

- **Short-Format / 2–4p Letter Budget (e.g., IEEE CAL)**: Skip the 12–16 figure portfolio below; budget **1–3 high-density figures/tables total** (typically one compact overview/mechanism diagram, one headline evaluation plot, and an optional small config/overhead table) and apply `§§2–8` in full.
- **Golden Portfolio Budget *(Full paper)***: Target **12–16 figures** and **2–4 tables** (~4:1 figure-to-table ratio) across a 12-page body.
  - Avoid under-budgeting (<6 figures) that forces unreadable 24-subplot walls, and avoid over-budgeting (>22 figures) that compresses plots into single-column barcodes.
  - *Venue calibration*: MICRO and HPCA sit near the upper end (14–16 figs, 3–4 tables); ASPLOS uses fewer tables (2–3, occasionally 0) and richer multi-sentence captions.
- **Section Allocation (~25 : 47 : 28)**: Place roughly **25%** of figures in Intro + Background/Motivation, **45–50%** in Design/Methodology, and **25–30%** in Evaluation/Discussion. Across the paper, **quantitative data plots (~48%)** and **architecture/mechanism diagrams (~52%)** balance roughly 1:1.

| Canonical Figure Category | Typical Count (14-Fig Paper) | Primary Narrative Role |
| :--- | :---: | :--- |
| **Evaluation Result Plots** | 5–6 (~40%) | Headline speedup/overhead, causal attribution, sensitivity sweeps, area/power. |
| **System / Microarch Overviews** | 2–3 (~16%) | Top-level architecture, pipeline hook-in, hierarchy zoom-in, die/PnR visuals. |
| **Mechanism Timelines & Walkthroughs** | 2 (~13%) | Baseline-vs-proposed cycle timelines, concrete storyboard frames, code snippets. |
| **Motivation / Headroom Plots** | 1–2 (~8%) | Bottleneck breakdown, Oracle headroom, fleet telemetry proving inevitability. |
| **Supporting Background / Format Diagrams** | 2–3 (~23%) | Compact hardware baseline, data/PTE layout, auxiliary structures. |

- **Figure 1 Anchor Rule**: Place Figure 1 **by the end of Page 2** (~69% standard). Place Figure 1 on **Page 1** *only* when it carries high-signal punch—one of three forms: (1) *Problem + Goal Quantified Teaser* (with explicit target arrow `GOAL`), (2) *Paradigm / Coverage Contrast*, or (3) *Minimal Attack / Code Example* (<=15 lines). Never spend Page 1 on textbook background.

---

## 2. Table vs. Figure vs. Prose Decision Boundary

Over **83%** of architecture tables hold heterogeneous structured lookup data—never primary bar-chart replacements:

| Carrier | Use When Presenting... | Concrete Architecture Examples | Never Use For... |
| :--- | :--- | :--- | :--- |
| **Table** | Heterogeneous multi-unit specs; exact parameter lookup; storage/area/power BOMs; qualitative feature/protocol diff matrices; extreme multi-order-of-magnitude scalars (`10^-11` vs `10^-44`); 2D grids needing exact values + visual optima (*heatmap table*). | System/simulator config (~41% of tables); workload suites (~15%); hardware storage/area/power (~15%); taxonomy/ISA/protocol diffs (~13%). | 20–30 benchmark speedup distributions; 2–3 isolated scalar numbers. |
| **Figure** | Trends, distributions, long-tail CDFs, latency/energy breakdowns, scaling sweeps, Pareto frontiers, pipeline/spatial topologies, or cycle-level timeline overlaps. | Sorted speedup bars + GEOMEAN; CDF slowdowns; architecture block diagrams; storyboard walkthroughs; hop-by-hop latency budgets. | Static 15-row simulator parameter lists; raw multi-field bit-width inventories. |
| **Prose** | **2–4 isolated homogeneous scalars** (*"average overhead is 0.2%, max 0.7%"*). | Single summary overhead, LoC count, or rare fallback rate. | Multi-row config tables or 10+ workload comparisons. |

---

## 3. Experimental Chart Selection & Ergonomics

| Evidence Structure | Preferred Chart Form | High-Ergonomics Details | Forbidden Anti-Patterns |
| :--- | :--- | :--- | :--- |
| **10–35 benchmark speedup / overhead** | **Sorted grouped bar chart** (ascending gain or grouped by suite) | Separate `GEOMEAN` / `AVG` with a **shaded band or vertical dashed line** + exact value callouts atop summary bars. | Alphabetical unsorted bars; `GEOMEAN` blended into benchmark bars; 40+ bars crammed into one column. |
| **50–160 benchmark distribution** | **Suite-grouped overview + adjacent CDF** (or sorted S-curve with win/loss shading) | Annotate off-scale outlier counts in a clean text box (*"3 outliers >100%, max 124%"*). | Single average hiding tails; **24-subplot raw data walls** with 4pt labels. |
| **Time / energy / area breakdown (<=5 parts)** | **Stacked bar chart** (absolute or 100%) | Pair muted colors with distinct sparse hatches for grayscale clarity. | **Pie charts**; **>6-part rainbow stacked bars** (e.g., 16 colors). |
| **Continuous parameter sweeps / scaling** | **Line plots or shared-axis small multiples** | Use **direct curve labels** next to lines instead of distant legend boxes; annotate off-scale superlinear peaks (`117×`) at the top edge rather than squashing lower curves. | **Connecting unordered discrete benchmarks with continuous lines**; repeating identical legends per subplot. |
| **Multi-metric trade-off** (accuracy vs latency, perf vs power) | **Pareto frontier scatter/line plot** | Mark target direction (`Better ↗`), shade infeasible regions, and use explicit `//` axis breaks across empty ranges. | Splitting coupled trade-offs into separate bar charts with mismatched scales. |
| **2D matrices / density / latency histograms** | **Perceptually uniform heatmap (`viridis`)** or **tier-annotated histogram** | Label hardware tiers directly above histogram bands (`L1/LLC Hit`, `1st–3rd DRAM`). | `jet` rainbow colormaps; **decorative 1D colorbars** duplicating the y-axis of a 1D chart. |

### Y-Axis Honesty & Dual-Axis Discipline
- **Default to `0` origin**. Silently truncating bar-chart y-axes (e.g., starting at `0.70`, `1.00`, or `55%`) visually inflates 5–10% gains by 2×–4×.
- When small normalized margins (`1.00–1.15`) need legibility, choose one honest method: (1) plot **relative `% improvement` from `0%`**, (2) draw an **explicit `//` axis break** on line/Pareto plots, or (3) draw a **prominent `1.00` dashed baseline** and print exact values atop summary bars.
- **Avoid dual y-axes** unless two tightly coupled quantities share one exact x-axis (never mix 6 bars + 2 lines on one dual-axis plot). Always label both axes with explicit units and match visual encoding to each axis.
- **Lock y-scales across side-by-side subplots** sharing one y-axis title—never shift scales silently (`60% / 300% / 400%`) across adjacent panels.

---

## 4. Color, Typography, and Column Ergonomics

1. **Global Semantic Palette Contract**: Lock **3–5 muted, colorblind-safe colors** with distinct grayscale luminance (e.g., Baseline = light/mid gray, Proposed = deep navy/teal, Ideal/Accent = muted brick red or charcoal) before creating Figure 1. Enforce this exact mapping across **every figure**—never invert red/blue assignments between figures, especially on the same page.
2. **Dual Redundant Encoding**: Never rely on hue alone or >3 unhatched shades of gray:
   - *Lines*: **color + line style (solid/dashed/dotted) + marker shape**.
   - *Bars (>3 series)*: **lightness gradient + sparse hatching**.
   - *Grayscale + Single Accent* excels for architecture diagrams (gray baseline + one crisp accent for added logic).
   - **Ban neon yellow (`#FFFF00`)**, raw Office/Excel saturated primaries, and low-contrast red-on-dark-blue text.
3. **Typography Floor**: Every printed character inside figures (ticks, axis labels, box text, callouts) must render at **>= 7 pt** (75–85% of body font). Use crisp sans-serif in diagrams and match body serif math notation inside plots.
4. **Column Width & Legend Hygiene**:
   - Cap single-column bar charts at **<= 6–8 x-axis groups**. Promote >=12 benchmarks or multi-panel sweeps to **two-column full width** (`figure*`).
   - **Never** pack two independent figures side-by-side in one column or use narrow `wrapfigure` cutouts.
   - Multi-panel figures sharing series get **one shared legend** (top or right) and drop duplicate interior axis labels.
   - Zero colliding ticks (`128256512`), zero axis labels touching captions, and zero legend boxes covering bars.

---

## 5. Microarchitecture Block-Diagram Grammar

1. **Unidirectional Flow + Path Typing**: Route primary data left-to-right or top-to-bottom. Lock **solid arrows = data path** and **dashed arrows = control, invalidation, or metadata path**.
2. **Hierarchy + Zoom-In Callouts**: Show macro organization first and expand one block via a dashed zoom callout. Keep boxes to **<= 5–8 words**—zero walls of text or 3.5pt sub-circuits.
3. **Pipeline-Stage Anchor Strip**: For core modifications, include a slim horizontal pipeline strip (`Fetch -> Decode -> Rename -> Issue -> Mem -> Commit`) showing exactly where added hardware attaches.
4. **Progressive Timeline Comparisons**: Compare `Baseline -> Ideal -> Tier 1 -> Full` with identical primitives and double-headed brackets directly labeled with saved cycles (`4 cycles saved`).
5. **Storyboard Walkthroughs with Step Badges**: Step through concrete frames `(A) -> (G)` or circled badges **`❶ ❷ ❸`** and highlight only per-step diffs (red entries or strikethroughs on invalidated rows).
6. **Engineering Ground-Truth Visuals**: When available, include hop-by-hop latency budget diagrams (ns/hop + compact assumption inset), die photos, scaled PnR floorplans, real terminal outputs (`numactl`), or hardware profiler waveforms. Ban amateur clipart (traffic signs, PowerPoint clouds).

---

## 6. Clean Booktabs Table Craft

- **Rules**: Use `\toprule`, `\midrule`, `\bottomrule`, and `\cmidrule` for grouped headers. **Zero vertical rules (`|`)** and **zero multi-color "candy" zebra shading** (at most ~5% light gray alternating rows for tall tables).
- **Alignment & Precision**: Left-align text; right-align numbers with thousands commas (`1,318,603`) and uniform significant figures (1–2 decimals; never raw 5-decimal CACTI logs like `0.43099 pJ`). Unify unit spacing (`35 KB`, never mixed `35 KB` / `9.4KB`) and check squared units (`mm²`).
- **Semantic Bolding**: Bold *only* your system row, per-row optima/extrema, or incremental protocol diffs—and define bolding explicitly in the table caption.

---

## 7. Caption Anatomy, Prose Coupling, and Visual Spec Format

### Caption Formulas & Anti-Patterns

| Caption Style | Target Length | Pattern / Example | Verdict |
| :--- | :---: | :--- | :---: |
| **Title + Back-Link + Takeaway** | 15–35w | *Pool access latency comparison (§4.1). Pond reduces latencies by 1/3 compared to switch-only designs.* | **Gold Standard** |
| **Setup + Quantified Claim** | 15–35w | *Whisper performance across baseline predictor sizes: Whisper cuts mispredictions by 11.2% even on a 1MB TAGE-SC-L.* | **Strong (Eval)** |
| **Claim-as-Title / Question-Form** | 10–20w | *`sssp` has plentiful ordered irregular parallelism.* / *Which rows are affected by an aggressor row?* | **Strong (Motiv/Char)** |
| **Table Caption** | 7–15w | *Baseline processor parameters.* / *Multi-bit errors per DIMM (bold marks uncorrectable).* | **Standard (Tables)** |
| **Cryptic Stub** | 3–5w | *LICM at 2c.* / *Store breakdown; 2-entry CLQ; 10-cycle WCDL.* | **Ban** |
| **Legend Dictionary** | >60w | *A) lane 1; B) lane 2; ... M) unit X...* (symptom of an overcrowded graphic) | **Ban — Simplify Plot** |

### Prose Coupling ("Three-Beat Rule")
1. **Plain Introduction Verbs**: Use `Figure X shows` (workhorse), `illustrates / depicts` (diagrams), `compares / plots` (data), or `Table Y summarizes / lists`. Never write `"elegantly showcases"` or `"holistically unveils"`.
2. **Sync Badges & Synthesize Regimes**: Walk diagrams via inline step badges (`❶ in Figure 8`). Interpret data plots in three beats—*frame axes -> distill 2–3 regime observations -> explain microarchitectural causality (including outliers)*—never read bars one by one.
3. **Strict `\ref{}` Sync**: Always generate numbers via `\ref{}` and confirm every sublabel (`(a)`, `(b)`) and badge (`❶–❿`) matches verbatim inside the graphic.

### Figure Specification Template (For Author Handoff — No Plotting Code)
When designing a figure for an author, specify: **(1) Role & Target Section**, **(2) Width** (`1-col` vs `2-col`), **(3) Chart/Diagram Type**, **(4) Axes, Units & Origin** (or Data vs Control Path Typing), **(5) Locked Palette / Hatch Mapping**, **(6) Direct Callouts & GEOMEAN Divider**, and **(7) Ready-to-Use Caption Draft**.

---

## 8. Six-Point Pre-Submission Visual Audit

- [ ] **Grayscale Print Check**: Convert rendered pages to grayscale—do all lines, stacks, hatches, and heatmaps remain 100% distinct?
- [ ] **Cross-Figure Palette Lock**: Do baselines and your proposed system keep identical color, hatch, marker, and legend order from Figure 1 to the final figure (zero inversions)?
- [ ] **Embedded Vector Spell & Unit Check**: Read every axis label, legend, box label, and unit manually (LaTeX spellcheckers miss vector graphics—catch `Efficiecny`, `Comparision`, `Lantecy`, missing `mm²`, or inconsistent spaces).
- [ ] **Zero-Collision & Completeness Check**: Confirm zero overlapping ticks/labels/captions, >=7pt printed text, units on all axes, and 100% legend coverage (no unexplained lines or bars).
- [ ] **Bidirectional Reference Parity**: Verify every prose pointer (`Figure 4(b)`, `Table 2`, `❸`) matches the exact figure number, sublabel, and unique badge inside the graphic.
- [ ] **3-Minute Figure-Skim Test**: Reading *only* figures, tables, and captions without body text, can a reviewer reconstruct the bottleneck, core design, and main results?

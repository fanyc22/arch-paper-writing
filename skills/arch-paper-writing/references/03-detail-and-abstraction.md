# Design Presentation, Abstraction Layering, and Detail Control

> **Scope**: **Universal** — Earned-Detail, General-before-Fast-Path, anti-RTL-sprawl, and anti-formalization-inflation apply to **all lengths**; the `3,500–4,800w` Design budget applies to **Full Conference Papers** only (in 2–4p Letters, compress the 6-layer ladder to Overview + Core Invariant + Primary Mechanism + inline cost summary).

Use this reference when structuring Design/Architecture/Implementation sections, deciding which parameters belong in prose vs tables vs appendices, crafting walkthrough examples, or pruning RTL sprawl and formalization inflation.

---

## 1. The Six-Layer Abstraction Ladder

Structure Design sections *(Full Conference Paper: ~38–45% of body, ~3,500–4,800 words; in 2–4p Letters, compress L1–L6 to Overview + Core Invariant + Primary Mechanism synced to one diagram + a 2–3 sentence cost summary)* strictly top-down so broad-area reviewers grasp the architecture from Layers 1–2 + 4 while specialists verify rigor in Layers 3 + 5–6. In full papers, open Design with a **3–5 sentence explicit layering roadmap**.

```text
L1: High-Level System Overview & Layered Roadmap (architecture diagram + scope)
 ↓
L2: Core Idea & Correctness Invariant (necessary & sufficient conditions)
 ↓
L3: Component Mechanics by Dataflow / Lifecycle (idea-driven, never a parts list)
 ↓
L4: Concrete End-to-End Walkthrough (synced with a numbered figure)
 ↓
L5: Corner Cases & Bounded-Resource Constraints (coherence, deadlock, squash, OS)
 ↓
L6: Hardware Cost, Storage Table & Bill of Materials (bytes, ports, FO4, area, power)
```

### Three Core Layering Moves
1. **Unbounded-First Layering**: When finite queues, buffer overflows, or eviction deadlocks obscure core semantics, strip resource limits first: *"First, we present the ISA extensions. Second, we describe the hardware assuming unbounded queues. Third, we handle bounded queues and deadlock. Fourth, we detail hardware costs."* Once the core execution model is crystal clear, bounded constraints become easy to absorb.
2. **Physical Section Split for Complex Designs**: When both conceptual semantics and microarchitectural integration are dense, separate them into two top-level sections—*Conceptual Mechanism / Data Structure* first, *Detailed Microarchitectural Integration* second—rather than interleaving cache ports and bit-packing into the core idea.
3. **Intentional Omission Statements & Empirical Corner-Case Pruning**:
   - Never silently omit edge cases (reviewers assume you overlooked them). Declare simplifications explicitly with scope and pointer: *"For simplicity, we assume no 1GB pages"*, *"Table 1 ignores transient states"*, *"The complete interface is listed in Appendix A."*
   - Before adding recovery hardware for rare events (e.g., checkpointing auxiliary tables on branch misprediction or rare register overflow), measure its ROI. If omitting recovery changes performance by `<0.2%` or triggers on `<0.2%` of dynamic instances, report that number in two sentences and fall back to baseline execution cleanly.

---

## 2. General Mechanism Before Fast-Path / Optimizations

Never interleave **mandatory correctness machinery** with **opportunistic fast paths or workload-specific optimizations**:

1. **Close a Correct Base Mechanism First**: Establish the simplest complete, deadlock-free baseline that satisfies all L2 invariants.
2. **Expose Concrete Base Limitations**: State precisely what performance, energy, or bandwidth bottlenecks remain in the base design (e.g., write-recovery serialization, insufficient timeliness, high swap traffic).
3. **Layer Decoupled Optimizations Incrementally**: Introduce each optimization in a separate subsection or clearly tagged `Optional` block (e.g., `Tier 1 -> Tier 2 -> Tier 3`, or `Base Pipeline -> Workload Optimizations -> Parallelism`). Flag any optimization restricted to specific algorithms or relaxed threat models—and tag its hardware cost as `optional` in the BOM.

---

## 3. The Earned-Detail Criterion

A low-level hardware number—bit-width (`33-bit`), port count (`3R/2W`), gate depth (`19 logic gates`), or circuit delay (`0.5 FO4`)—earns space in body prose **only if the same sentence or the next sentence uses it to prove an architectural constraint or design choice**:

- **Earned (Keep in Prose)**:
  - *Line-packing invariant*: Showing that 8 PTEs plus a 33-bit VPN tag (bits 47–15) fit into a single 64-byte cache line without an extra memory read.
  - *Critical-path proof*: Showing that adding one transmission-gate mux (`0.5 FO4` in a 20-FO4 stage) costs 2.5% clock frequency, or that a 19-gate logic tree executes in parallel with a branch predictor.
  - *Comparator / SRAM physical floor*: Showing that region alignment reduces bounds checks to one 32-bit comparator, or that an 8-bit hint matches the minimum SRAM compiler row width.
- **Unearned (Push to Table / Appendix)**: Raw entry counts, field widths, associativities, port specs, and timing parameters listed purely as inventory.
- **Noise (Cut Completely)**: Undergraduate binary comparison tutorials (`'1100' > '0101'`), pin-level gate wiring (`2 SR latches, 2 3-input AND gates with Tc fed to 'b'`), textbook reviews of ROB/RAT/MSHR/4-level page tables, or duplicated symmetric handshake traces.

### Unhurried Natural Pacing & Unpacking Stacked Noun Compounds
- **Write at Natural Pacing (`~100%` Budget, Never Bullet-Compressed)**: Do not artificially compress Design prose below natural pacing (`-10%` summary-note density). Let complex hardware interactions breathe across normal clauses rather than jamming three modifiers into one noun phrase.
- **Unpack Stacked Hyphenated Noun Compounds**: Expand dense synthetic noun stacks into plain prepositional phrases or clauses:
  - *Compressed*: `"atomicity-versus-reactivity provisioning tension"`, `"relocation-induced miss-rate overhead"`, `"switch state-retention duration"`.
  - *Unpacked*: `"the tension between atomicity and reactivity when provisioning energy"`, `"miss-rate overhead from relocating cache lines"`, `"how long switches hold their state"`.
- **Stay In-Flow, Repeat Plain Datapath Verbs & Avoid Redundant Colon Restatements**: Assume acronyms defined earlier are known—never re-expand them mid-Design or define one-off unused acronyms (`(ILP)`, `(MLP)`). Repeat 1–2 plain datapath verbs (`crosses`, `reads`, `stores`, `updates`) instead of cycling synonyms (`traverse/cross/pass through/travel across`), while keeping natural pronouns (`it`, `they`, `its`) and clean ellipsis so adjacent clauses never stutter robotically; cut synonym doublets (`"fixed and provisioned"`, `"physical spatial locality"`) and redundant colon restatements (`"two register pairs: one register pair for X and one register pair for Y"`), and let complex multi-stage mechanics run organically to `26–38w` rather than chopping every sentence to 16–20w.

### Surgical Detail-Pruning Micro-Examples
- **RTL Datasheet Sprawl -> Earned Summary**:
  - *Cut*: 300 words explaining MSB comparison of `'1100'` vs `'0101'` plus `"2 SR latches... and 2 3-input AND gates, with Tc fed to 'b' and Ts to 'a'"`.
  - *Keep*: `"We use a bit-serial MSB-first comparator that scans 32-bit timestamps over 32 cycles, adding two latches and two logic gates per SRAM column (0.4% array area)."`
- **Peppered SRAM Specs -> Table-Backed Prose**:
  - *Cut*: `"The RAT, a 6-bit × 32-entry structure... the P-VRF is implemented as eight 4R-2W 1-KB (64-bit words × 128 entries) SRAM structures..."` scattered across mechanism paragraphs.
  - *Keep*: Describe register renaming semantics cleanly in prose and cite `Table 1` once for all entry counts, bit-widths, and port configurations.
- **Fake Combinatorial Wrapper -> Plain Invariant**:
  - *Cut*: Three numbered `Cost` / `S* = argmax` equations disguising a queue grouping heuristic.
  - *Keep*: One crisp invariant sentence (*"We group sibling beams spawned from the same parent in the queue while preserving parent arrival order"*) synced to a concrete walkthrough diagram.

---

## 4. Four-Subfield Detail Decision Matrix

Calibrate detail placement to the subfield's native baseline:

| Subfield | Keep in Body Prose (Idea & Invariant Driven) | Push to Table / Diagram / Appendix | Cut Completely (Noise / Bloat) |
| :--- | :--- | :--- | :--- |
| **1. CPU / Cache / Prefetch / Memory** | Critical-path impact (`+0.5 FO4`, `1-cycle` lookup); correctness invariants (coherence pinning, store disambiguation, squash); port/capacity bottlenecks driving redesign; headline total KB, area `%`, power. | **Storage & Port Breakdown Table** (entries, per-field bits, total KB, R/W ports); DRAM timing tables; full simulator parameters; full FSM truth tables. | Gate/pin wiring (`latch`, `pin 'a'/'b'`); textbook RAT/MSHR/ROB reviews; binary comparison lessons; trivial `Algorithm` boxes. |
| **2. Accelerator / ML / GPU / Quantization** | Dataflow mapping & PE folding; algebraic transformations that *directly eliminate hardware blocks*; memory-hierarchy reuse tiers (RF / SRAM / DRAM); headline PE array, SRAM, node, area, power. | **PE / Buffer Spec Table** (MAC/accumulator bit-widths, mixed-precision modes, double-buffer KB); operator approximation tables; concise <=6-line topology specs if needed. | Textbook CNN/Attention/Softmax/uniform-quantization formulas; per-mux PE wire narration; 15-line pseudocode wrapping simple `for` loops. |
| **3. SW-HW Co-Design / OS / VM / CXL / Serving** | HW/SW interface contract & responsibility split; cache-line/page alignment arithmetic *when proving scaling limits*; OS corner cases (`fork`, CoW, TLB shootdown, fragmentation fallback); high-level scheduling decomposition. | Complete ISA / syscall / ABI tables (Appendix); algebraic bounds & optimality proofs (Appendix); compact 1-paragraph software stack & LoC summary. | Wrapping plain heuristics in fake `argmax` combinatorial math; kernel source dumps; standard x86 PTE or CXL header recitations. |
| **4. Hardware Security & Microarch Attacks** | Exact **Threat Model** (In-Scope vs Out-of-Scope channels); security invariants & **compact hardware BOM**; complete side-channel/speculation/coherence/interrupt closure; empirical tests validating silicon behavior. | Attack-surface & protection matrices; multi-tier security config tables; full instruction encodings & register layouts (Appendix); reverse-engineered mapping tables. | Duplicate numbered equations for simple subtractions; sweeping security claims outside the threat model; basic cache/DRAM primers. |

---

## 5. Dual-Track Concrete Walkthrough Craft

Never explain multi-cycle state evolution, out-of-order hazards, or multi-core races through 500 words of abstract letters. Replace abstract prose with one **120–200 word concrete walkthrough synchronized to a numbered figure**:

1. **Fix Concrete Values and Step Badges**: Use concrete numbers (`N=8`, `GPU0–GPU7`, `W0–W7`, `PC_x`, timestamps `X=2, T=3, U=1`, cache line `A`) and walk steps `❶ -> ❷ -> ❸` or `(A) -> (G)`. If shrinking dimensions for visual clarity (e.g., vector width 4 instead of 16), state the scaling explicitly in a footnote or sentence.
2. **Pair Real Code with Simplified Diagrams**: When instruction-level behavior matters, anchor the mechanism to a compact real hot-loop assembly snippet (15–30 lines) marking the exact dependent loads/branches.
3. **Run Happy Path + Corner Case Together**: Demonstrate both the normal speedup and one hazard/recovery path in the same tight scenario (e.g., `LD1` trains and pins coherence -> `LD2` hits and eliminates execution [happy path] -> intervening `ST1` to address `A` triggers disambiguation flush and re-execution of `LD3` [corner case]). A 3-timestamp concrete counterexample (`X=2, T=3, U=1`) clarifies a concurrency bug faster than two pages of prose.

---

## 6. Defending Against Both Extremes: RTL Sprawl vs. Formalization Inflation

### Defending Against Extreme A: RTL / Datasheet Sprawl
Consolidate hardware cost cleanly at **L6** instead of scattering parameters across prose:
1. **Storage & Port Breakdown Table**: List every added/modified structure, entry count, per-entry bit fields, total KB, and R/W ports.
2. **Compact Hardware Bill of Materials (BOM, 5–8 lines)**: Tally total added instructions, registers, comparators/muxes, critical-path delay, synthesized area (`mm²` and `%`), and power in one clean paragraph.

### Defending Against Extreme B: Post-2023 Formalization Inflation
Nearly 90% of classic top-venue architecture papers use **0 `Algorithm` blocks** and average **<2 numbered equations**. Never use pseudocode or Greek notation as decorative rigor:

1. **Default to 0 `Algorithm` Blocks**: Include at most one compact (**<= 15 lines**) listing *only* for non-obvious concurrency, lock-step synchronization, recursive routing, or subtle eviction invariants that prose + diagram cannot state unambiguously. **Never** box trivial `argmin` loops, zero-initialization loops, or black-box wrapper calls (`Q-LG(·)`).
2. **Ban Line-by-Line Algorithm Narration**: If an `Algorithm` block is warranted, explain its invariant and key branch in 3–5 sentences. **Never** write `"Line 1 initializes m' to ∞ ... Lines 7–14 iterate ... Line 15 returns..."`.
3. **Ban Decorative Equations and Unused Notation**:
   - Every defined set or symbol must participate in a real derivation or hardware rule—never declare `Let S = ...` and drop it.
   - Keep elementary arithmetic (`ACT_left = T_RH - ACT_aggr`) inline; **never** number basic arithmetic and **never** assign two equation numbers to the same formula across sections. Push algebraic derivations and bounds to an Appendix, keeping only the governing inequality in the main body.

---

## 7. Five-Point Design Section Self-Check

- [ ] **Layered Roadmap**: Does Design open with a 3–5 sentence top-down roadmap (unbounded/conceptual before bounded/detailed)?
- [ ] **General Before Fast-Path**: Is the base correctness mechanism completely closed before any optional optimization is introduced?
- [ ] **Earned-Detail & Natural Pacing**: Does every bit-width, port count, or gate delay in prose immediately prove an architectural constraint, and are stacked hyphenated noun compounds unpacked into plain, unhurried clauses?
- [ ] **Dual-Track Walkthrough**: Does at least one concrete figure-synced walkthrough demonstrate both the normal path and one conflict/corner case?
- [ ] **Zero Formalization Bloat**: Are `Algorithm` blocks at 0 (or <=1 justified <=15-line block with zero line-by-line narration), with zero unused symbols or numbered trivial math?

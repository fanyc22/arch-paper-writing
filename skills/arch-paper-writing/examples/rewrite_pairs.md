# Surgical Rewrite Pairs (Before -> After)

Twelve diagnostic rewrite pairs spanning **Class B (classic LLM-drifted)**, **Class C (try-hard anti-AI over-correction and deep-discourse tells)**, and **Class A (weak-human)** failures across Introduction, Motivation, Design, Methodology, Evaluation, Related Work, and Conclusion. Every **After** rewrite satisfies all seven gates of `references/08-adversarial-self-audit.md`—relaxed, plainspoken engineering prose with bounded Given-New flow (`0` tail-stutters), asymmetric sentence openings, calibrated modals, zero editorial gloss, zero Tier-1/2 or elevated-register leaks, zero trailing result participles, zero mid-clause `, however,` smuggling, and zero em-dash bursts.

---

## Pair 1: AI Intro Throat-Clearing & Frankenstein Seam -> Mechanism-First Opening

**Before (LLM purple opener + broken unedited follow-up + abstraction whiplash):**
> In the ever-evolving realm of quantum computing, quantum computers (QCs) in Noisy Intermediate-Scale Quantum (NISQ) era [71] have captivated people's attention, offering immense potential of computation to unravel intricate problems in chemistry, biology, algorithms, and machine learning. Superconducting QCs [4, 47], particularly the utilizing fixed-frequency transmon qubits anchored by Josephson junctions, stands out as a leading option for scalable quantum computing. These merits have led to significant advancements in the field, as evidenced by the current generation of superconducting QCs, which boasts over 1000 physical qubits [41]. However, this scale is still insufficient for tackling intricate real-world problems [10].

**After (Mechanism-first, single abstraction band, plain sentence-initial `However,`):**
> Superconducting processors built from fixed-frequency transmon qubits [4, 47] now exceed 1,000 physical qubits [41], backed by nanosecond-scale gate latencies [6, 7] and fidelities approaching fault-tolerance thresholds [80]. However, scaling physical layouts past a thousand qubits exposes severe crosstalk. Fixed-frequency transmons cannot retune their operating frequencies after fabrication, so neighboring components placed too closely in space or frequency degrade two-qubit gate fidelity.

**Diagnostics:**
- Deleted the 44-word press-release opener (`ever-evolving realm`, `captivated people's attention`, `unravel intricate problems`) and generic application list.
- Eliminated the **Frankenstein seam** (`the utilizing ... stands out`) and hollow shell noun (`These merits`).
- Used plain sentence-initial `However,` (not postpositive `, however,`) to introduce an 11-word factual pivot (`28w -> 11w -> 23w`), keeping a clean `B2 -> B3` zoom-in.

---

## Pair 2: AI Paraphrase-Echo + Fake Discourse Glue -> Zero-Redundancy Causal Chain

**Before (4 sentences orbiting one claim, flat `13w–22w` cadence, synonym cycling + `Additionally,`):**
> Hestia offers a comprehensive simulation approach that supports multiple behaviors and levels simultaneously. This multi-level interpretation enables more effective debugging by providing designers with deeper insights into their HLS designs. Through its multi-level debugger, Hestia enables transparent and efficient debugging across different abstraction levels, facilitating more effective bug identification. Additionally, by establishing an equivalence mapping among these levels, Hestia enables precise bug localization, further enhancing its effectiveness in the debugging process.

**After (`SK-6`, zero echoes, parentheses instead of em-dashes, concrete verbs):**
> Rather than running a single monolithic RTL simulator, Hestia splits HLS simulation into three synchronized IR interpreters (functional, schedule, and structural). Designers isolate control-flow bugs at the fast schedule level and descend to cycle-accurate structural state only during the failing execution window. Equivalence maps then pinpoint the exact compiler pass causing each mismatch.

**Diagnostics:**
- Removed three consecutive Paraphrase Echoes repeating `enables effective debugging / identification / localization`.
- Stripped Tier-2 bloat (`comprehensive`, `facilitating`, `enhancing`), fake glue (`Additionally,`), and synonym cycling (`simulation approach -> multi-level interpretation -> multi-level debugger`).
- Used standard parentheses `(functional, schedule, and structural)` instead of em-dashes and kept a clean `21w -> 21w -> 11w` technical progression where every sentence delivers a non-swappable delta.

---

## Pair 3: AI Hollow Shell-Noun + Participle-Tail Bloat -> Grounded Concrete Causality

**Before (Fake `However,`, double hollow shell nouns, `, offering ... tailored to ...`, `, ensuring ...`):**
> Large language models (LLMs) have revolutionized natural language processing by achieving state-of-the-art performance across diverse benchmarks. However, nonlinear operations in LLMs significantly contribute to inference latency and present unique challenges that have not been encountered previously. Addressing these challenges requires accelerators that combine efficiency, flexibility, and support for user-defined precision. Coarse-Grained Reconfigurable Arrays (CGRAs) provide an effective solution, offering a balance of performance and flexibility tailored to domain-specific workloads, ensuring efficient execution across emerging models.

**After (`SK-1`, natural `However,`, plain factual pivot, explicit `because`, paired `up to`):**
> Existing LLM accelerators optimize matrix multiplication (GEMM), so nonlinear operators such as Softmax, RMSNorm, and SwiGLU account for 24% of inference latency on average (and up to 46% at long sequence lengths). However, fixed function units cannot keep pace with new models. Static silicon becomes obsolete before tape-out because new architectures keep adding nonlinear primitives that require floating-point precision to preserve perplexity. Rather than building dedicated blocks for each operator, we map all nonlinear operators onto a plug-in CGRA that shares the systolic array's output SRAM and reconfigures its tile datapaths across operators and precisions.

**Diagnostics:**
- Killed the false `However,` (NLP accuracy never contradicted nonlinear latency), generic opener (`revolutionized`, `diverse`), double hollow shell nouns (`unique challenges` -> `Addressing these challenges`), and stacked participle tails (`, offering ... tailored to ..., ensuring ...`).
- Grounded the problem in named operators, a paired quantitative anchor (`24%` average, `up to 46%`), a plain factual 10-word pivot (`However, fixed function units cannot keep pace with new models.`), and an explicit `because` clause (`32w -> 10w -> 20w -> 33w`).

---

## Pair 4: AI Formalization-Inflation & Pseudocode Echo -> Invariant + Concrete Trace

**Before (Decorative `argmax` dressing up a FIFO-grouping heuristic + line-by-line echo):**
> To formalize prefix-aware scheduling, we define the optimal batch sequence $S^* = \arg\max_{S \in \Pi(B)} \sum_{k} \text{Reuse}(b_k, b_{k-1}) - \lambda \cdot \text{Cost}(S)$. Algorithm 1 presents our scheduling procedure. Line 1 initializes the ready queue $Q$ to empty, and Lines 2–5 iterate over all incoming beams to inspect their parent identifiers. Lines 6–9 subsequently check whether a matching parent group exists in $Q$ and append the beam accordingly, thereby ensuring optimal KV-cache reuse while preserving fairness.

**After (Plain invariant + natural `As a result,` + concrete trace, zero fake optimization):**
> Our scheduler avoids unnecessary KV-cache evictions with one invariant: beams spawned from the same parent are grouped contiguously in the ready queue while preserving their parents' arrival order. As a result, sibling beams run back-to-back before their shared prefix is evicted. On a four-slot KV cache serving four candidate paths (`ABDG`, `ACFJ`, `ABEI`, `ABDH`), keeping the three `AB*` siblings together cuts total prefix evictions from 8 nodes under FIFO scheduling to 6.

**Diagnostics:**
- Stripped decorative pseudo-math (`S* = argmax`) disguising a queue-grouping rule, and deleted the redundant line-by-line pseudocode translation (`Line 1... Lines 2–5...`).
- Replaced `subsequently` and `, thereby ensuring optimal...` with a 28-word invariant, a natural 13-word `As a result,` transition, and a 31-word concrete trace proving the eviction drop (`8 -> 6`).

---

## Pair 5: Weak-Human RTL Datasheet Sprawl + Nominalization -> Earned-Detail Mechanism

**Before (Class A nominalization + undergraduate binary/gate-wiring prose):**
> The freeing up of a physical register occurs in two distinct cases, and the comparison of the 32-bit timestamps `Ts` and `Tc` is performed bit-serially. For instance, the greater of the two numbers `'1100'` and `'0101'` can be determined as the first number `'1100'` by looking at the MSB. Each bit-serial comparator consists of 2 SR latches and 2 three-input AND gates, with the `Tc` bit fed to pin `'b'` and the `Ts` bit fed to pin `'a'`. This allows comparing all 32 bits in 32 cycles.

**After (Active verbs, plain `9w -> 31w -> 28w` progression, earned constraints only, gates in Table 2):**
> The core reclaims a physical register in two cases. To avoid wiring a 32-bit parallel comparator into every cache way, the tag array compares the incoming timestamp `Ts` against stored timestamps `Tc` bit-serially from MSB to LSB over 32 cycles. This bit-serial check adds only 4 logic gates per way (Table 2) and stays off the L1 hit critical path because timestamp verification runs only on cross-process misses.

**Diagnostics:**
- Fixed nominalization (`The freeing up of... occurs in` -> `The core reclaims... in`) and bare `This allows`.
- Deleted undergraduate binary trivia (`'1100' > '0101'`) and pin-level RTL wiring (`fed to pin 'b'`).
- Applied the **earned-detail rule**: kept `32-bit`, `32 cycles`, and `4 logic gates per way` only because each directly proves an architectural constraint (way area and off-critical-path timing), delegating latch counts to Table 2.

---

## Pair 6: Weak-Human Dead Passive Wall (Methodology) -> Active Engineering Prose

**Before (Class A: 6 consecutive passive sentences, 85 words):**
> An aggressive branch predictor was chosen to not unduly penalize Deep Pipe. Performance simulations were run using gem5 [5], fast forwarding for 1 billion instructions and executing for 1 billion instructions. Frequency for a given voltage was determined by the linear scaling in [2]. Nominal dynamic and static power overheads were determined using the simulation results and McPAT [19]. Low supply voltage dynamic power was scaled quadratically with respect to voltage [32]. Low supply voltage static power was scaled cubically with respect to voltage [32].

**After (Active `We` verbs, `16w -> 24w -> 8w -> 16w` contour, 25% tighter):**
> We model an aggressive TAGE predictor so branch mispredictions do not mask Deep Pipe's pipeline effects. Using gem5 [5], we fast-forward each benchmark for 1 billion instructions, simulate the next 1 billion instructions, and feed activity counts into McPAT [19]. We derive per-voltage frequency via linear scaling [2]. At low supply voltages, we scale dynamic power quadratically and static power cubically with voltage [32].

**Diagnostics:**
- Broke a 6-sentence dead passive wall (`was chosen ... were run ... was determined ... was scaled`) into 4 direct active sentences (`We model`, `we fast-forward...`, `We derive`, `we scale`).
- Preserved every methodological parameter and citation while cutting word count from 85 words to 64 words with a plain 8-word middle statement.

---

## Pair 7: Weak-Human Bar-Chart Narration & AI Cheerleading -> Regime Attribution + Honest Regression

**Before (Alphabetical bar reading + false precision + AI cover-up of losing bars):**
> Figure 10 shows the speedup across all benchmarks. The first application is `axpy`, which gets 1.03×. The second application is `blackscholes`, which achieves 1.12×, while `lavamd` achieves 1.38× and `mcf` achieves 2.41×. Overall, our design consistently achieves superior performance with a speedup of 1.5472× and up to 2.4138×, confirming the substantial effectiveness of our approach.

**After (`SK-8`, regime clustering, paired geomean + `up to`, honest regression, clean stop):**
> Across all 16 benchmarks (Figure 10), SALP-2 improves performance by 18.4% on average (geomean) and up to 2.4× on `mcf`. The speedup splits cleanly by memory intensity. Workloads gaining more than 10% average 18.4 MPKI and 15.2 WMPKI, where bank conflicts stall row activation; compute-bound benchmarks such as `axpy` and `blackscholes` average 1.1 MPKI and stay within 3% of baseline. On two streaming kernels (`stream` and `triad`), SALP-2 regresses by 2.1% because subarray interleaving slightly lowers row-buffer hit rate.

**Diagnostics:**
- Replaced alphabetical bar-reading (`The first application is...`) with microarchitectural regime clustering (`18.4 MPKI` vs `1.1 MPKI`) introduced by a plain 7-word observation.
- Killed false 4-decimal precision (`1.5472×`, `2.4138×`), cheerleading (`consistently achieves superior performance`), and trailing `, confirming the substantial effectiveness`.
- Paired `up to 2.4×` cleanly with `18.4% on average (geomean)` (without a trailing participle), reported the 2.1% regression with its exact hardware cause, and stopped cleanly once the last technical fact landed (zero em-dash editorial moral).

---

## Pair 8: Laundry-List Related Work & Combative Dismissal -> Design-Axis Taxonomy

**Before (Author-by-author list + sweeping attack + bare citation):**
> [56] conducted pioneering work that introduced a brute-force strategy for DRAM mapping recovery. Wang et al. [65] proposed a knowledge-assisted approach to shrink the search space. Jattke et al. [30] extended this strategy to AMD platforms. However, all prior works fail on modern systems and suffer from high manual effort. To the best of our knowledge, our method is the first to solve this problem seamlessly.

**After (Taxonomic grouping, plain sentence-initial `However,`, Cover-Up clean citations):**
> Prior DRAM reverse-engineering tools recover bank functions either by brute-force timing sweeps over physical address pairs [56] or by constraining the search with platform-specific heuristics [30, 65]. Both families work well on DDR4 controllers with narrow XOR functions. However, DDR5 controllers add bank groups and wider multi-bit XOR masks, which cause heuristic templates to miss valid functions and brute-force sweeps to stall. Our solver keeps the row-buffer conflict primitive from prior work [56] but replaces exhaustive search with a linear-constraint formulation that recovers DDR5 mappings without platform-specific templates.

**Diagnostics:**
- Fixed the bare citation subject (`[56] conducted...`) and replaced 3 consecutive `Author et al.` sentences with a two-branch mechanism taxonomy (`brute-force timing sweeps` vs `platform-specific heuristics`).
- Replaced combative dismissal (`all prior works fail`) and Tier-1 fluff (`seamlessly`) with generous 10-word scoping (`Both families work well on DDR4...`), followed by a plain sentence-initial `However,` explaining the exact DDR5 hardware shift.

---

## Pair 9: Bloated AI Conclusion (Abstract Echo + Slogan Hype) -> Crisp Single-Paragraph Verdict

**Before (Abstract copy-paste + zero numbers + grandiose vision slogan):**
> In conclusion, this paper has presented FastTTS, a holistic and comprehensive framework designed to tackle the critical challenges of deploying reasoning LLMs on edge devices. Through three novel synergistic techniques, FastTTS significantly enhances serving efficiency and seamlessly bridges the gap between cloud-scale models and edge hardware. Our extensive evaluation demonstrates that FastTTS consistently delivers superior throughput and substantial latency reductions across diverse workloads. Ultimately, this work paves the way for future hardware-software co-design and advances the vision of democratized agentic AI.

**After (96 words, 5 past-tense sentences, `23w -> 23w -> 27w -> 11w -> 12w` contour, zero hype):**
> Test-time scaling makes small edge models viable for complex reasoning, but naive serving wastes KV-cache capacity and stalls decoding under bursty tree search. We presented FastTTS, a runtime and memory-management system that groups sibling beams to cut prefix evictions and adapts draft budgets to per-query difficulty. Across four open-weight reasoning models on an edge GPU, FastTTS raised serving goodput by 2.2× (geomean) and cut median latency by 38% to 68% without altering accuracy. These gains assume multi-path reasoning; single-path greedy decoding sees negligible change. Our implementation adds 1,400 lines of C++ without kernel or hardware changes.

**Diagnostics:**
- Purged 12 Tier-1/Tier-2/structural AI tells (`In conclusion`, `holistic`, `comprehensive`, `critical challenges`, `three novel synergistic techniques`, `enhances`, `seamlessly`, `consistently`, `substantial`, `diverse`, `paves the way`, `democratized agentic AI`).
- Replaced zero-number hype with verified end-to-end metrics (`2.2×` geomean, `38% to 68%`, `1,400 lines of C++`) and an explicit scope boundary (`single-path greedy decoding sees negligible change`).
- Closed with two plain factual statements (`11w`, `12w`) in past tense with zero Abstract copy-paste.

---

## Pair 10: Try-Hard Anti-AI Over-Correction -> Relaxed Authentic Human Prose

**Before (Class C: theatrical slogan opener, em-dash bursts & dramatic closer, mid-clause `, however,`, stacked hyphen compounds, elevated thesaurus verbs):**
> FlexCache replaces fixed partitioning with runtime reconfiguration. The shared L2 serves as the primary bottleneck for co-running workloads — memory-intensive, streaming, and latency-sensitive jobs alike — because static way partitioning locks idle ways away from active threads. Dynamic way-stealing schemes, however, exhibit eviction-induced miss-rate inflation prior to phase convergence. Built atop a lightweight miss-counter array alongside per-core shadow tags, FlexCache employs a 16-entry epoch tracker that permits fast reallocation and attains 96% of oracle hit rate. Static allocation, however, still wins on uniform compute-bound mixes. Table 3 explains why — only 12% of workload intervals actually need way migration, compelling strict hysteresis.

**After (Relaxed plainspoken register, natural `However,`, zero em-dashes, unpacked compounds, zero tail stutters):**
> Static way partitioning in a shared L2 cache can hurt co-running workloads (such as streaming and latency-sensitive workloads) because idle cache ways are locked away from active threads. However, dynamic way partitioning often increases L2 misses when cache ways move between workloads before a phase change finishes. FlexCache tracks L2 misses with per-core miss counters and shadow tags, and uses a 16-entry epoch table to update the L2 cache partition. Across mixed workloads, this controller reaches 96% of the oracle L2 hit rate.
>
> Table 3 shows one exception. On uniform compute-bound workloads, static way partitioning still gives a higher L2 hit rate than dynamic way partitioning. Only 12% of intervals require moving cache ways in those workloads, so FlexCache waits before updating the L2 cache partition.

**Diagnostics:**
- Cut the theatrical copywriting slogan (`FlexCache replaces fixed partitioning with runtime reconfiguration.`) and dramatic em-dash closer (`Table 3 explains why — ...`), reducing em-dashes from **3** to **0** (using plain parentheses and a plain 5-word factual lead-in `Table 3 shows one exception.`).
- Removed both smuggled postpositive `, however,` clauses: converted the first to plain sentence-initial `However,` and opened a clean second paragraph for the uniform compute-bound exception (zero ping-pong `However,` inside one paragraph).
- Replaced every elevated-register thesaurus verb/preposition (`serves as`, `exhibit`, `prior to`, `Built atop`, `alongside`, `employs`, `permits`, `attains`, `compelling`) with plain core English (`can hurt`, `increases`, `before`, `tracks`, `and`, `uses`, `reaches`, `waits`), unpacked `eviction-induced miss-rate inflation`, and avoided tail-to-head stuttering (`Given-New5 = 0.40`, `0.0` AI watchlist, `0.0` em-dashes).

---

## Pair 11: Mid-Paper Textbook Recap & Neat Symmetry -> In-Flow Architecture Prose

**Before (Mid-paper Section 6 Evaluation re-expands 4 already-defined acronyms, opens with a standalone system recap, mirrors `Two X... / Two Y...` across paragraphs, forces `First,... Second,... Third,...`, and appends `, leaving`):**
> In modern datacenter servers, TierMem is a hardware-software memory tiering system that manages Compute Express Link (CXL) memory alongside High Bandwidth Memory (HBM) using a Metadata Tracking Pool (MTP) and a Latency-Aware Replacement Table (LRT). Two memory-system advantages drive TierMem's throughput gains in Figure 8. First, the MTP keeps hot pages in HBM with 94% accuracy. Second, the LRT batches cold-page migrations to CXL during idle bus windows. Third, asynchronous writebacks overlap page copies with core execution, leaving negligible stall overhead on the critical path.
>
> Two architectural properties preserve low hardware cost across all 12 workloads. The MTP occupies 64 KB per socket and tracks only 2 MB superpages, while the LRT uses a 4-way direct-mapped table. Thus, TierMem achieves both high throughput and low area across diverse server applications.

**After (Enters directly in-flow using already-defined acronyms, organic openings, finite clauses, zero tail stutter):**
> Figure 8 compares TierMem against static HBM pinning and software page migration across 12 workloads. TierMem stays within 4% of an all-HBM system on average because MTP keeps hot 2 MB pages in HBM with 94% accuracy while LRT batches cold 2 MB page migrations to CXL during idle bus windows. Asynchronous writebacks are also used to overlap page copies with execution, so migration stalls add less than 1.2% to execution time.
>
> Hardware cost stays low across these 12 workloads. Because MTP tracks 2 MB pages instead of 4 KB pages, MTP needs only 64 KB per socket. LRT fits in a 4-way table off the L3 hit path, so its lookups add no latency to L3 hits.

**Diagnostics:**
- Removed the mid-paper textbook system recap and stopped re-expanding `CXL`, `HBM`, `MTP`, and `LRT` (already introduced in Sections 1–4); opened directly inside the Evaluation thread with `Figure 8 compares...` and progressed directly to `TierMem stays...` without stuttering `"Across these 12 workloads,"`.
- Eliminated the mirrored paragraph openers (`Two memory-system advantages drive...` / `Two architectural properties preserve...`) and the unprompted `First, ... Second, ... Third, ...` listification.
- Converted the trailing participle `, leaving negligible stall overhead` into a finite clause (`so migration stalls add less than 1.2% to execution time`) and deleted the empty summary closer (`Thus, TierMem achieves...`), letting paragraph 2 stop cleanly on its final technical fact (`0.0` AI watchlist, `0.0` em-dashes).

---

## Pair 12: Tail-Stutter Given-New, Mirrored Sentence Templates & Stripped Modals -> Natural Human Engineering Flow

**Before (Deep-discourse tells: literal tail-to-head Given-New stutters `...shared across 16 cores. Because 16 cores share...` & `...all 16 banks. Across all 16 banks,...`; mirrored consecutive sentence templates `On read requests... / On write requests...` & `During light load... / During heavy load...`; absolute modals `eliminates` / `guarantees` / `directly produce` + editorial gloss):**
> In a multi-core processor, the coherence directory is shared across 16 cores. Because 16 cores share the same coherence directory, snoop lookups serialize across all 16 banks. Across all 16 banks, directory bandwidth saturates whenever memory-intensive threads run together, showing why centralized tracking falls short. On read requests, a directory miss sends a probe to the owner core. On write requests, a directory miss invalidates every sharer before granting ownership.
>
> Our banked snoop filter eliminates unnecessary coherence lookups and guarantees zero bandwidth saturation. During light load, filter checks complete in two cycles. During heavy load, filter checks still avoid off-chip probes and directly produce the full 19% speedup, which confirms the efficiency advantage of distributed filtering.

**After (Bounded Given-New flow without tail stutters, asymmetric grammatical entry, calibrated modals, zero editorial gloss):**
> In a 16-core processor, a single coherence directory is shared across all cores, so concurrent snoop lookups often serialize at the directory banks. Under memory-intensive workloads, bank bandwidth can saturate quickly. A read miss forwards a single probe to the owner core, whereas handling a write miss requires invalidating all active sharers before the requester gets ownership.
>
> Adding a banked snoop filter can cut many of these coherence lookups and typically keeps bank bandwidth below saturation. Filter lookups take two cycles at light load. Even under heavier sharing, the filter avoids most off-chip probes and can help recover up to 19% speedup (11% geomean) over the baseline directory.

**Diagnostics:**
- Eliminated both literal tail-to-head Given-New stutters (`...shared across 16 cores. Because 16 cores share the same coherence directory` and `...across all 16 banks. Across all 16 banks,`), bringing lead-5 chaining cleanly into natural human range (`0.50`, zero `>= 3`-word tail repeats) while letting half the sentence boundaries advance directly to the next technical fact.
- Broke both pairs of mirrored consecutive sentence frames (`On read requests... / On write requests...` -> asymmetric `A read miss forwards..., whereas handling a write miss requires...`; `During light load... / During heavy load...` -> asymmetric `Filter lookups take two cycles at light load. Even under heavier sharing, the filter avoids...`).
- Restored calibrated engineering modals (`often serialize`, `can saturate`, `can cut`, `typically keeps`, `can help recover`) in place of absolute overclaims (`eliminates`, `guarantees zero`, `directly produce the full 19%`), paired `up to 19%` with `11% geomean`, and deleted both editorial-gloss tails (`showing why centralized tracking falls short`, `which confirms the efficiency advantage of distributed filtering`).

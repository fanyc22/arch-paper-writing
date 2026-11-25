# Intra-Paragraph Logic, Cohesion, and Information Flow

> **Scope**: **Universal** — applies identically to 10–15p conference papers, 2–4p Letters (e.g., IEEE CAL), workshop papers, rebuttals, and single paragraphs. *(Macro per-100-sentence rates scale proportionally in short pieces: e.g., `<= 1` explicit transition adverb per 2–3 paragraph block.)*

Strong computer architecture prose succeeds or fails at the paragraph boundary. Individual sentences that are grammatically spotless still collapse into flat prose when they orbit a topic word without advancing the technical state. Treat every paragraph as a **directed causal chain** whose sentence order is locked by physical, architectural, or logical dependency—never a flat cloud of parallel restatements, and never a choppy sequence of disconnected staccato claims.

---

## 1. The Eight Canonical Intra-Paragraph Skeletons (`SK-1`–`SK-8`)

Build core paragraphs around one of these eight directed skeletons rather than improvising sentence by sentence.

| ID | Skeleton | Primary Sections | Directed Sentence Arc |
| :---: | :--- | :--- | :--- |
| **`SK-1`** | **Dual-Constraint Tension Closure** | Abstract, Intro | Baseline dual goal (`X + Y`) -> Existing mechanism achieves `X` -> Pivot: breaks `Y` -> Proposed design closes both `X` and `Y` |
| **`SK-2`** | **Physical Root-Cause Cascade** | Intro, Motivation | Macro symptom or root cause -> Hardware structure -> Triggering action -> Physical amplification -> System-level failure |
| **`SK-3`** | **Split-Topic Strawman Elimination** | Intro, Motivation | Intuitive direction -> Announce `K` paths, all costly -> Path 1 -> circuit/HW cost 1 -> Path 2 -> cost 2 -> Path `K` -> scalability verdict |
| **`SK-4`** | **Short-Pivot Reframing** | Abstract, Intro | Mainstream mechanism seems appealing -> Real mechanism flaw -> Workload consequence -> **Plain short (`<=12w`) pivot rejecting the premise** -> Inverted architectural insight |
| **`SK-5`** | **Concrete Trace -> Structural Bottleneck** | Background, Motivation | Abstract program property -> Concrete figure/node/instruction trace proving failure -> Conventional software workaround -> False dependence or HW bottleneck |
| **`SK-6`** | **Hardware State-Machine Walkthrough** | Design | Module role -> State register/counter & update rule -> Gating condition / action -> Quantitative or timing consequence -> Runtime benefit or contrast |
| **`SK-7`** | **Invariant -> Race Boundary -> Liveness Proof** | Design | Core invariant or transaction rule -> Common safe path -> Pivot: corner-case race / violation boundary -> Counterexample or retry/bounce mechanism -> No-starvation / correctness closure |
| **`SK-8`** | **Diagnostic Attribution & Risk Audit** | Evaluation | **(A) Anomaly Detective:** Headline trend -> Surprising reversal -> Plain diagnostic question -> Multi-step circuit/HW root cause. **(B) Additive Ablation:** Total gain -> Component 1 (`Δ1`) -> Component 2 (`Δ2`) -> Component `K` (`ΔK`). **(C) Risk/Outlier Verdict:** Reviewer worry or outlier -> Exact HW mechanism -> Targeted measurement -> Bounded verdict |

---

## 2. The Zero-Redundancy Delta Law

Every sentence $S_{i+1}$ inside a paragraph must advance the technical argument by **at least one concrete, non-deletable delta** relative to $S_1 \dots S_i$. Choose from eight atomic roles:

1. **`Mechanism`**: Introduces a concrete hardware unit, data structure, protocol message, or execution action.
2. **`Physical Cause`**: Explains *why* a phenomenon happens at the circuit, microarchitectural, or OS level.
3. **`Quantitative Anchor`**: Pins down a measured number, scaling threshold, equation bound, or real-system fact.
4. **`Consequence`**: Derives the downstream latency, bandwidth, energy, area, or correctness effect.
5. **`Contrast Pivot`**: Reverses expectation, exposes a hardware conflict, or flags an inflection point.
6. **`Elimination`**: Rules out a plausible alternative via a concrete physical constraint (die area, pin count, electrical load, critical-path delay)—never vague labels like "impractical."
7. **`Boundary / Caveat`**: Specifies a precondition, assumption scope, degradation regime, or fallback path.
8. **`Next-Step State`**: Advances a multi-cycle protocol, queue, or pipeline state machine to its next invariant.

**Hard Bans**:
- **Zero Paraphrase Echoes**: Never write an $S_{i+1}$ that re-skins $S_i$ in different words (`enables more effective debugging` -> `facilitates transparent and efficient bug identification`). If two adjacent sentences add no distinct hardware entity, state transition, or number, **delete one or fuse them**.
- **Zero Theatrical Slogan Openers or Editorial Summary Closers**: Never open a paragraph with a punchy copywriting headline (`System X replaces fixed capacity with runtime reconfiguration.`) that merely previews the next sentence, and never append a tidy editorial wrap-up moral or dramatic reveal (`Table 4 explains why — only a fraction...`). **Stop the paragraph as soon as the last technical fact lands.**

---

## 3. Given-New Subject-Anchor Law, Terminology Lock, and Anti-Symmetry

Cohesion comes from chaining known concepts forward in plain, consistent language.

### Theme-Rheme Chaining Mechanics (Bounded — Never Stutter!)
- Place the **new entity, state, or variable** near the end of $S_i$ (its *Rheme*), and pick up that concept inside the opening 1–5 words of $S_{i+1}$ (its *Theme*) **when the next step naturally builds on it**.
- **Bounded Target**: **`35–48%`** direct lead-5 lexical chaining across adjacent sentences (rewrite trigger **`< 28%` disconnected** OR **`> 52%` verbal stuttering**). **Roughly 55% of sentence boundaries in real human papers progress naturally WITHOUT repeating a tail word in the opening 5 words**—advancing instead via the next physical step, a contrast (`However,`), a concrete measurement, or a constant topic. Do **not** force tail-to-head chaining on every boundary.
- **HARD BAN — The Tail-Stutter & Multi-Hop Stem-Echo Rule**: Never repeat a **`>= 3`-word phrase** from $S_i$'s tail, never mirror $S_i$'s `Subject + Verb` predicate at the start of $S_{i+1}$, and never chain the **same word stem across 3+ consecutive sentences** (`colocate -> colocating -> Such colocation -> this placement`):
  - *Bad (mirrored Subject+Verb stutter)*: `"...is shared across multiple cores. Because multiple cores share the same directory, snoop lookups serialize."` -> *Fix*: `"All cores share a single coherence directory, so concurrent snoop lookups often serialize at the banks."`
  - *Bad (`>= 3`-word tail stutter)*: `"...across all 16 banks. Across all 16 banks, bandwidth saturates..."` -> *Fix*: Delete the echoed preamble and state the new consequence directly (`"Bank bandwidth can saturate whenever..."`).
  - *Bad (3-hop stem echo)*: `"...colocate metadata near cores. Colocating metadata cuts latency. Such colocation also reduces..."` -> *Fix*: Advance directly to the next architectural actor or metric instead of re-deriving the same stem three times.
- **Permitted Non-`GN` Progressions**:
  - **Constant-Topic (`CT`)**: Reuse the same subject for at most **2–3 consecutive sentences**, provided each sentence adds a strictly orthogonal property or stage.
  - **Split-Topic (`ST`)**: Use only when the underlying design naturally splits into orthogonal paths. Always state the branch count and axis upfront (`three ways`, `two reasons`), then resume natural causal progression inside every branch.
- Use natural passive voice selectively when needed to pull a known entity into subject position.

### Terminology Lock & Shameless Plain-Term Repetition
- Lock one plain, concrete name per hardware block, bottleneck, or metric throughout a paragraph and across the paper (`subarray`, `wordline`, `rate limiter`, `range TLB`, `miss rate`, `latency`, `overhead`).
- Repeat plain core nouns and verbs (`is`, `has`, `uses`, `shows`, `adds`, `causes`, `reduces`, `stores`, `maps`) freely across adjacent sentences. **Never cycle synonyms** (`approach -> method -> strategy -> paradigm` or `outer-product formulation -> outer-product execution`) to avoid repetition—synonym cycling pushes `MATTR-100 > 0.70`, severs lexical chains, and sounds synthetic.
- **Pronoun & Ellipsis Balance Guardrail**: Locking core nouns and avoiding 4+ verb synonyms does **not** mean robotically echoing the exact same noun phrase or verb in every clause (`"As density drops, energy drops below X and drops below Y"`)—keep natural pronouns (`it`, `they`, `its` when the antecedent is unambiguous) and clean ellipsis (`"energy falls below X and then Y"`).

### Anti-Symmetry Rule (Paragraphs AND Consecutive Sentences)
- **Ban Mirrored Consecutive Sentence Templates**: Never clone syntactic openings across adjacent contrasting or case-split sentences (`"During X, ... / During Y, ..."`, `"On GPUs, ... / On CPUs, ..."`, `"A hit ... / A miss ..."`, `"When X ..., ... / When Y ..., ..."`). Give consecutive contrasting sentences **asymmetric grammatical entry** (e.g., `"A read miss forwards a probe to the owner core, whereas handling a write miss requires invalidating all active sharers."` or `"Filter lookups take two cycles at light load. Under heavier sharing, the filter still avoids most off-chip probes."`).
- **Ban Mirrored Paragraph Openings**: Never open consecutive paragraphs with cloned structural frames (`Two memory-system advantages drive...` followed by `Two architectural properties preserve...`).
- **Ban Unprompted `First, ... Second, ... Third, ...` Scaffolding**: Do not force organic multi-sentence prose into mechanical numbered lists unless the reader genuinely needs explicit branch tracking across several long clauses.

---

## 4. Bimodal Reference Discipline

Both weak human prose and LLM-polished prose break reference chains through opposite surface forms. Ban **both**:

| Failure Mode | Prohibited Pattern | Why It Fails | Target Cap |
| :--- | :--- | :--- | :---: |
| **Class A: Bare Pronoun** | `This is...`, `This allows...`, `This leads to...`, `It avoids...` | Leaves the antecedent ambiguous across multi-clause sentences or attaches to the wrong subject. | `<= 2.0%` of non-initial sents |
| **Class B: Hollow Shell Noun** | `This approach`, `This strategy`, `This method`, `This paradigm`, `These merits`, `These challenges`, `This finding`, `Such issues`, `This capability`, `This phenomenon` | Creates a syntactic illusion of cohesion without naming any real hardware object or physical event. | `<= 0.5%` of non-initial sents |

**Mandatory Grounding Pattern**: Write **`This / These / Such <concrete architectural entity or physical event>`**—using plain, short nouns rather than multi-hyphen stacks.
- *Weak (bare)*: `This avoids O(n) metadata storage.` -> *Grounded*: `TimeCache avoids O(n) metadata storage.`
- *Weak (hollow shell)*: `This strategy preserves frequency isolation.` -> *Grounded*: `Keeping total segment count fixed preserves the resonator's electrical length and frequency.`
- *Strong grounded anchors*: `This miss burst`, `This tag lookup`, `This writeback stall`, `This L2 stalling`, `Such voltage fluctuations`, `Such bounces`, `These queues`.

---

## 5. Natural Logical Pivots vs. Fake Glue (and Banning Staccato Prose)

Physical causality rests primarily on entity recurrence, intra-sentence subordination (`because`, `since`, `when`, `if`, `as`, `so long as`, `instead`), and state-variable handoffs (`counter -> count > 0 -> k/p`). At the same time, **real human architects DO use plain sentence-initial logical pivots** (`However,`, `Therefore,`, `Thus,`, `In contrast,`, `As a result,`, `For example,`) to guide the reader through turns in an argument.

### Two-Sided Quota on Logical Transitions
- **Target Band**: **`4–7` sentence-initial logical transitions per 100 sentences**—keep **`<= 1` explicit transition adverb per 2–3 paragraph excerpt** so you neither strip transitions to `0/100` staccato nor overshoot above `7.5/100`.
- **Ban Non-Contrastive `However,`**: Never insert `However,` between two additive or elaborative sentences—verify that $S_{i+1}$ genuinely overturns an expectation or trend set by $S_i$.
- **Ban Postpositive `, however,` Smuggling**: Do **not** hide `however` inside the middle of a sentence (`Way prediction, however, triggers...`; `Block prefetching, however, suffers...`) just to avoid opening a sentence with `However,`. **Hard cap: `<= 1` postpositive `, however,` per full section (`0` in short 2–3 paragraph excerpts).** Use plain sentence-initial `However,` or `But` instead.
- **Ban Fake Additive Glue**: Cap sentence-initial transitions at `<= 1` per paragraph (rewrite trigger `> 7.5/100` overall), **`0` stacked additive adverbs** (`Moreover`, `Furthermore`, `Additionally`, `In addition`) in the same paragraph, **`0` ping-pong `However,` pairs** in one paragraph, and **`0` conclusion adverbs stranded after `Note that...`**.

### Warranted Operator Trigger Matrix

| Operator | Legitimate Trigger (Keep & Use Naturally) | Reject When Used As Fake Glue |
| :--- | :--- | :--- |
| **`However,`** (or **`But`**) | True semantic reversal: prior sentence sets an expectation, assumption, or trend that this sentence overturns with a concrete constraint. | Jumping from generic domain hype ("LLMs achieve SOTA accuracy") to a latency problem with no actual contradiction. |
| **`Instead,`** | Strict binary replacement immediately following an explicit negation (`cannot X`, `does not Y`). | Introducing an alternative when nothing was negated in the preceding sentence. |
| **`Therefore,` / `Thus,` / `Hence,` / `As a result,`** | Direct logical entailment from premises established in the immediately preceding 1–2 sentences. | Launching a generic slogan ("Therefore, hardware co-design is needed") or jumping across an intervening caveat. |
| **`In contrast,`** | Symmetric comparison of Entity A vs Entity B along the **exact same dimension**. | Comparing different dimensions (e.g., accuracy in $S_1$, latency in $S_2$). |
| **`For example,` / `For instance,`** | Grounding an abstract mechanism in a specific instruction sequence, trace node, workload, or number. | Dropping concrete examples in favor of abstract recap sentences (`Notably, ...`). |
| **`Moreover,` / `Furthermore,` / `Additionally,`** | Rare, strictly orthogonal second constraint (keep `Additionally,` near zero; never stack two in one paragraph). | Appending a paraphrase echo, padding a flat list, or bolting a late reviewer note onto an unrelated paragraph. |

---

## 6. Single-Abstraction-Band Law

Partition architectural prose into four abstraction bands:
- **`B1` (Macro / Domain)**: Workload trends, datacenter economics, threat models.
- **`B2` (System / Workload)**: End-to-end throughput, tail latency, MPKI regimes, OS/compiler interfaces.
- **`B3` (Microarchitecture / Protocol)**: Queues, tables, coherence transactions, pipeline stages, schedulers.
- **`B4` (Circuit / Bit-Level)**: Wordline voltage, charge pumps, bit widths, gate delays, algebraic terms.

**Monotonicity Rule**: A single paragraph may span **at most two adjacent bands** (`B1->B2`, `B2->B3`, `B3->B4`) and must move **monotonically** (clean zoom-in or zoom-out). Never whiplash `B1 -> B4 -> B1` inside one paragraph, and never graft cross-subsystem numbers onto an unrelated paragraph via `Additionally,`.

---

## 7. Natural Role-Coupled Sentence Length (Plain Short Sentences, Not Slogans)

Natural human rhythm varies sentence length according to technical job—neither a flat `20–22w` conveyor belt nor theatrical op-ed staccato:

| Logical Role | Typical Length | What Authentic Human Prose Actually Looks Like |
| :--- | :---: | :--- |
| **Plain Fact / Scope Bound / Figure Pointer / Direct Pivot** | **`7–13` words** | Plain, workaday technical statements: `"Figure 3 shows this behavior."`, `"We use a 4-level page table."`, `"This cost grows with core count."`, `"We argue that this is not a fundamental limitation."` |
| **Quantitative / Concrete Anchor** | **`10–20` words** | States a measured regime threshold, workload fact, or system boundary cleanly without fanfare. |
| **Mechanism / Causal Chain / Ablation** | **`18–35` words** | Carries complete state conditions, timing dependencies, and hardware causality at unhurried pacing (up to ~40w when a single unified invariant or multi-part hardware path requires it). |
| **Paragraph Close** | **Natural length** | Stop as soon as the last technical fact lands—do **not** bolt on an engineered summary punchline. |

**Anti-Slogan & Anti-Checklist-Stiffness Guardrail**: Never inject a short sentence only to hit a burstiness ratio, and never let rule-checking flatten every sentence into a cautious `16–22w` box (`SD < 7.5w`). If a short sentence reads like a marketing tagline (`"FlexCache replaces fixed capacity with runtime reconfiguration."`) or duplicates the next sentence, delete it or fold it into the mechanism sentence. At the same time, let complex multi-step hardware explanations run organically to **`26–38` words** (using natural inline parentheticals or `because`/`where`/`when` clauses) next to plain **`8–13` word** factual statements so prose breathes naturally (`SD ~8.5–11.5w`, `CV ~0.35–0.55`).

# Surgical Anti-AI, Anti-Over-Correction, and Anti-Bad-Human Playbook

> **Scope**: **Universal** — applies identically to all computer architecture writing lengths and formats (full papers, 2–4p Letters, workshops, rebuttals, excerpts).

Publication-grade computer architecture prose must avoid **three distinct failure basins**:
- **Class B (Classic LLM-Drifted Prose)**: Glossy buzzwords, elevated-register thesaurus swaps, unnaturally scrubbed passive voice (`< 15%`, or `~16%` paired with hollow active wrapper verbs), trailing participle slogans, hollow shell nouns (`This approach`), synonym cycling, and uncritical cheerleading.
- **Class C (Try-Hard Anti-AI Over-Correction)**: Over-correcting anti-AI rules into robotic `0/100` staccato prose, mid-clause `, however,` smuggling, em-dash bursts, theatrical punchline slogans, compressed hyphenated noun stacks, mechanical same-word repetition, and tidy editorial wrap-ups.
- **Class A (Weak Human Prose)**: Dead passive datasheet walls (`> 27%`), heavy nominalization, RTL bit-level sprawl in running text, bare ambiguous `This is`, alphabetical bar-chart narration, non-native calques, and defensive reviewer patches.

Enforce all three boundaries simultaneously so prose lands squarely in relaxed, plainspoken senior-architect voice.

---

## 1. Tier 1 Hard Ban (Zero Tolerance — AI Lexicon Red Cards)

Eliminate every token and phrase below unconditionally, **with one strict domain exception**: legitimate hardware/system proper nouns (e.g., ARM CCA's `Realm` / `Realm Management Extension (RME)`, Google's `REALM`), verbatim quoted titles, or rare negated scope statements (`we intentionally do not delve into...`).

- **Banned Verbs**: `delve` / `delving`, `underscore` / `underscores` / `underscoring`, `foster` / `fosters`, `transcend` / `transcends`, `empower` / `empowers`, `streamline` / `streamlines`, `unveil` / `unveils`, `unravel`, `harmonize` / `harmonizing`, `democratize` / `democratizing`, `captivate` / `captivated`, `scrutinize`, `orchestrate` / `orchestrates`, `pave the way` / `paving the way`.
- **Banned Adjectives & Adverbs**: `pivotal`, `paramount`, `nuanced`, `multifaceted`, `holistic`, `seamless` / `seamlessly`, `intricate`, `synergistic`, `meticulous` / `meticulously`, `ever-evolving`, `groundbreaking`, `transformative`, `valiant`, `breakthrough` (as self-praise).
- **Banned Wrapper Metaphors & Macro Openers**: `tapestry`, `linchpin`, `synergy`, `landscape` (metaphorical), `pillars` / `planes` / `realms` (as abstract wrappers), `in recent years`, `in the past decade`, `play a crucial/pivotal role`, `delicate balance`, `has recently emerged as a promising candidate`, `Despite its great potential`, `killer computer applications`, `broader landscape`.

> **Multi-Signal Guardrail (Avoiding False Positives)**: When auditing existing drafts, never flag a legitimate domain proper noun (`ARM CCA Realm`, `Google REALM`) or an isolated literal technical adjective (`size-preserving for seamless interoperation`) as AI prose on its own. Trigger mandatory rewrites whenever any high-specificity cliché phrase appears (`in the intricate realm of`, `harmonizing the delicate balance`, `marks a pivotal advancement`) or whenever `>= 2` independent signals co-occur in the same paragraph.

---

## 2. Tier 2 Over-Use Watchlist (Replace Unless Literally Technical)

Replace every token below with a concrete verb, explicit quantifier, or plain human word unless its literal technical sense is strictly required.

> **Pass-1 Source-Note Normalization Rule**: Rough author outlines, bullet notes, and draft tables frequently contain Tier-2 tokens (`consistently`, `solely`, `substantial`, `confirming`, non-security `mitigate`). **Normalize them into plain concrete English during Pass 1**—never copy Tier-2 phrasing verbatim from input notes into manuscript prose.

| Watchlist Token | Why It Triggers AI Detection | Required Replacement Strategy |
| :--- | :--- | :--- |
| **`diverse`** | Replaces concrete workload characterization. | Name exact workload classes or counts (`12 memory-bound and compute-bound traces`). |
| **`enhance / enhances / enhancing`** | Hollow wrapper verb hiding real mechanism effects. | Use `improve`, `raise`, `increase`, or state the exact delta (`cuts tail latency by 18%`). |
| **`facilitate`** | Bureaucratic filler replacing hardware actions. | Use `support`, `allow`, `let`, `simplify`, `carry out`. |
| **`comprehensive`** | Empty boast replacing evaluation scope. | State exact coverage (`across 158 production traces and 3 DRAM speeds`). |
| **`subsequently`** | Stiff LLM temporal filler. | Use `then`, `next`, or anchor the trigger (`after the writeback completes`). |
| **`confirming`** (trailing) | Participial summary crutch. | Use a finite clause stating what the measurement verifies. |
| **`consistently`** | Cheerleading adverb; fatal if any bar loses or ties. | Give the exact win ratio (`faster on 14 of 16 benchmarks`) and explain exceptions. |
| **`conversely`** | Over-formal contrast marker. | Use `in contrast`, `whereas`, or `unlike`. |
| **`mitigate`** | Over-applied outside security/reliability. | Reserve for security/RowHammer/faults; otherwise use `reduce`, `hide`, `mask`, `amortize`, `cut`. |
| **`solely`** | Inflated substitute for plain English. | Use `only`. |
| **`inherently`** | Hand-waves away physical causes. | State the physical reason (`because banks share global I/O drivers`). |
| **`essential` / `crucial`** | Asserts importance without proof. | Use `required`, `needed`, or show the ablation drop without the component. |
| **`tailored`** | Promotional modifier. | Use `specialized for`, `configured for`, `built for`, `tuned to`. |
| **`substantial` / `significant`** | Vague substitute for real numbers. | Replace with the actual measurement (`38%`, `2.1×`, `1.4 mm²`). |
| **`leverage` / `utilize`** | Overused hollow substitutes for `use`. | Use `use`, `exploit`, `rely on`, `read`, `index` (keep `utilize` only for hardware utilization). |
| **`Additionally,` / `Notably,`** | Top AI sentence-opener crutches. | Delete and chain the previous sentence's concrete noun; use `Note that...` sparingly instead of `Notably,`. |
| **`novel`** | Self-congratulatory filler. | Cap at `<= 1` per paper (target `0`); let the concrete mechanism demonstrate novelty. |

---

## 3. Structural AI Tells to Eliminate

1. **All Tacked-On Trailing Participle Clauses**: Eliminate not only `, ensuring ...`, `, enabling ...`, `, thereby ...ing`, `, allowing ...`, `, confirming ...`, and `, highlighting ...`, but **ANY tacked-on result participle appended to a complete clause**: **`, leaving ...`, `, totaling ...`, `, violating ...`, `, yielding ...`, `, creating ...`, `, causing ...`, `, making ...`, `, resulting in ...`, `, forcing ...`, `, reducing ...`**.
   - *Fix*: Split into a clean finite clause (`so ...`, `which ...`, `and ...`, or a new sentence), or move the cause inside with `because` / `since`.
2. **Mechanical `Not only X, but also Y`**: Replace with two direct finite predicates (`cuts LLC misses by 24% and trims DRAM energy by 19%`).
3. **Symmetrical Rule-of-Three & Mirrored Templates (Sentence AND Paragraph Level)**: Ban generic application triplets (`healthcare, autonomous driving, and defense`), **mirrored consecutive sentence frames** (`"During X, ... / During Y, ..."`, `"On GPUs, ... / On CPUs, ..."`, `"A hit ... / A miss ..."`, `"When X ..., ... / When Y ..., ..."`), mirrored paragraph openings (`Two memory advantages drive...` / `Two architectural properties preserve...`), unprompted `First, ... Second, ... Third, ...` scaffolding, and `Challenge I / II / III` colon cloning. Give consecutive contrasting sentences asymmetric grammatical entry.
4. **Evaluation & Datapath Verb Cycling**: Rotating 4+ distinct verbs for the same quantitative trend (`reaches / surpasses / climbs to / overtakes / crosses below`) or datapath movement (`traverse / cross / pass through / travel across`) inside one paragraph. Reuse 1–2 plain verbs (`is`, `achieves`, `drops to`, `crosses`, `reduces`) cleanly—without starving natural pronouns or ellipsis (see Section 4, Trap 8).
5. **Pleonasms, Synonym Doublets, Essay-Gloss Idioms & Unused Acronyms**:
   - **Pleonasms & doublets**: Ban `"up to X% at maximum"`, `"fixed and provisioned"`, `"physical spatial locality"`, `"strongly outperform"`, and redundant colon restatements (`"two register pairs: one register pair for X and one register pair for Y"` -> `"one register pair for X and one for Y"`).
   - **Textbook / essay-gloss idioms**: Ban `"Conventional X wisdom holds"`, `"operate in a very different regime"`, `"underlying hardware substrates"`, `"a surprisingly high payoff"`, `"inevitably"`, `"at its core"`, and `"in a fundamentally different way"`.
   - **Use-It-Or-Drop-It acronyms**: Never introduce `(ILP)`, `(MLP)`, or any other acronym unless it is reused at least once more in the same section or Abstract.
6. **Editorial Gloss & Epistemic Modal Stripping**:
   - Ban tacked-on interpretive gloss telling the reader what a clean measurement or mechanism means (`"showing why static partitioning falls short"`, `"which confirms the efficiency advantage"`). State the hardware mechanism or number directly and move on.
   - Ban upgrading calibrated human engineering modals (`can`, `may`, `often`, `typically`, `in practice`, `tends to`, `can help`, `we evaluate this option`) into absolute universal assertions (`prevents`, `guarantees`, `directly produces`, `reaches full utilization`, `eliminates`).
7. **Cliché Problem Bridges & Extinct Roadmaps**: Ban `"However, prior works suffer from..."`, `"Despite its great potential, ..."`, and `"The rest of this paper is organized as follows. Section 2 describes..."` (embed section anchors in the contribution list instead).
8. **Mid-Paper Textbook Recaps & Acronym Re-Expansion**: Inside Motivation, Design, or Evaluation, never re-expand acronyms already defined earlier in the paper and never prepend a standalone overview recapping the entire system. Enter directly inside the local technical thread.
9. **Empty Section Preambles & Frankenstein Seams**: Ban 80–130 word hype throat-clearers before `X.1`, and keep register uniform across Intro, Design, and Evaluation.

---

## 4. Class C: Try-Hard Anti-AI Over-Correction Tells (NEVER Do These!)

Applying anti-AI rules rigidly creates a distinct, instantly detectable "try-hard humanized AI" signature that **hurts** cohesion and still fails blind review. Avoid all eight traps:

| Class C Over-Correction Tell | What It Looks Like (Reject!) | Why It Fails | Authentic Human Fix |
| :--- | :--- | :--- | :--- |
| **1. Tail-Stutter & 3-Hop Stem Echoes (`> 52%` Lead-5)** | `"...shared across 16 cores. Because 16 cores share..."`, `"...across 16 banks. Across 16 banks, ..."`, or 3-hop chains (`colocate -> colocating -> Such colocation`). | Mechanical verbal echo that drags down cohesion; real human papers advance ~55% of boundaries without repeating tail words. | Keep lead-5 chaining in **`35–48%`**; **ban `>= 3`-word tail repeats, mirrored `Subject + Verb` preambles, and 3-hop stem echoes**—advance directly to the next step or actor. |
| **2. Staccato (`0/100`) OR Transition Overshoot (`> 7.5/100`)** | Zero pivots across 15+ sentences, OR stuffing 2+ transitions / non-contrastive `However,` into a short excerpt to overcompensate. | Reads either like stitched bullet notes or artificially padded prose. | Keep genuine sentence-initial pivots at **`4–7 / 100 sents`** (**`<= 1` per 2–3 paragraph excerpt**); use `However,` only on real logical reversals. |
| **3. Postpositive `, however,` Smuggling** | `"Way prediction, however, triggers..."`; `"Block prefetching, however, suffers..."` repeated across paragraphs. | Classic tell of avoiding sentence-initial `However,` artificially. | Hard cap **`<= 1` per full section (`0` in short excerpts)**; write plain sentence-initial `However,` or `But`. |
| **4. Em-Dash Bursts & Dramatic Reveals** | `> 1.5/1k` em-dashes, lists wrapped in `— ... —`, or `"Table 4 explains why — only a fraction..."` closers. | Reads like an op-ed essay rather than an architecture paper. | Target **`0.0–1.2/1k` (default `0` in 150–350w passages)**; use parentheses `(...)`, commas, or a clean period. |
| **5. Theatrical Slogans & Editorial Closers** | `"System X replaces fixed capacity with runtime reconfiguration."`; `"Bandwidth and latency directly collide."`; tidy wrap-up moral at paragraph end. | Manufactured copywriting rhythm that adds zero new technical fact. | Make short sentences plain workaday facts (`"Figure 3 shows this split."`); stop as soon as the last technical fact lands. |
| **6. Checklist Stiffness & Stacked Hyphen Compounds** | Flattening every sentence to `16–22w` (`SD < 7.5w`) while juggling rules, or packing prose `-10%` into dense stacks (`"eviction-induced miss-rate overhead"`). | Produces stiff, uniform cadence and telegraphic phrasing. | Stay relaxed (`~100%` pacing, **`SD 8.5–11.5w`**): let complex explanations run naturally to `26–38w` next to plain `8–13w` facts, and unpack stacked compounds into plain phrases. |
| **7. Elevated-Register Thesaurus Swaps** | Scrubbing Tier-1 words but still writing `serves as`, `built atop`, `permits`, `attains`, `prior to`, `alongside`, `undermine`, `resilience`, `yields`, `exhibits`, `employs`, `compels`. | Keeps `MATTR-100 > 0.70` and exposes LLM formality. | Use plain core English (`is`, `built on`, `allows`, `gets`, `before`, `with`, `hurt`, `protection`, `gives`, `shows`, `uses`, `forces`) and repeat core terms freely. |
| **8. Robotic Plain-Word Repetition (Anti-Synonym Over-Correction)** | Starving natural pronouns or ellipsis by literally repeating the same noun or verb 3+ times across one or two clauses (`"As density drops, energy drops below X and drops below Y"`, `"Local TLBs... yet local TLBs"`). | Over-corrects `MATTR` downward and sounds stilted and synthetic rather than plainspoken. | Keep natural pronouns (`it`, `they`, `its`) when the antecedent is unambiguous, use clean ellipsis (`"energy falls below X and then Y"`), or allow one plain shift (`drops -> falls`) while still banning 4+ verb cycles. |

---

## 5. Class A Weak-Human Anti-Patterns (Do Not Over-Correct Into These)

- **Dead Passive Walls**: `> 2` consecutive passive sentences or `> 27%` passive overall (`was chosen... were run... was determined...`). Use `We` or concrete hardware actors.
- **Nominalization & Nested-`of` Bloat**: `The freeing up of a physical register occurs in two cases` -> `The core frees a physical register in two cases.`
- **RTL Datasheet Sprawl**: Explaining binary comparison (`'1100' > '0101'`), pin wiring (`fed to 'a'`), or unmotivated bit widths in prose instead of a Storage/Config Table (`references/03-detail-and-abstraction.md`).
- **Bare Ambiguous Pronouns**: Floating `This is`, `This allows`, or `It avoids`.
- **Mechanical Bar-Chart Narration & Triplication**: Walking alphabetically down bars (`The first application is A...`) or repeating the same numbers in prose, table, and figure.
- **Decorative Pseudo-Math & Line-by-Line Pseudocode Narration**: Fake `argmax` wrappers, numbered subtraction (`A = B - C`), or translating `Line 1... Line 15` in prose.
- **Defensive Patches, Double Hedges, Combative Dismissals, & Calques**: Ban `because we do not innovate in this context`, `can potentially`, `All prior works fail`, `cannot but be`, `need not have to`, and `responsible of`.

---

## 6. Quick Replacement Table: Flagged Form -> Concrete Domain Form

| Prohibited / Flagged Form | Concrete Architecture Replacement |
| :--- | :--- |
| `In recent years, LLMs have revolutionized...` | `Serving 70B-parameter LLMs bottlenecks on HBM bandwidth during decode.` |
| `we delve into the inner workings of X` | `Section 4 details X` / `We next describe how X handles...` |
| `underscores the paramount importance of X` | `shows that X dominates latency (62% of stalls)` |
| `diverse workloads / comprehensive evaluation` | `18 SPEC CPU2017 and GAP workloads` / `evaluated on 158 traces` |
| `enhances / facilitates / mitigates latency` | `raises IPC by 21%` / `routes messages` / `hides memory latency` |
| `serves as / built atop / permits / attains` | `is` / `built on` / `allows` / `reaches` |
| `prior to / alongside / yields / exhibits / employs` | `before` / `with` / `gives` / `shows` / `uses` |
| `..., leaving / totaling / violating / ensuring ...` | `. This step leaves...` / `for a total of 134 workloads.` / `and violates...` |
| `Way prediction, however, triggers...` | `However, way prediction triggers...` |
| `Table 4 explains why — only 8% of pages...` | `Table 4 shows that only 8% of pages need mode switching.` |
| `eviction-induced miss-rate overhead` | `miss-rate overhead from extra evictions` |
| `...across 16 banks. Across all 16 banks, bandwidth...` | `...at the banks. Bank bandwidth can saturate...` |
| `On reads, a miss... On writes, a miss...` | `A read miss forwards..., whereas handling a write miss requires...` |
| `eliminates stalls, confirming the efficiency advantage` | `can cut most lookup stalls and typically keeps bandwidth below saturation.` |
| `reaches / surpasses / climbs to / overtakes / crosses below` | *(Repeat 1–2 plain verbs: `reaches`, `is`, `drops to`, `exceeds`.)* |
| `up to 30% at maximum` / `physical spatial locality` / `fixed and provisioned` | `up to 30%` / `spatial locality` / `fixed` |
| `Conventional wisdom holds...` / `underlying hardware substrates` / `a surprisingly high payoff` | `Prior designs assume...` / `hardware` / `a 28% latency reduction` |
| `two register pairs: one register pair for X and one register pair for Y` | `one register pair for X and one for Y` |
| `This approach / These merits / This challenge` | `This bank interleaving` / `This miss burst` / `This pin-count limit` |
| `consistently achieves superior performance` | `outperforms Base on 14 of 16 workloads (1.38× geomean); on two compute-bound apps...` |
| `was run using gem5... was determined via McPAT` | `We simulate workloads in gem5 [5] and model power with McPAT [19].` |
| `The freeing up of a register occurs when...` | `The core frees a register when...` |

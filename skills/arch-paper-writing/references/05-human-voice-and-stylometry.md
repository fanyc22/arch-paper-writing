# Human Voice, Stylometric Envelope, Naming, and Output Typography

> **Scope**: **Universal** — plainspoken register, burstiness, diction, modality, and LaTeX/citation hygiene apply to **all** computer architecture writing (full papers, 2–4p Letters, workshops, rebuttals). Full-section statistical targets (`~16–24%` passive, `per 1k` punctuation rates, `65–115w` average paragraph length) apply cleanly across multi-page prose; in 2p letters or 150–350w excerpts, single sentences swing percentages widely, so obey qualitative balance rather than rigid per-10-sentence ratios.

Authentic top-venue computer architecture prose sounds like a working systems engineer explaining a machine they built, measured, and debugged: plainspoken, unhurried, concrete, comfortable repeating core technical words, and skeptical of both marketing fluff and theatrical prose tricks. Avoid all three failure modes: classic LLM inflation, stiff passive datasheet walls, and try-hard anti-AI over-compression.

---

## 1. Target Stylometric Envelope

Calibrate drafted and edited sections against these quantitative targets from clean pre-2023 ISCA/MICRO/HPCA/ASPLOS prose.

| Metric | Target Band | Safe Range | Rewrite Trigger | Operational Guidance |
| :--- | :---: | :---: | :---: | :--- |
| **Sentence length mean** | `18–21` w/sent | `17–23` w | `< 15` or `> 25` w | Never impose a hard 25-word ceiling; unhurried precision beats artificial chopping. |
| **Burstiness (sent-length SD)** | **`8.5–11.5` w** | `8.5–13.5` w | **`< 7.5` w** | Avoid **Checklist Stiffness**: let complex hardware explanations run organically to `26–38w` (with natural parentheticals or `because`/`where`/`when` clauses) next to plain `8–13w` factual sentences—never flatten into `16–22w` runs and never manufacture slogans. |
| **Adjacent length delta** | **`9.5–11.8` w** | `8.6–14.3` w | **`< 7.5` w** | Break monotonous runs of 3+ identical-length sentences naturally. |
| **Length mix (`<=12` / `13–25` / `>30`w)** | `25–28%` / `46–52%` / `12–16%` | `20–34%` / `41–55%` / `8–24%` | Short `< 15%` or Med `> 65%` | Allow natural `30–40w` mechanism/invariant sentences; ban `>35w` trailing-participle chains. |
| **Paragraph length** | `3.5–5.5` sents / `75–105` w | `3.5–6.0` sents / `70–115` w | `> 7` sents or `> 145` w | Use bold `\paragraph{...}` signposts on `~8–15%` of paragraphs in full papers; keep natural `95–105%` length pacing without compressing. |
| **Given-New lead-5 chaining** | **`35–48%`** | `31–52%` | **`< 28%` or `> 52%`** | Bounded target: **~55% of boundaries advance naturally without repeating a tail word**; `> 52%` signals literal tail-to-head stuttering. |
| **Adjacent content Jaccard** | **`0.088–0.106`** | `0.081–0.113` | **`< 0.075`** | Repeat plain hardware nouns and verbs shamelessly instead of rotating synonyms. |
| **Lexical diversity (`MATTR-100`)** | **`0.64–0.68`** | `0.63–0.70` | **`> 0.70`** | **Anti-thesaurus guard**: `MATTR > 0.70` signals elevated-register synonym cycling that erases human voice and weakens cohesion. |
| **First-person `We/Our`** | `18–25` / 100 sents | `13–31` / 100 s | `< 10` / 100 s | Own design choices, hypotheses, and methodology actively (`We model`, `We find`). |
| **Passive voice** | **`16–24` / 100 sents** | `15–26` / 100 s | **`< 15` or `> 27`** (or `>2` in a row) | Keep natural hardware-flow passive (`is fetched`, `are buffered`); avoid both dead passive walls and glossy active-only prose. |
| **Initial logical transitions** | **`4–7` / 100 sents** | `3.0–7.5` / 100 s | **`0/100` (staccato) or `> 7.5`** | Keep `<= 1` explicit transition adverb per 2–3 paragraph excerpt; never insert non-contrastive `However,`; cap postpositive `, however,` at `<= 1`/section. |
| **Quantitative anchors** | **`2.0–3.2` / 100 w** | `1.4–4.3` / 100 w | Intro/Design `> 5.0` | Dense in Evaluation; restrained and purposeful in Intro and Design. |
| **Em-dashes** | **`0.0–1.2` / 1k w** | `0.0–1.5` / 1k w | **`> 1.5` / 1k w** | **Default ZERO in 150–350w passages**; never use for dramatic reveals or punchlines. |

> **Tight Em-Dash Envelope**: Keep em-dashes sparse (`0.0–1.2 / 1k` words, hard cap **`<= 1.5 / 1k`**). **Default to ZERO em-dashes in short 150–350 word passages**; prefer standard parentheses `(...)`, commas, or a separate sentence for asides and lists. Reserve rare em-dashes strictly for an indispensable inline definition in a full paper, and **never** use em-dashes for dramatic reveals or punchlines (`Table 4 explains why — ...`).

> **Short-Excerpt Calibration Note**: Full-paper ratios (passive %, sentence-length SD, `We/Our`) naturally have wider sampling variance across a 150–350 word excerpt (8–15 sentences). Never distort natural phrasing just to chase an exact 10-sentence passive percentage, and never over-compress a passage below `~95–105%` of its target length budget.

---

## 2. Plainspoken Engineering Register and Vocabulary Bank

### A. Shameless Plain-Term Repetition & Anti-Verb-Cycling (`MATTR-100 <= 0.68`)
Human architects repeat ordinary verbs and technical nouns freely across adjacent sentences because clarity beats literary variety. Reuse plain core words without apology:
- **Core plain verbs**: `is`, `has`, `uses`, `shows`, `causes`, `adds`, `reduces`, `increases`, `requires`, `stores`, `maps`, `reads`, `writes`, `keeps`, `checks`, `gives`, `runs`, `takes`, `achieves`, `drops to`, `crosses`.
- **Ban Evaluation & Datapath Verb Cycling**: Never rotate 4+ action verbs for the same measurement trend (`reaches / surpasses / climbs to / overtakes / crosses below`) or datapath hop (`traverse / cross / pass through / travel across`) inside one paragraph. Repeat the same 1–2 plain verbs (`is`, `achieves`, `drops to`, `crosses`, `reduces`) cleanly so `MATTR-100` stays `<= 0.68`.
- **Natural Pronoun & Ellipsis Balance**: Do **not** over-correct `MATTR-100` downward by mechanically repeating identical nouns or verbs inside adjacent clauses (BAD: `"Local TLBs fill quickly, yet local TLBs cannot..."` or `"latency drops to 12 ns, and energy drops to 0.4 nJ"`). Use unambiguous pronouns (`"yet they cannot..."`), clean ellipsis (`"latency drops to 12 ns and energy to 0.4 nJ"`), or one plain shift (`"latency drops to 12 ns while energy falls to 0.4 nJ"` / `"trims energy to 0.4 nJ"`) while still rejecting 4–7 decorative verb cycles.
- **Core plain nouns**: `overhead`, `latency`, `misses`, `bandwidth`, `memory`, `cache`, `table`, `buffer`, `cost`, `time`, `rate`, `size`, `access`.
- **Plain anchors & hedges**: `roughly`, `describe`, `discuss`, `Note that...`, `possible`, `able`, `assume`, `because`, `since`, `hence`, `instead`, `whereas`, `unlike`, `unfortunately`, `in practice`, `to first order`, `within the noise`, `at the cost of`, `modest`, `conservatively`, `typically`, `for most`.

### B. Elevated-Register Thesaurus Ban Table
LLMs routinely "upgrade" plain engineering verbs and prepositions into slightly formal literary equivalents that spike `MATTR-100` above `0.70` even when zero classic AI buzzwords appear. Replace every elevated swap below with plain engineering English:

| Elevated Register (Ban / Replace) | Plain Engineering English (Use Instead) |
| :--- | :--- |
| `serves as` | `is` |
| `built atop` | `built on` |
| `permits` | `allows` / `lets` |
| `attains` | `achieves` / `gets` / `reaches` |
| `prior to` | `before` |
| `alongside` | `with` |
| `undermine` | `hurt` / `break` / `degrade` |
| `resilience` | `protection` / `resistance` / `security` |
| `yields` | `gives` / `produces` |
| `exhibits` | `shows` / `has` |
| `employs` / `utilizes` | `uses` |
| `compels` | `forces` |

### C. Concrete Microarchitectural Verbs
Use specific physical verbs whenever describing hardware behavior:
- **Pipeline & Execution**: `stalls`, `squashes`, `retires`, `speculates`, `dispatches`, `serializes`, `hoists`, `bypasses`, `flushes`, `starves`.
- **Memory & Coherence**: `evicts`, `invalidates`, `coalesces`, `remaps`, `reclaims`, `packs`, `prefetches`, `pins`, `tracks`, `snoops`.
- **Parallelism & Bandwidth**: `exploits`, `overlaps`, `interleaves`, `hides`, `masks`, `amortizes`, `saturates`, `throttles`, `trims`, `batches`.
- **Overhead & Attribution**: `incurs`, `dominates`, `eliminates`, `suffers`, `triggers`, `exposes`, `pinpoints`, `limits`, `bounds`.

### D. Calibrated Epistemic Modality and Zero Editorial Gloss
- **Preserve realistic engineering modals**: Real architecture claims reflect finite benchmarks, specific configurations, and empirical trade-offs. Keep calibrated modals (`can`, `may`, `often`, `typically`, `in practice`, `tends to`, `can help`, `we evaluate this option`) on empirical and design statements—never strip them into absolute universal laws (`prevents`, `guarantees`, `directly produces`, `reaches full utilization`, `eliminates`).
- **Zero editorial gloss**: Report the hardware mechanism, trade-off, or measurement directly and move on to the next fact. Do **not** append interpretive commentary telling the reader what a clean number proves (`"showing why static partitioning falls short"`, `"which confirms the efficiency advantage"`).
- **Transparent bounds**: Model costs conservatively (`conservatively assume`), report full intervals (`2.9% to 6.1%`), label noise honestly (`within the noise`), and admit hardware ceilings (`limited by DRAM bandwidth at 64% of peak`). Pair `up to Y` with the average/geomean whenever measured, but **factual fidelity overrides pairing** when source data only reports a bound or worst-case figure—never fabricate an average.

---

## 3. Naming Discipline and Terminology Hygiene

### System and Technique Names
Prefer four clean conventions: (1) plain 1–2 syllable English word (`Pond`, `Swarm`, `Constable`), (2) transparent semantic compound (`FireSim`, `InvisiSpec`, `MorphCore`), (3) clean functional initialism (`SALP`, `RMM`, `HFI`), or (4) **no coined name at all** (`Vector Runahead`, `Elastic Cuckoo Page Tables`).
- **Hard Bans**: Zero forced backronyms stuffing filler words (`Handling Upcoming`, `Mathematically Adaptive`) and zero non-ASCII Greek system names (`ρHammer`) that break plain-text search.

### Components, Acronyms, and Unpacked Compounds
- **Plain component names (2–4 words)**: Prefer functional English (`range table`, `Epoch ID`, `likely-stable load`, `Register Monitor Table`) over ornamental coinages.
- **New acronym budget & Use-It-Or-Drop-It rule**: Cap **paper-coined** acronyms at **`<= 5`** (standard community terms like `DRAM`, `LLC`, `TLB`, `CXL`, `NUMA`, `ROB`, `MSHR` do not count). **Never introduce a parenthetical acronym `(XYZ)` unless it is reused at least once more in the same section or Abstract** (do not define `(ILP)` or `(MLP)` once and leave it unused). Ban colliding alphabet soup (`VRF`, `P-VRF`, `M-VRF`, `VVR`, `VRLT`), mid-paper renames, and redefining established acronyms (`hereafter, SB refers to GSB`).
- **Macro-lock the system name** in LaTeX (`\newcommand{\sysname}{...}`) so capitalization and hyphenation never drift.
- **Unpack stacked hyphenated noun compounds**: Keep established domain compounds (`out-of-order`, `state-of-the-art`, `end-to-end`, `just-in-time`), but unpack synthetic 3+ hyphen stacks into plain prepositional phrases (`miss-rate overhead from extra evictions` instead of `eviction-induced miss-rate overhead`; `instructions that depend on load data` instead of `load-data-dependent instructions`).

---

## 4. Output Format Mode and Venue Micro-Typography

### Output Format Mode Toggle
Match surface markup strictly to the requested deliverable format:
- **LaTeX Mode (`.tex` manuscripts)**: Use `---` (rare em-dash), `--` for numeric/page ranges (`55--500~ns`), `~` before units (`16~GB`, `3.2~GHz`), `\texttt{}` for instructions/APIs/benchmarks, `\paragraph{...}` for inline bold headings, `$\times$` for multipliers, and `\figref{}`/`\secref{}` macros.
- **Plain-Text / Markdown Mode**: Emit clean prose without raw LaTeX tokens—use regular spaces before units (`16 GB`, `3.2 GHz`), plain ranges (`55–500 ns` or `55-500 ns`), plain multipliers (`1.79×` or `1.79x` locked globally), and zero stray `~`, `---`, or `\texttt{}` escapes.

### Venue Cross-Reference Matrix (Lock One Style Globally)
Ignore the obsolete textbook split between sentence-initial `Figure` and mid-sentence `Fig.`—lock **one style globally**:

| Target Venue | Figure Ref | Section Ref | Table Ref | Venue Voice Notes |
| :--- | :--- | :--- | :--- | :--- |
| **ISCA** | `Figure 1` (preferred) | `Section 3` | **`Table 1`** (never `Tab.`) | Broad framing, clear `\paragraph{}` signposting, honest Discussion. |
| **MICRO** | `Figure 1` (preferred) | `Section 3` | **`Table 1`** (never `Tab.`) | Deep microarchitectural detail, tight area/power accounting. |
| **HPCA** | `Figure 1` or `Fig. 1` | `Section 3` or `Sec. 3` (**NEVER `§`**) | **`Table 1`** (never `Tab.`) | Direct, quantitative, 1-decimal `%` common; `§` is absent in HPCA. |
| **ASPLOS** | `Figure 1` (preferred) | `§3` or `Section 3` | **`Table 1`** (never `Tab.`) | Full-stack active voice, clean integer `%`, rich multi-sentence captions. |

### Citations, Punctuation, and Formal Mechanics
- **Citation Cover-Up Test**: Covering `[12]` must leave a grammatically complete sentence. Zero clause-initial `In [12], ...` and zero bare `[12] proposed...`; use `Prior work [12]`, `Smith et al. [12]`, or end-of-clause `[12].` Sort and compress citations (`[16, 38]`, never `[21] [42]`).
- **Mechanics**: Always write `e.g.,` and `i.e.,` with the American comma (never `For e.g.,`). Zero contractions (`doesn't`, `can't`, `it's`). Keep parenthetical asides under `~10` words so they never split a verb from its complement. Keep footnotes sparse (`0–2` per paper).

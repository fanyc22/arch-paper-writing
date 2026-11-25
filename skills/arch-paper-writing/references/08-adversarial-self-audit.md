# Two-Pass Adversarial Self-Audit Protocol

> **Scope**: **Universal** — execute all seven checks on every architecture format (10–15p conference papers, 2–4p Letters, workshops, rebuttals, standalone excerpts). Length-sensitive rules (macro `per 100 sents` / `per 1k` rates and full-section passive bands) scale by document size as marked in the Sign-Off Gate table; skip full-paper section/page-budget checks when auditing short formats or excerpts.

Never ship Pass 1 prose. After drafting or revising any section, execute **all seven checks below in order** and apply direct in-place rewrites until every gate passes. Audit for **all three failure classes**: classic AI tells (Class B), try-hard anti-AI over-corrections (Class C), and weak human habits (Class A). Perform the audit internally unless the user requests an explicit critique report; deliver clean, publication-ready prose.

---

## Check 1 — The Shuffle Test (Paragraph Topology & Anti-Symmetry)

1. For every non-enumerated paragraph with `>= 3` sentences, test swapping two interior sentences ($S_2 \leftrightarrow S_3$ or $S_3 \leftrightarrow S_4$). Also scan for chatbot-style `\item \textbf{Label}:` bullet-list sprawl.
2. **PASS**: Swapping breaks physical causality, leaves a hardware variable undefined, or detaches a grounded reference; neither consecutive paragraphs nor **consecutive sentences** clone syntactic openings; block bullet lists stay restrained (`0–2` `itemize` blocks full paper, `0` default on 2–4p Letters, and `0` in Related Work, Evaluation prose, or Conclusion).
3. **FAIL**: The paragraph still reads fine after shuffling (flat laundry list or paraphrase cloud), consecutive paragraphs mirror identical structures (`Two X... / Two Y...`, unprompted `First, ... Second, ... Third, ...`), **adjacent sentences clone syntactic templates** (`"During X, ... / During Y, ..."`, `"On GPUs, ... / On CPUs, ..."`, `"A hit ... / A miss ..."`, `"When X ..., ... / When Y ..., ..."`), OR prose is chopped into gratuitous `\begin{itemize}\item \textbf{Label}: ...` blocks where inline `(1)/(2)` / `(i)/(ii)` prose belongs.
4. **Fix**: Rebuild on `SK-1`–`SK-8` (`references/04-paragraph-logic-and-cohesion.md`); vary paragraph openings organically; rewrite mirrored contrasting sentences with **asymmetric grammatical entry**; fold non-essential bullet blocks into flowing paragraphs with inline `(1)/(2)` or `(i)/(ii)` enumerations.

---

## Check 2 — The Connector-Deletion & Natural-Pivot Test

1. Inspect both sentence-initial transitions (`However,`, `Therefore,`, `Thus,`, `In contrast,`, `As a result,`, `For example,`, `Moreover,`, `Furthermore,`, `Additionally,`, `Notably,`) and mid-clause `, however,`.
2. **PASS**:
   - Logical pivots sit in the healthy human band: **`4–7` per 100 sentences** (**`<= 1` explicit transition adverb per 2–3 paragraph excerpt**).
   - Every kept pivot performs a real logical operation (genuine reversal for `However,`, explicit replacement for `Instead,`, premise entailment, or concrete example).
   - Postpositive `, however,` count is **`<= 1` per full section** (**`0` in short 2–3 paragraph excerpts**).
3. **FAIL**:
   - **Too glued / overshoot**: `> 7.5/100` (or `>= 2` transitions in a short 2–3 paragraph excerpt), **non-contrastive `However,`** between two additive/elaborative sentences, `>= 2` additive adverbs (`Moreover/Furthermore/Additionally`) in one paragraph, ping-pong `However,` pairs, or conclusion adverbs stranded after `Note that...`.
   - **Too staccato (Class C over-correction)**: **`0` sentence-initial logical pivots across 12+ sentences**, OR mid-clause `, however,` smuggling (`X, however, Y`).
4. **Fix**: Strip fake additive glue and non-contrastive `However,`; repair missing causes with `because`/`when`; restore plain sentence-initial `However,` or `Therefore,` only where a real turn occurs; rewrite mid-clause `X, however, Y` as plain `However, X Y` or `But X Y`.

---

## Check 3 — Zero-Redundancy Delta, Tail-Stutter, Band Monotonicity & Clean Stops

1. Tag each sentence with a 3–5 word delta (`[Mechanism]`, `[Cause]`, `[Quant]`, `[Consequence]`, `[Pivot]`, `[Elimination]`, `[Boundary]`, `[Next-State]`) and an abstraction band (`B1`–`B4`), and inspect every $S_i \rightarrow S_{i+1}$ boundary for verbal tail echoes or editorial gloss.
2. **PASS**:
   - Every sentence delivers a distinct hardware entity, state transition, number, or scope limit; bands stay within at most two adjacent levels monotonically.
   - **Given-New lead-5 chaining stays bounded at `35–48%`** (trigger `< 28%` or **`> 52%`**; ~55% of boundaries progress naturally without repeating a tail word).
   - **Zero Tail-Stutter & 3-Hop Stem Echoes**: no adjacent sentence repeats a `>= 3`-word tail phrase (`"...across all 16 banks. Across all 16 banks, ..."`), mirrors $S_i$'s `Subject + Verb` (`"...shared across multiple cores. Because multiple cores share..."`), or chains the same stem across 3+ consecutive sentences (`colocate -> colocating -> Such colocation`).
   - **Zero Editorial Gloss, Pleonasms & Essay Idioms**: no interpretive tails (`"showing why static partitioning falls short"`, `"which confirms the efficiency advantage"`), no pleonasms/doublets (`"up to X% at maximum"`, `"fixed and provisioned"`, `"physical spatial locality"`, `"strongly outperform"`, redundant colon restatements `"two pairs: one pair for X and one pair for Y"`), and no textbook/essay idioms (`"Conventional X wisdom holds"`, `"operate in a very different regime"`, `"underlying hardware substrates"`, `"a surprisingly high payoff"`, `"inevitably"`, `"at its core"`, `"in a fundamentally different way"`). Every paragraph stops cleanly once the final technical fact lands.
3. **FAIL**: Any Paraphrase Echo, `>= 3`-word tail stutter, 3-hop stem echo, `> 52%` forced chaining, theatrical slogan opener, pleonasm/doublet, essay idiom, editorial gloss, or `B1 -> B4 -> B1` whiplash.
4. **Fix**: Delete echoes, echoed preambles, pleonasms, essay idioms, slogan openers, and editorial gloss; state the next hardware step or measurement directly; split or cut cross-band jumps.

---

## Check 4 — Bimodal Reference & Shell-Noun Sweep

1. Highlight every sentence-initial or clause-initial `This`, `These`, `Such`, `That`, and `It`.
2. **PASS**: Every demonstrative names a concrete entity or physical event from the preceding sentence (`This miss burst`, `This writeback stall`, `Such bounces`, `This L2 stalling`) in plain, unpacked phrasing.
3. **FAIL**: Bare ambiguous pronouns (`This is...`, `It avoids...`), hollow shell nouns (`This approach / strategy / method / paradigm / merit / challenge / finding / issue / capability`), OR over-packed hyphenated noun stacks (`this latency-versus-capacity provisioning tension`).
4. **Fix**: Replace with `This / These / Such <plain concrete noun>`, restate the hardware unit name, or unpack stacked compounds into plain prepositional phrases.

---

## Check 5 — Role-Coupled Burstiness, Pacing & Anti-Checklist-Stiffness Check

1. Inspect sentence lengths `[w1, ..., wk]`, paragraph pacing, and passive runs.
2. **PASS**:
   - **Relaxed, breathing burstiness (`SD 8.5–11.5w`, `CV ~0.35–0.55`)**: natural mix of plain `8–13w` workaday technical facts (`"Figure 3 shows this split."`, `"We use a 4-level page table."`) and organic `26–38w` multi-step hardware explanations (using natural inline parentheticals or `because`/`where`/`when` clauses).
   - **Natural length pacing (`~95–105%` of target length)**: Pass-2 edits have **not** over-compressed prose into telegraphic summaries or hyphenated noun stacks.
   - Passive voice sits around `16–24%` with **`<= 2` consecutive passive sentences** (in short 150–350w excerpts, do not warp natural phrasing to hit a 10-sentence passive % target).
3. **FAIL**:
   - **Checklist Stiffness**: Pass-2 rule juggling flattened every sentence into a cautious `16–22w` run (`SD < 7.5w`, `CV < 0.25`).
   - **Engineered copywriting slogans** (`"X replaces fixed capacity with runtime reconfiguration."`) or dramatic reveals (`"Table 4 explains why — ..."`).
   - `> 35w` sentence bloated by chained trailing participles, OR dead passive walls (`>= 3` passives in a row).
4. **Fix**: Let genuine multi-step hardware explanations stay unified at `26–38w` rather than chopping them into uniform 18w chunks; replace theatrical slogans with plain factual statements; unpack compressed hyphen stacks (`eviction-induced miss-rate overhead` -> `miss-rate overhead from extra evictions`); break participle chains into finite clauses; activate dead passive walls.

---

## Check 6 — Lexicon, Participle-Tail, Register, Mid-Paper Flow, Precision & Format Sweep

Run six surgical scans across the full draft:

1. **Tier 1, Tier 2 & Source-Note Normalization**: Confirm **`0`** Tier-1 hard bans (except literal proper nouns like ARM `Realm`). Scrub Tier-2 risers (`diverse`, `enhance`, `facilitate`, `comprehensive`, `subsequently`, `confirming`, `consistently`, `conversely`, non-security `mitigate`, `solely`, `inherently`, `essential`, `tailored`, `crucial`, `substantial`, `leverage`, `utilize`, `novel`)—**including any that leaked in from rough author notes**.
2. **Elevated-Register, Verb-Cycling & `MATTR <= 0.68` Sweep**: Hunt and replace `serves as` (`is`), `built atop` (`built on`), `permits` (`allows`/`lets`), `attains` (`achieves`/`gets`), `prior to` (`before`), `alongside` (`with`), `undermine` (`hurt`/`break`), `resilience` (`protection`/`resistance`), `yields` (`gives`), `exhibits` (`shows`/`has`), `employs` (`uses`), `compels` (`forces`). Confirm no paragraph rotates 4+ action verbs for the same measurement or datapath action (`reaches/surpasses/climbs to/overtakes/crosses below` or `traverse/cross/pass through/travel across`)—repeat 1–2 plain verbs (`is`, `achieves`, `drops to`, `crosses`, `reduces`) and core nouns freely. Verify that plain-verb discipline did **not** introduce robotic literal verb or noun stuttering inside adjacent clauses (`"Local TLBs... yet local TLBs"`, `"As density drops, energy drops below X and drops below Y"`) that starves unambiguous pronouns (`it`/`they`/`its`) or clean ellipsis (`"energy falls below X and then Y"`).
3. **Expanded Participle-Tail & Em-Dash Audit**:
   - Kill **ALL** tacked-on result participles appended to complete clauses: `, ensuring`, `, enabling`, `, thereby ...ing`, `, allowing`, `, confirming`, `, highlighting`, **`, leaving`, `, totaling`, `, violating`, `, yielding`, `, creating`, `, causing`, `, making`, `, resulting in`, `, forcing`, `, reducing`**.
   - Count em-dashes: **`<= 1.5 / 1k` full paper**, **default `0` in short 150–350w passages** (remove any `> 1` in a 2–3 paragraph section, and remove **every** dramatic reveal em-dash). Replace with parentheses `(...)`, commas, or a full stop.
4. **Mid-Paper Flow & Use-It-Or-Drop-It Acronym Check**: In Motivation, Design, and Evaluation, confirm **`0` re-expansions of already-defined acronyms** and **`0` standalone textbook system recaps**. Delete any parenthetical acronym `(XYZ)` defined once and never reused in the same section or Abstract. Confirm locked system-name spelling, `<= 5` paper-coined acronyms, and zero mid-paper renames.
5. **Quantitative Discipline, Calibrated Modality & Factual Fidelity**:
   - Never fabricate metrics, baselines, or citations; leave `[TODO: <missing datum>]` when source data is absent.
   - **Preserve calibrated engineering modals** (`can`, `may`, `often`, `typically`, `in practice`, `tends to`, `can help`, `we evaluate this option`) on empirical/design statements—never inflate hedged findings into absolute universal laws (`prevents`, `guarantees`, `directly produces`, `reaches full utilization`, `eliminates`).
   - Pair `up to Y` with the average/geomean whenever measured, **unless source notes only report a bound/worst-case range** (factual fidelity overrides inventing an average).
   - Use `geomean` for ratios; integer or 1-decimal `%` (kill false precision like `450.65×`, `0.43099 pJ`); explain slowdowns, outliers, and within-noise results honestly without editorial gloss; keep Conclusion to one `90–150w` past-tense paragraph on full papers (`< 12%` Abstract 3-gram overlap; `2–3` sentences in 2–4p Letters).
6. **Output Format & Mechanical Hygiene**:
   - **Mode Check**: Emit LaTeX tokens (`---`, `--`, `~`, `\texttt{}`, `$\times$`) **only** in `.tex` mode; use clean standard punctuation in plain-text/Markdown mode.
   - **Citation Cover-Up Test**: zero `In [X],` and zero bare `[X] verb`. Locked `Figure`/`Fig.` and venue-matched `Section`/`§` (**zero `§` in HPCA**); **`Table` never abbreviated**. `e.g.,`/`i.e.,` with commas; zero contractions, double words (`the the`), unclosed parens, `??`, or tool tags. Run `references/07-figures-tables-captions.md`'s 6-point audit whenever figures/tables/captions are specified.

---

## Check 7 — The Hostile Area-Chair Turing Check

Re-read the finished section as a skeptical ISCA/MICRO/HPCA/ASPLOS PC chair hunting for **both** classic LLM fingerprints and try-hard anti-AI prose. Rewrite immediately if any answer raises doubt:

1. **Try-Hard Anti-AI & Deep-Discourse Test**: Does the passage read like someone trying too hard *not* to sound like an LLM—literal tail-to-head Given-New stuttering (`> 52%`), robotic same-word repetition starving pronouns/ellipsis, mirrored consecutive sentence openers (`During X... / During Y...`), zero logical transitions, mid-clause `, however,`, dramatic em-dashes, punchy slogans, stacked hyphenated compounds, editorial gloss, or stripped epistemic modals? *If yes, relax into plainspoken, calibrated, unhurried engineering prose.*
2. **System-Name Swap Test**: Could you swap our system name for another paper's name and keep a sentence true? *If yes, delete it or anchor it to hardware reality.*
3. **Press-Release & Too-Smooth Test**: Does any sentence sound like marketing copy, a textbook recap, or conflict-free cheerleading? *Name concrete bottlenecks, ceilings, and caveats.*
4. **Causal-Leap / Tautology Test**: Does any claim skip a physical mechanism or explain a speedup tautologically (`wins because of its heuristic`)?
5. **Mid-Paper Seam Test**: Does a Motivation/Design/Evaluation passage drop abruptly into a standalone overview or re-expand terms already introduced earlier? *Start directly in-flow.*

---

## Quick Sign-Off Gate Summary

| Gate | Applies To | Pass Threshold | Immediate Action on Failure |
| :--- | :--- | :--- | :--- |
| **Topology, Lists & Symmetry** | **Full Paper / Scales on Short** *(order-lock, list restraint & anti-mirroring: Universal)* | Order-locked paragraphs; `4–7/100s` pivots (`<=1` per 2–3 para excerpt, `0` non-contrastive `However,`, never `0/100`); `<=1` `, however,` per section (`0` in short excerpts); `0` stacked additives; `0` mirrored sentence or paragraph openers; `0–2` `itemize` blocks full paper (`0` default on 2–4p Letters & RW/Eval/Conc) | Rebuild on `SK-1`–`SK-8`; trim excess/fake `However,`; fold `\item \textbf{Label}:` sprawl into inline `(1)/(2)` prose |
| **Delta, Stutter & Gloss** | **Full Paper / Scales on Short** *(0 stutters/gloss/shell nouns: Universal)* | `Given-New5 35–48%` (trigger `>52%`); `0` `>=3`-word tail stutters or 3-hop stem echoes; `0` pleonasms/essay idioms/editorial gloss/slogans; `0` hollow shell nouns (cap `<=0.5%`); `<=2%` bare `This/It`; `0` stacked hyphen compounds | Delete echoed preambles, pleonasms & editorial gloss; ground as `This <plain noun>`; unpack hyphen stacks |
| **Burstiness, Passive & Em-Dashes** | **Full Paper / Scales on Short** *(<=2 passive run & 0 dramatic dashes: Universal)* | Relaxed `SD 8.5–11.5w` (`95–105%` pacing; plain `8–13w` facts + organic `26–38w` explanations; zero checklist stiffness); passive `~16–24%` (`<=2` in a row; qualitative in short excerpts); em-dashes `<=1.5/1k` (default `0` in short passages) | Un-flatten stiff 18w runs; activate dead passive walls; replace em-dashes with parens/commas/periods |
| **Lexicon, Verbs & Modality** | **Universal** | `0` Tier-1 bans; Tier-2 scrubbed (incl. from notes); `0` elevated-register swaps; `0` 4-verb cycling; `0` robotic same-word stuttering (keep clear pronouns & ellipsis); `MATTR <=0.68`; `0` trailing result participles; calibrated modals (`can/may/often/typically`) preserved | Reuse 1–2 plain verbs without starving pronouns/ellipsis; split `, leaving/, totaling/, violating`; restore realistic modals |
| **Flow, Acronyms & Turing** | **Universal** | `0` mid-paper acronym re-expansions or unused single-use acronyms; factual fidelity on `up to`; correct LaTeX vs plain-text mode; `0` citation-as-noun; passes all 5 Turing checks | Enter directly in-flow; drop single-use `(XYZ)`; relax try-hard polish into plain engineering prose |
| **Page & Section Budgets** | **Full Paper Only** *(skip on 2–4p Letters & excerpts; use `01 §6` for Letters)* | `40-25-20-15` body split (`~11.5–12.5p`), Intro by p.2, `12–16` figures / `2–4` tables, late Related Work, `90–150w` single-paragraph Conclusion | Rebalance against `01-architecture-and-budgets.md` (`§§1–5` for full papers; `§6` for 2–4p Letters) |

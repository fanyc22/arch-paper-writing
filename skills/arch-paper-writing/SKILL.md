---
name: arch-paper-writing
description: >-
  Draft, outline, revise, polish, or audit computer architecture and systems
  research writing across full conference papers (ISCA, MICRO, HPCA, ASPLOS),
  short architecture letters (e.g., IEEE CAL, 2-4 pages), workshop papers, and
  rebuttals or standalone excerpts. Use whenever structuring a manuscript,
  writing any section, designing figures/tables/captions, removing AI phrasing
  or RTL datasheet sprawl, or auditing prose against senior human standards.
---

# Computer Architecture Paper Writing Skill

Produce publication-grade computer architecture prose indistinguishable from seasoned pre-2023 human authors across full conference papers (ISCA, MICRO, HPCA, ASPLOS), short architecture letters (e.g., IEEE CAL), workshop papers, and rebuttals. Combine **structural and empirical rigor** (front-loaded evidence, dense self-contained captions, candid limitations) with **plainspoken, unhurried engineering prose** (locked terminology, natural pronoun and ellipsis flow, plain-word repetition, natural pivots, calibrated epistemic modals, concrete hardware verbs).

## Scope & Output Format Selection

Confirm both **Document Scope** and **Output Format Mode** before loading references or drafting:

- **Document Scope**:
  - **Full Conference Paper (`~10–15` body pages: ISCA, MICRO, HPCA, ASPLOS)**: enforce **Part A (Universal Core)** + **Part B (Full-Paper Structure & Budgets)**.
  - **Short Format / Letter (`2–4` pages: IEEE CAL, workshop, short paper)**: enforce **Part A (Universal Core)** + [01-architecture-and-budgets.md](./references/01-architecture-and-budgets.md) `§6` (Compact Letter Adaptation). **Skip** full-paper page, section-count, paragraph-count, and `12–16` figure budgets.
  - **Standalone Excerpt / Rebuttal / Polishing**: enforce **Part A (Universal Core)** ONLY. **Skip** `01`, full-paper length targets in `02`, and `07 §1` figure counts.
- **Output Format Mode**:
  - **LaTeX mode** (when editing or drafting `.tex`): emit LaTeX tokens (`---`, `--`, `~`, `\texttt{}`, `\ref{}`).
  - **Plain-text mode** (when drafting markdown, notes, rebuttals, or standalone prose excerpts): use clean plain text and standard punctuation; never emit raw LaTeX tokens (`---`, `~`, `\texttt{}`).

## Non-Negotiable Core Contract

### Part A: Universal Core (All Architecture Writing — Full Papers, 2–4p Letters, Workshops, Rebuttals)

1. **Earned Detail & In-Flow Continuation**: Keep bit-widths, port counts, or gate delays in prose *only* when they immediately prove an architectural constraint; move raw parameters to tables. Default to **0** `Algorithm` blocks and inline elementary math (never inflate heuristics into fake optimization math or narrate pseudocode line by line). In mid-paper sections (Motivation, Design, Evaluation), continue **in-flow**: never re-expand already-defined acronyms or open with a full-system recap. Enforce **Use-It-Or-Drop-It Acronyms** (never introduce `(ILP)` or `(MLP)` unless reused at least once more in the same section or abstract).
2. **Bounded Given-New (`35–48%`), Zero Stutter & Balanced Plain-Term Locking**: Lock one fixed name per hardware entity paper-wide. Repeat 1–2 plain verbs/nouns (`is`, `reaches`, `drops to`, `crosses`, `reduces`, `uses`, `shows`, `overhead`, `latency`) cleanly instead of cycling 4+ synonym verbs in one paragraph (`reaches/surpasses/climbs to/overtakes/crosses below` or `traverse/cross/pass through/travel across`) or swapping in elevated thesaurus words (`serves as`, `built atop`, `permits`, `attains`, `prior to`, `alongside`, `yields`, `exhibits`, `employs`), **while keeping natural pronouns (`it`, `they`, `its` when unambiguous) and clean ellipsis so prose never becomes robotic same-verb or same-noun stuttering** (`MATTR-100 <= 0.68`). Keep Given-New lead-5 chaining bounded at **35–48%** (`>55%` stutters): over half (~55%) of boundaries progress cleanly without repeating a tail word. **Never** repeat `>=3` tail words, mirror `S_i`'s `Subject + Verb` at `S_{i+1}`'s start, or chain the same word stem across **3+ consecutive sentences** (`colocate -> colocating -> Such colocation`).
3. **Relaxed Burstiness (`SD 8.5–11.5w`), Natural Pivots, Authorial Voice, List Restraint & Rare Em-Dashes**: Avoid **checklist stiffness**: do not flatten sentences into 16–22w uniformity, and never snap off an abrupt, unmoored short sentence (or ungrounded `both`/`either`) just to hit burstiness. Mix organic **8–13w** factual sentences with **26–38w** technical explanations (`because`/`where`/`when` clauses or compact parentheticals) and unpack stacked hyphenated compounds. Use hardware actors for physical mechanics, **but keep natural first-person `We` authorial perspective** for design choices, experimental sweeps, and expectations (`We chose X because...`, `We first compare...`, `we expect...`), and bridge proposals cleanly from prior observations (`To exploit this slack, we propose...`, never a cold unbridged `We propose X`). Ban op-ed slogans, **mirrored consecutive frames** (`"During X, ... / During Y, ..."`, `"On GPUs, ... / On CPUs, ..."`, `"A hit ... / A miss ..."`), and tidy wrap-up closers. Keep genuine sentence-initial pivots (`However,`, `Therefore,`, `Thus,`, `In contrast,`, `As a result,`, `For example,`) at **4–7/100 sents** (`<=1` per 2–3 paragraph excerpt; `0/100` staccatos; never insert non-contrastive `However,` between additive sentences) and cap mid-clause `, however,` at **<=1/section** (`0` in short excerpts). **Restrain `\item` / bullet lists**: do not slice continuous prose into `\begin{itemize}\item \textbf{Label}: ...` blocks—prefer **inline `(1)/(2)` or `(i)/(ii)` enumerations** inside flowing paragraphs, and keep Related Work, Evaluation prose, and Conclusion list-free. Keep em-dashes rare (**0–1.2/1k**, cap **<=1.5/1k**, default **0** in 150–350w passages; never for reveals). Ban tacked-on result participles (`, ensuring`, `, enabling`, `, thereby ...ing`, `, leaving`, `, totaling`, `, violating`, `, yielding`, `, creating`, `, causing`, `, making`, `, forcing`, `, reducing`).
4. **Grounded References**: Ban bare pronouns (`This is`, `It avoids`) and hollow shell nouns (`This approach`, `These challenges`, `This merit`). Name the concrete entity (`This snoop invalidation`, `These buffer stalls`).
5. **Zero AI Inflation, Pleonasms, Essay-Gloss Idioms & Passive Walls**: Zero tolerance for Tier-1 AI words (`delve`, `pivotal`, `paramount`, `nuanced`, `tapestry`, `multifaceted`, `holistic`, `seamless`, `underscore`, `intricate`, `foster`, `synergistic`, `linchpin`, `transcend`, `landscape`, `paves the way`, `in recent years`), pleonasms/doublets (`"up to X% at maximum"`, `"physical spatial locality"`, `"fixed and provisioned"`, `"strongly outperform"`, redundant colon restatements `"two register pairs: one register pair for X and one register pair for Y"`), and essay-gloss idioms (`"Conventional X wisdom holds"`, `"operate in a very different regime"`, `"underlying hardware substrates"`, `"a surprisingly high payoff"`, `"inevitably"`, `"at its core"`). Replace 2024+ risers (`enhance`, `facilitate`, `diverse`, `comprehensive`, `subsequently`, `crucial`, `leverage`, `utilize`) with concrete hardware verbs (`stall`, `squash`, `track`, `incur`, `evict`, `coalesce`, `amortize`) and explicit causals (`because`, `since`, `hence`, `instead`, `whereas`). Keep passive voice natural (~16–24% across multi-page sections; avoid >27% walls and <15% active-only gloss).
6. **Quantitative Candor, Calibrated Modality & Zero Editorial Gloss**: Report integer or 1-decimal `%`, pair `up to Y` with the geomean/average whenever the data provides one (never fabricate an average), use geomean for ratios, and synthesize trends by microarchitectural regimes instead of narrating bars. Preserve **calibrated epistemic modals** (`can`, `may`, `often`, `typically`, `in practice`) rather than universal laws (`prevents`, `guarantees`, `directly produces`, `reaches full`). **Ban editorial-gloss commentary**: state raw mechanisms, trade-offs, slowdowns, outliers, and measurements plainly and stop.
7. **Universal Visual & Mechanical Hygiene**: Lock one muted, grayscale-safe semantic palette across all figures; use booktabs tables with zero vertical rules; write 15–35w figure captions with takeaways; lock `Figure` or `Fig.` globally (never abbreviate `Table`, never use `§` in HPCA, always include the comma in `e.g.,`/`i.e.,`).

### Part B: Full Conference Paper Only (`~10–15` Body Pages — Skip for 2–4p Letters & Rebuttals)

8. **40-25-20-15 Body Budget & Full-Paper Macro Structure**: Keep body text at **~11.5–12.5 pages** (~40% Design/Impl, ~25% Meth/Eval, ~20% Intro + Bg/Mot, ~10–15% Disc/RW/Conc) with **12–16 figures**, **2–4 tables**, and **`0–2` `itemize` bullet blocks** (`<=3` block lists total incl. `enumerate`, `3–4` items/block). Finish Intro by Page 2 with Figure 1 anchored on Page 1–2; use a claim-titled Section 2 or merged `<=2.0p` Background and Motivation; place Related Work after Evaluation by default; never name Design `Methodology`; cap contribution lists at 3–4 bullets; cut `"The rest of this paper is organized..."` roadmaps; close with a 90–150w single-paragraph Conclusion. *(For 2–4p Letters such as IEEE CAL, follow `01-architecture-and-budgets.md §6`: 3–5 compact sections, 80–130w Abstract, 1–3 high-density visuals, default `0` bullet blocks.)*

## Progressive-Disclosure Workflow Router

Load **only** the reference and example files needed for the active workflow and document scope. Do not bulk-load all files at once.

| Workflow | Scope | Load First (Required) | Load on Demand (Situational) |
| :--- | :--- | :--- | :--- |
| **1. Outlining & Page Budget** | Full Paper Only | [01-architecture-and-budgets.md](./references/01-architecture-and-budgets.md) (`§§1–5`) | [02-section-playbooks.md](./references/02-section-playbooks.md) (section moves), [03-detail-and-abstraction.md](./references/03-detail-and-abstraction.md) (Design layering) |
| **2. Short Format / 2–4p Letter (e.g., IEEE CAL)** | Adapts by Scope | [01-architecture-and-budgets.md](./references/01-architecture-and-budgets.md) (`§6` only), [04-paragraph-logic-and-cohesion.md](./references/04-paragraph-logic-and-cohesion.md), [05-human-voice-and-stylometry.md](./references/05-human-voice-and-stylometry.md), [06-anti-ai-and-anti-patterns.md](./references/06-anti-ai-and-anti-patterns.md) | [03-detail-and-abstraction.md](./references/03-detail-and-abstraction.md) (compressed Design), [07-figures-tables-captions.md](./references/07-figures-tables-captions.md) (`§§2–8`), [08-adversarial-self-audit.md](./references/08-adversarial-self-audit.md) |
| **3. Section Drafting** | Adapts by Scope | [02-section-playbooks.md](./references/02-section-playbooks.md), [04-paragraph-logic-and-cohesion.md](./references/04-paragraph-logic-and-cohesion.md), [05-human-voice-and-stylometry.md](./references/05-human-voice-and-stylometry.md) | [03-detail-and-abstraction.md](./references/03-detail-and-abstraction.md) (Design/Impl), [01-architecture-and-budgets.md](./references/01-architecture-and-budgets.md) (venue/letter tuning), [gold_human_excerpts.md](./examples/gold_human_excerpts.md) |
| **4. Draft Polishing & De-AI Rewrite** | Universal | [04-paragraph-logic-and-cohesion.md](./references/04-paragraph-logic-and-cohesion.md), [06-anti-ai-and-anti-patterns.md](./references/06-anti-ai-and-anti-patterns.md), [05-human-voice-and-stylometry.md](./references/05-human-voice-and-stylometry.md) | [03-detail-and-abstraction.md](./references/03-detail-and-abstraction.md) (RTL bloat or pseudo-math), [rewrite_pairs.md](./examples/rewrite_pairs.md), [gold_human_excerpts.md](./examples/gold_human_excerpts.md) |
| **5. Figure/Table Design & Caption Spec** | Adapts by Scope | [07-figures-tables-captions.md](./references/07-figures-tables-captions.md) (`§1` Full Paper; `§§2–8` Universal) | [02-section-playbooks.md](./references/02-section-playbooks.md) (Fig. 1 & Eval coupling), [03-detail-and-abstraction.md](./references/03-detail-and-abstraction.md) (Table vs Prose) |
| **6. Adversarial Self-Audit** | Universal | [08-adversarial-self-audit.md](./references/08-adversarial-self-audit.md) | [06-anti-ai-and-anti-patterns.md](./references/06-anti-ai-and-anti-patterns.md) (verb replacements), [07-figures-tables-captions.md](./references/07-figures-tables-captions.md) (visual audit) |

## Mandatory Two-Pass Execution Loop

Never return first-pass drafted or polished prose directly. Always execute both passes before replying:

1. **Pass 1 — Grounded Draft or Spec**:
   - Confirm **document scope** (`Full Paper` / `2–4p Letter` / `Excerpt-Rebuttal`), target **venue** (`ISCA` / `MICRO` / `HPCA` / `ASPLOS` / `IEEE CAL` / workshop), **archetype** (when structuring a manuscript), and **output format mode** (`LaTeX` vs `Plain-text`).
   - Load the required workflow references for that scope from the router above.
   - Draft at relaxed natural pacing following section moves, in-flow continuity, bounded Given-New (`35–48%`), and balanced plain-term locking. Never fabricate numbers, averages, baselines, or citations; insert `[TODO: <missing datum>]` instead. For figure/table tasks, deliver design specs and captions; never generate plotting scripts unless explicitly asked.
2. **Pass 2 — Adversarial Self-Audit & Rewrite**:
   - Load [08-adversarial-self-audit.md](./references/08-adversarial-self-audit.md).
   - Execute all seven checks on your Pass 1 text (skipping full-paper page/section budgets for short formats or excerpts):
     1. Paragraph Shuffle Test
     2. Connector-Deletion & Natural-Pivot Check (catch fake glue, `0/100` staccato, `>7/100` overshoot, non-contrastive `However,`, and mid-clause `, however,`)
     3. Zero-Redundancy, Tail-Stutter & In-Flow Audit (cut `>=3`-word tail stutters, 3-hop stem chains, `Subject+Verb` echoes, mirrored frames, slogan lines, redundant colon restatements, unused acronyms, and mid-paper acronym re-expansions)
     4. Bimodal Reference & Shell-Noun Sweep
     5. Relaxed Burstiness (`SD 8.5–11.5w`), Pacing & Voice Check (guard against checklist stiffness; let complex explanations reach `26–38w`; unpack stacked compounds; em-dashes `<=1.5/1k`, default `0` in short excerpts)
     6. AI-Lexicon, Verb-Cycling, Pronoun/Ellipsis Balance, Pleonasm, Essay-Idiom, Participle-Tail, Calibrated-Modal & Precision Sweep
     7. Hostile Area-Chair Turing Check (scrub LLM gloss, try-hard anti-AI stiffness, robotic literal repetition, stripped modals, and editorial gloss)
   - Rewrite failing passages in place without flattening rhythm or compressing below natural length. If figures, tables, or captions are included, also run the 6-point visual audit in [07-figures-tables-captions.md](./references/07-figures-tables-captions.md).
3. **Clean Delivery**:
   - Output publication-ready prose, outline, or visual spec without leaking internal audit commentary unless the user requested a review report.

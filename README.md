# Architecture Paper Writing Plugin (`arch-paper-writing`)

An empirical, battle-tested Agent Plugin for drafting, outlining, revising, polishing, and auditing computer architecture and systems research manuscripts—spanning full top-venue conference papers (**ISCA, MICRO, HPCA, ASPLOS, OSDI, SOSP**), short architecture letters (**IEEE CAL, 2–4 pages**), workshops, and rebuttals.

Distilled from a **16-year empirical study (2011–2026)** of **160 stratified top-venue papers** (152 full-text stylometry corpus + 48 deep-read exemplars & contrasts + 20 Open-Access PDFs inspected visually + 671 figure / 164 table captions) and validated via **468 closed-loop blind verdicts** across three frontier model families (**OpenAI `gpt-6.2-astra`**, **Anthropic `Claude Opus 5.5`**, and **Google `Gemini 4 Neon`**) on 8 strictly quarantined pre-LLM human papers.

---

## Key Capabilities

- **Two-Layer Scope Architecture**:
  - **Part A — Universal Core** *(applies to all lengths: 10–15p conference papers, 2–4p IEEE CAL letters, workshops, rebuttals)*: earned detail & in-flow continuation, bounded Given-New cohesion (`35–48%`), balanced plain-term locking with natural pronouns & ellipsis, relaxed sentence-length burstiness (`SD 8.5–11.5w`), natural pivots (`4–7/100 sents`), `\item` / bullet-list restraint (prefer inline `(1)/(2)` or `(i)/(ii)` prose over bold-lead-in bullet sprawl), rare em-dashes, calibrated epistemic modals, quantitative candor, and zero Tier-1/2 AI inflation or Class-C "anti-AI stiffness."
  - **Part B — Full Conference Paper Budgets** *(10–15p papers only; skipped for 2–4p letters & rebuttals)*: 40-25-20-15 body page budget (`11.5–12.5` body pages), Page 1–2 Figure 1 anchor, 6-layer Design abstraction ladder, late Related Work, `12–16` figures / `2–4` tables, and `0–2` `itemize` bullet blocks (`<= 3` incl. `enumerate`)—plus a dedicated `2–4p Letter / IEEE CAL` compact adaptation (`references/01-architecture-and-budgets.md §6`, default `0` bullet blocks).
- **Progressive-Disclosure Skill (`skills/arch-paper-writing/`)**: Routes agents to only the reference modules needed for the active task (Outlining, Short Letter, Section Drafting, Draft Polishing / De-AI, Figure & Caption Spec, or Pass-2 Adversarial Self-Audit) so context stays lean.
- **Always-On Scoped Rulebook (`rules/AGENTS.md`)**: Compact `<6 KB` high-density rule sheet active whenever the plugin is enabled and scoped specifically to architecture/systems writing tasks.
- **Empirical Figure, Table & Caption Craft**: Chart-type decision matrix, semantic palette locking, grayscale-safe redundant encoding, booktabs table rules, four gold caption formulas (`15–35w` figures, `7–15w` tables), and a 6-point pre-submission visual audit.
- **Full Research & Benchmark Transparency (`docs/`)**: Includes all 10 Chinese empirical analysis reports (`docs/analysis/00..09`) and the complete 468-verdict tri-family blind benchmark report (`docs/verification/final_benchmark_report.md`).

---

## Installation

### 1. Antigravity (Recommended — Standard Global Plugin)

Clone directly into your global Antigravity plugins directory:

```bash
mkdir -p ~/.gemini/config/plugins
git clone https://github.com/fanyc22/arch-paper-writing.git ~/.gemini/config/plugins/arch-paper-writing
```

The plugin loads automatically on the next turn and appears under **Customizations → Installed**, where you can toggle the entire bundle (Skill + Rules) on or off in one click.

Or install from a local clone via the Antigravity CLI (`/plugin`):

```text
/plugin install /path/to/arch-paper-writing
```

### 2. Project / Team Workspace Plugin

Share the plugin inside a paper repository so co-authors get the exact same writing discipline automatically:

```bash
mkdir -p .agents/plugins
git clone https://github.com/fanyc22/arch-paper-writing.git .agents/plugins/arch-paper-writing
```

### 3. Other Coding / Writing Agents (Claude Code, Codex, Cursor, Gemini CLI)

This bundle uses standard open Markdown layouts (`skills/<name>/SKILL.md` + `rules/AGENTS.md`):

- **Skills**: Copy `skills/arch-paper-writing/` into `.claude/skills/`, `.agents/skills/`, or your tool's skills folder.
- **Rules**: Append or link `rules/AGENTS.md` into your project's `AGENTS.md`, `CLAUDE.md`, or `GEMINI.md`.

---

## Package Structure

```text
arch-paper-writing/
├── plugin.json                                     # Standard Antigravity Plugin manifest
├── README.md                                       # Documentation & installation guide
├── LICENSE                                         # MIT License
├── assets/
│   └── logo.svg                                    # Light/dark-safe vector plugin icon
├── rules/
│   └── AGENTS.md                                   # Scoped writing rules (Part A Universal + Part B Full Paper)
├── skills/
│   └── arch-paper-writing/
│       ├── SKILL.md                                # Scope router, core contract & mandatory 2-pass audit loop
│       ├── references/
│       │   ├── 01-architecture-and-budgets.md      # 40-25-20-15 full-paper budgets (§§1–5) & 2–4p Letter (§6)
│       │   ├── 02-section-playbooks.md             # Section-by-section rhetorical moves & venue conventions
│       │   ├── 03-detail-and-abstraction.md        # 6-layer Design abstraction ladder & Earned-Detail Rule
│       │   ├── 04-paragraph-logic-and-cohesion.md  # Bounded Given-New (35–48%), pivots & pronoun/ellipsis balance
│       │   ├── 05-human-voice-and-stylometry.md    # Plainspoken register, calibrated modals & stylometric envelope
│       │   ├── 06-anti-ai-and-anti-patterns.md     # Class A/B/C AI & anti-AI-stiffness blacklists + replacements
│       │   ├── 07-figures-tables-captions.md       # Visual hierarchy, booktabs, caption formulas & 6-point audit
│       │   └── 08-adversarial-self-audit.md        # Pass-2 7-check adversarial self-audit checklist
│       └── examples/
│           ├── gold_human_excerpts.md              # 12 annotated pre-LLM top-venue prose exemplars
│           └── rewrite_pairs.md                    # 12 Bad -> Good surgical rewrite pairs
└── docs/                                           # Empirical study & blind verification reports (Chinese)
    ├── analysis/                                   # Phase 1: 160-paper empirical analysis (00–09)
    └── verification/
        └── final_benchmark_report.md               # Phase 3: 468-verdict tri-family blind benchmark report
```

---

## Recommended Usage & Empirical Benchmark Summary

Our 5-stage blind evaluation ([final_benchmark_report.md](./docs/verification/final_benchmark_report.md)) across 8 quarantined pure-human papers (**468 blind verdicts** from `gpt-6.2-astra`, `Claude Opus 5.5`, and `Gemini 4 Neon`) established three practical findings:

1. **Surface AI Artifacts Eliminated**: Across tri-family pairwise blind audits (Round 3, 120 verdicts), classic LLM tells dropped to `0%–5%` (`participle_tail 43.3% → 0.0%`, `em_dash_overuse 28.3% → 0.0%`, `cheerleading_hype 28.3% → 0.0%`, `unsupported_certainty 13.3% → 0.0%`, `ai_lexicon 40.0% → 5.0%`).
2. **Publication-Grade Quality Parity & Real-Human Blind Check**: Unassisted baseline prose scored significantly below published human papers (`-0.40, p = 0.0007`), whereas Skill-guided prose achieved statistical parity (`-0.08, Wilcoxon p = 0.3958`, 75% win+tie rate; outperforming published originals on Opus `+0.15` and Gemini `+0.10`, and matching human quality in standalone 18-passage blind evaluation `p = 0.5228`). In a supplementary blind A/B quiz with 2 real human architecture readers (12 judgments across 4 venues × 5 sections), combined human AI detection landed at exact chance (**`6/12 = 50.0%`**, `p = 1.00`), while qualitative human feedback directly drove `v1.0.2` guardrails (preserving natural authorial `We` in Design/Eval, grounded proposal bridges, avoiding abrupt unmoored short sentences / `both`, and replacing metaphorical `absorb`).
3. **Honest Boundary — Best Used Human-in-the-Loop**: Zero-shot reconstruction from isolated bullet cards still leaves semantic synthesis traces (`AUC = 1.00` against raw pre-2023 human manuscripts containing natural quirks). For best results, **draft core technical claims and causal mechanisms yourself (or interactively with full experimental context), then run this plugin to enforce structure, clarity, earned detail, captions, and de-AI discipline**.

---

## Empirical Research Reports (`docs/`, in Chinese)

- **Executive Synthesis**: [00_executive_synthesis.md](./docs/analysis/00_executive_synthesis.md)
- **01 · Structure & Story Arc**: [01_structure_and_story_arc.md](./docs/analysis/01_structure_and_story_arc.md)
- **02 · Title, Abstract & Golden First Two Pages**: [02_title_abstract_intro.md](./docs/analysis/02_title_abstract_intro.md)
- **03 · Motivation & Background**: [03_motivation_and_background.md](./docs/analysis/03_motivation_and_background.md)
- **04 · Design & Detail Control**: [04_design_and_detail_control.md](./docs/analysis/04_design_and_detail_control.md)
- **05 · Evaluation, Related Work & Venue Matrix**: [05_evaluation_and_related_work.md](./docs/analysis/05_evaluation_and_related_work.md)
- **06 · Lexicon, Style & Anti-Patterns**: [06_lexicon_style_and_antipatterns.md](./docs/analysis/06_lexicon_style_and_antipatterns.md)
- **07 · Intra-Paragraph Logic & Cohesion**: [07_paragraph_logic_and_cohesion.md](./docs/analysis/07_paragraph_logic_and_cohesion.md)
- **08 · Stylometry & 15-Year Evolution**: [08_stylometry_and_evolution.md](./docs/analysis/08_stylometry_and_evolution.md)
- **09 · Figures, Tables, Visuals & 671 Captions**: [09_figures_tables_and_visuals.md](./docs/analysis/09_figures_tables_and_visuals.md)
- **Blind Verification Benchmark (468 Verdicts)**: [final_benchmark_report.md](./docs/verification/final_benchmark_report.md)

---

## Copyright & Ethics Notice

This repository contains **only** original plugin configurations, writing rules, empirical analysis reports, and brief fair-use scholarly citations with full venue attribution. No copyrighted full-text papers, PDFs, or rendered paper figures are included.

## License

Released under the [MIT License](./LICENSE).

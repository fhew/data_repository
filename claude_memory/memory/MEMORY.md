# Kraken Project Memory

## Memory files

- [Doc-drift on file deletion](feedback_doc_drift.md) — grep markdowns before `git rm`; codified in CLAUDE.md
- [Starting-state memory before compaction](feedback_starting_state_memory.md) — meta-pattern: capture decisions + safety nets + open questions when context is about to compact and substantial work is queued
- [Phase 1 starting state](project_phase1_starting_state.md) — cohort refactor decisions + parity test, captured 2026-04-16 pre-compaction
- [Git commit conventions](feedback_git_commits.md) — no Co-Authored-By, keep messages short

## User Preferences

- Values educational insights during development — explain domain reasoning, not just code
- Wants development notes documented in `docs/development/` for features involving domain knowledge or architecture decisions
- Prefers structured, side-by-side comparison layouts in Streamlit (target gene vs partner gene columns)
- Professional tone, no emojis

## Project Patterns

- All external API calls: `@st.cache_data(ttl=3600)`, `timeout=10`, try/except with logger.error
- CSV data files go in `/data/`, helper modules in `/helpers/`
- Knowledge Base (`data/knowledge_base.csv`) stores per-gene biological assessments via Polars
- Gene selection uses `gene_selection.render_gene_selection()` returning (target_gene, partner_gene)
- UniProt data already fetched early in general_info.py — reuse `target_uniprot`/`partner_uniprot` dicts for downstream sections

## Key Files

- `pages/general_info.py` — Biological info page (~1700 lines), has sections for gene info, protein properties, internalization, 3D structure, pathways, interactions, literature
- `helpers/knowledge_base_helpers.py` — KB CRUD with Polars, pattern reference for new helpers
- `helpers/internalization_helper.py` — Three-source internalization data (curated CSV + QuickGO API + KB notes)
- `config.py` — Centralized config with `AnalysisConfig`, `UIConfig`, `DatabaseConfig` dataclasses
- `CLAUDE.md` — Project-level instructions (now tracked in git as of 2026-04-16)

## Universal Pool / Run-Centric Architecture (refreshed 2026-04-16)

- **Single-sweep model.** The two-pass (canonical → all-transcripts) was collapsed in the 2026-04 refactor. `run.py` has one `_run_full` path; `analysis_pass` column was dropped from schema.
- **Run-centric DuckDB.** `pair_coverage` / `pair_overall` keyed by `(run_id, ...)`. `analysis_runs` table holds `config_yaml` plus denormalized parameter columns. Re-running same config resumes via deterministic `run_id` hash; changing parameters auto-creates a new run.
- **Gene-level views.** `pair_coverage_gene` and `pair_overall_gene` collapse transcripts via MAX-per-indication for coverage and sample-weighted average for Spearman/MEI. Gene-level is the Explorer default.
- **Surface filter.** `gene_metrics.has_transmembrane` flag from UniProt topology. `require_transmembrane: true` in `universal.yaml` gates the pool at construction time; competitor targets bypass to preserve GPI-anchored ADC targets.
- **Canonical provenance.** `transcript_metadata.canonical_source` ∈ {`adc_override`, `mane_select`, `first_sorted`}. Most genes currently fall through to `first_sorted` because the MANE Select CSV is unpopulated for the full pool — building it is an open follow-up in IMPROVEMENTS.md.
- **Files:** `automated_analysis/modules/db_writer.py` (schema), `run.py` (orchestrator), `gene_manager.py` (pool construction with TM gate). Full docs: `docs/development/universal_list_architecture.md`.

## Domain Context

- ADC = Antibody-Drug Conjugate: antibody binds surface target, internalizes, releases cytotoxic payload in lysosomes
- Internalization speed/pathway/fate are critical ADC design parameters
- GESP scores (Hu et al. 2021) validate surface protein status — genes with Core GESP >= 4 are confirmed surface proteins. Sensitivity-tuned, so post-hoc filter with UniProt Transmembrane to suppress intracellular false-positives (Rab, Rho, ribosomal, catenins).
- GENCODE v23 legacy names require mapping (e.g., NECTIN4 -> PVRL4 in the database)

---
name: Phase 1 (subtype-cohorts) starting state and locked decisions
description: Decisions, parity test, and follow-up state captured before context compaction on 2026-04-16, just before Phase 1 begins.
type: project
originSessionId: 7de990dc-790b-45b5-906c-bc86de339ac9
---
Phase 1 of the subtype-cohort upgrade (`feat/subtype-cohorts` branch) refactors `core/bispecific_metrics.py` and the batch pipeline to be cohort-agnostic. Before context compaction on 2026-04-16, the following decisions were locked in and the following safety nets were put in place. Read these before starting Phase 1 work.

**Why:** Pre-compaction state capture so the Phase 1 refactor doesn't relitigate decisions or miss the parity gate.

**How to apply:** When Phase 1 work resumes, read `docs/development/subtype_cohort_architecture.md` for the full plan and check the items below for state that was decided in this session and isn't necessarily in the doc yet.

## Decisions locked in

1. **Cohort-level priority (Option A) supersedes indication-level.** Decided 2026-04-16. Priority is a property of the patient sample group (cohort), not the disease category. NEPC is the canonical example: generic Prostate Cancer is P2 for the pipeline, but NEPC subtype within mCRPC is P1. `data/indications/indications.csv` keeps its mapping/metadata role (TCGA join, indication name, sample counts) but sheds the `priority` and `select` columns to cohort YAMLs. Compatibility cohorts (TCGA studies) inherit priority from `indications.csv` at migration time so existing analyses keep working.

## Safety nets in place

1. **Parity snapshot test:** `scripts/test_pipeline_parity.py` captures schema, row counts, and aggregate hashes for every run in the DuckDB. The golden file `tests/parity_golden.json` was captured 2026-04-16 against ITGB4 + CDH17 fixed-partner runs. After Phase 1 lands, run `python scripts/test_pipeline_parity.py verify data/results/universal.duckdb tests/parity_golden.json` — any change in metric values, schema, or row counts fails the test.
2. **Doc-drift convention:** When a Python module is removed/renamed/moved, grep for its name in `*.md` files BEFORE committing. Codified in `CLAUDE.md` under "Refactoring Hygiene." The cohort refactor will move plenty of code surface; this convention applies.

## Pre-Phase 1 prep done

1. **MANE Select canonical CSV refresh** (in progress at compaction time, ~30 min Ensembl REST sweep): regenerates `data/canonical_transcripts.csv` for the full universal pool (~1,749 genes). Before this, most genes fell through to `canonical_source = "first_sorted"`. After this, they get proper MANE Select picks.

## Open questions still unanswered (need user input at Phase 1 kickoff)

1. Feature flag on Phase 1, or rely on additive compatibility (existing TCGA analyses unchanged)?
2. PBTA release version — OpenPBTA v23 vs OpenPedCan latest. (Phase 2a, but worth knowing the answer for Phase 1's compatibility-cohort generator.)
3. Pediatric normal coverage aggressiveness — BrainSpan ingest required before v1 pLGG output, or caveat flag sufficient? (Phase 2a.)
4. AR/NE signature choice — Labrecque 2019 is the reference; Beltran NE score and Tsai AR activity are alternatives. (Phase 2b.)

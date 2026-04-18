---
name: Phase 2a pLGG scaffold ready (awaits data)
description: Phase 2a code + docs + setup.py integration complete; blocked only on PBTA data download
type: project
originSessionId: a304eb01-cfde-4c39-9d2b-1e9a6c019e34
---
Phase 2a (pediatric low-grade glioma ingest) scaffold is committed on `feat/phase1-cohort-refactor`. Runs to completion on its own via `scripts/setup.py` — no further code work needed until data arrives and we iterate on column-probe heuristics.

**Source choice:** OpenPedCan v15 (not Treehouse 25.01). Treehouse publishes gene-level log2(TPM+1) only; OpenPedCan publishes transcript-level `rna-isoform-expression-rsem-tpm.rds` which matches our existing schema. OpenPedCan is dataset-neutral in v15 — files live under `https://s3.amazonaws.com/d3b-openaccess-us-east-1-prd-pbta/open-targets/v15/`, filter by `cohort == "PBTA"` in `histologies.tsv` to isolate PBTA samples.

**GENCODE version skew is real:** OpenPedCan uses GENCODE v27, existing Kraken SQLite uses GENCODE v23 (Xena Toil Recompute). Transcript-ID overlap ~90-95%. `scripts/ingest_pbta.py` has a 15% loss-ratio gate (`--loss-threshold 0.15`, configurable) that refuses the ingest if reconciliation drops more than that fraction.

**Cohort rules documented in `docs/development/plgg_ingest.md`:** plgg_all + plgg_pilocytic_astrocytoma + plgg_ganglioglioma + plgg_dnet + plgg_pxa (histology); plgg_braf_fusion + plgg_braf_v600e + plgg_nf1_loss + plgg_braf_wt (molecular). All carry `pediatric_caveat: true, normal_reference_tier: adult_gtex` — the Explorer surfaces a warning banner when any such cohort is selected.

**`scripts/setup.py` now runs the ingest** as the final step, opt-out via `--skip-pbta`, release pinnable via `--pbta-release v16` when newer releases drop. Requires `pyreadr` (now in requirements.txt) for the .rds expression matrix.

**Known probe fragility:** fusion + SNV MAF column-name probes in `ingest_pbta.py` were widened after inspecting real v15 headers (added `sample` + `kids_first_biospecimen_id_tumor` etc.). If a future OpenPedCan release changes column names again, the probes may need re-widening — the script reports clearly which column names it couldn't match.

**How to apply:** When PBTA data lands, `python scripts/setup.py --skip-expression --skip-depmap --skip-synlethdb --skip-tcga --skip-incidence --skip-competitors --skip-proteomics` runs the ingest alone; the full `python scripts/setup.py` on a fresh machine does everything including PBTA.

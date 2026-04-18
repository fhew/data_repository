---
name: doc-drift on file deletion is a recurring pattern in this repo
description: When deleting/renaming/moving files in Kraken, grep markdowns for the path before committing. Codified as a convention in CLAUDE.md.
type: feedback
originSessionId: 7de990dc-790b-45b5-906c-bc86de339ac9
---
When you delete a file, rename a module, or move a path in this repo, grep the repo for its name in `*.md` files BEFORE committing the deletion. Treat any markdown reference to a non-existent path as a doc bug to fix in the same commit.

**Why:** April 2026 audit found two cases of doc drift: (1) a deleted `parallel_processor.py` still documented in `automated_analysis/README.md` as a 572-line module, and (2) a deleted `automated_analysis_v2.py` still documented in `scripts/ANALYSIS_METRICS_REFERENCE.md`. New contributors reading the docs would be misled. The repo accumulates these silently because the file system doesn't enforce doc consistency.

**How to apply:** Run `grep -rn "<filename>" --include="*.md" .` before any `git rm` or `git mv` of a Python file, README cluster, or top-level directory. Roll the markdown updates into the same commit as the code change. Same applies to renames — the path string in docs is part of the rename surface.

This convention is now in `/home/wessel/code/kraken/CLAUDE.md` under "Refactoring Hygiene" so it travels with the repo for any contributor (human or AI). The memory entry is about the broader pattern: the user values documentation that doesn't lie about reality, and will appreciate proactive doc-sync work during refactors even when not explicitly asked.

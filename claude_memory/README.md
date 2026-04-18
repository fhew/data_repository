# Claude Code memory + transcripts — Kraken project

Snapshot of the project-specific Claude Code state for the Kraken
codebase, taken on 2026-04-18 before a WSL VHDX compaction / PC
migration.

## What's here

- `memory/` — auto-managed knowledge about the project (user
  preferences, feedback, project state). Small, hand-curated.
- `*.jsonl` — session transcripts. Each UUID.jsonl is one conversation
  session's full message log.
- `<uuid>/` directories — per-session auxiliary state.

## Restore on a new PC

1. Install Claude Code.
2. Open the Kraken repo once in Claude Code to create the project slug
   directory:
   `~/.claude/projects/-home-<user>-code-kraken/`
3. Copy the contents of this folder (except this README) into that
   directory. Overwrite any empty files Claude created.
4. On the next Claude Code session in the Kraken project, memory and
   past transcripts will be visible.

## Not included (on purpose)

- `.credentials.json` — never push auth to git. Re-log in on the new PC.
- `settings.local.json` — machine-specific config.
- Other projects' memory / transcripts — only Kraken is here.

## Freshness

The `*.jsonl` with the newest timestamp is the active (or most recent)
session. Older files are archived sessions kept for historical
searchability.

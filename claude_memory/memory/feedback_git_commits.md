---
name: Git commit conventions
description: No authorship attribution in commit messages; keep them short.
type: feedback
originSessionId: a304eb01-cfde-4c39-9d2b-1e9a6c019e34
---
Do not add `Co-Authored-By` lines (or any other authorship attribution for me) to git commit messages. Keep commit messages short — a concise subject line plus at most a brief body when the "why" needs explanation.

**Why:** User preference expressed 2026-04-18 when I drafted a verbose commit with a Claude co-author tag. They rejected the commit before it ran.

**How to apply:** Any time I'm asked to commit code on this project:
- No `Co-Authored-By: Claude ...` footer.
- No `🤖 Generated with ...` line.
- Subject line ≤72 chars, imperative voice.
- Body only when non-obvious context is needed; otherwise subject alone.

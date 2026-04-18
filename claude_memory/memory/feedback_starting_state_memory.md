---
name: Write a starting-state memory before context compaction
description: When context is about to compact and substantial work is queued for the next session, leave a project-type memory capturing decisions, safety nets, and open questions.
type: feedback
originSessionId: 7de990dc-790b-45b5-906c-bc86de339ac9
---
When context is about to compact AND a substantial piece of work is queued for the next session, write a project-type memory capturing the starting state for that work — decisions locked in this session, safety nets put in place (tests, golden files, conventions), and open questions still unanswered.

**Why:** User validated this pattern explicitly on 2026-04-16: "I like that idea of yours." The trigger was Phase 1 of the cohort refactor — substantial work that needed the prior session's context (NEPC priority decision, parity test, MANE regen) to start cleanly. Writing it down beat hoping I'd reconstruct it from scattered conversation.

**How to apply:**

- Trigger conditions: (1) context budget is near compaction, AND (2) the next session has a discrete substantial piece of work queued. Both conditions matter — don't write a starting-state memory after every casual chat.
- Use type=project (not feedback) for the starting-state itself, since the content is project-specific. This feedback memory documents the *meta-pattern*; the actual content goes in a separate project memory.
- Three sections work well: decisions locked in, safety nets in place, open questions still unanswered.
- Reference checked-in artifacts (test scripts, golden files, doc paths) so post-compact me can verify the state independently rather than trusting the memory.
- File-name pattern: `project_<feature>_starting_state.md` so the index is self-explanatory.

This pattern beats scattered conversation history because compaction can lose decisions made in a single message exchange. The memory file persists.

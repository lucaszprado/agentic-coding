---
name: reconcile-work
description: Reconcile implementation with the memory bank, update progress, and capture durable project decisions.
---

Use this skill when a scope or a meaningful part of it has been implemented and documentation must be synchronized.

## Instructions
1. Read only the memory bank files relevant to this workflow located at `memory_bank/`:
2. Focus on `active_context.md` and `progress.md`
2. Inspect what was actually implemented.
3. Compare codebase implementation against what is written in `active_context.md` and `progress.md`
4. Update:
   - `active_context.md` to reflect completed and pending VDTs
   - `progress.md` to reflect scope-level progress
   - `system_patterns.md` and `tech_context.md` only when implementation introduced durable changes
5. Call out mismatches between the documented plan and the implemented reality.
6. Keep conclusions factual and concise.

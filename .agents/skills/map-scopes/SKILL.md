---
name: map-scopes
description: Map or reshape project scopes, discuss trade-offs, and update scope-level project sequencing in the memory bank.
---

Use this skill when the project needs initial scope discovery, project slicing, or major rescoping.

## Instructions
1. Read only the memory bank files relevant to this workflow located at `memory_bank/`:
 - Focus on `project_brief.md` and `progress.md`
 - Read other files only if you still need more context

2. Treat blank `scope_context.md`, `active_context.md`, or sparse `progress.md` as valid signals that the project is still being mapped.
3. Identify candidate scopes to implement the project objective as integrated, testable slices with minimal cross-scope dependency. Prefer slices that:
- can ship meaningful value independently
- integrate backend and frontend when appropriate
- minimize dependency on other scopes
- keep review surface reasonably bounded
- can later be decomposed into VDTs cleanly
4. Explain trade-offs, sequencing risks, and what is must-have versus later-stage work.
5. Ask only the clarifying questions that materially affect scope boundaries.
6. Once the user agrees, update:
   - `progress.md` as the primary artifact
   - `system_patterns.md` and `tech_context.md` only if project-level decisions changed
7. Keep the output at scope level, not VDT level.

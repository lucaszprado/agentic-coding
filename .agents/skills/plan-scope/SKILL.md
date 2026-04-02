---
name: plan-scope
description: Turn the current scope into concrete value delivery tasks, implementation notes, and a reviewable delivery plan.
---

Use this skill when a scope is selected and the next step is to define how it will be delivered.

## Instructions
1. Read only the memory bank files relevant to this workflow located at `memory_bank/`:
2. Focus on `scope_context.md` and `progress.md`
3. Break the scope into VDTs that produce a clear, testable increment.
4. Prefer slices that reduce file sprawl and avoid unnecessary context switching.
5. Explain important implementation trade-offs and dependencies.
6. Once approved, update:
   - `active_context.md` as the primary artifact
   - `scope_context.md` if the scope definition itself changed
   - `system_patterns.md` and `tech_context.md` only for durable decisions
7. Do not implement code as part of this skill unless the user explicitly asks to move into execution.

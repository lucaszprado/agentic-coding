This README defines the purpose, reading order, and update rules for the memory bank, your long term memory.

The memory bank is the project-state layer for the coding agent. It should contain only the information that helps the agent understand what is being built, why it matters, what constraints apply, and what has already been decided.

All files mentioned in this README.md are inside `memory_bank/`.

# Software development project definitions
Two concepts are important to understand the project development process: scope and value delivery tasks — VDT.
- A project is composed by one or more scopes.
- Scopes are integrated slices of work that delivers a clear, testable increment and can be completed **independently** or with minimal dependency on other scopes.
- A good scope minimizes context switching and keeps code review manageable (ideally less than 10 files substantially changed).
- A scope is broken into value deliver tasks — VDTs, which are the concrete pieces of work required to complete that scope.

# Reading order
Read files in this order:
1. `project_brief.md`: Describe the overall project goals in term of the problem, solution and overall organization.
2. `system_patterns.md`: Document what are the overall design patterns in the project.
3. `tech_context.md`: Bring stack choices in the project.
4. `scope_context.md`: Explain what's the current scope under development.
5. `active_context.md`: VDTs and key information to complete a scope.
6. `progress.md`: required scopes to complete the overall project and not only the current scope and key information to complete the project.

# Update policy
Not every workflow updates every file.
Please keep the memory bank files compliant with the scaffold.

## Stable memory
Update only when durable project knowledge changes:
- `project_brief.md`
- `system_patterns.md`
- `tech_context.md`

## Session-state memory
Update as scope work advances:
- `scope_context.md`
- `active_context.md`
- `progress.md`

# Workflow usage

Do not infer missing information if a file is empty.
Empty state is a valid and intentional signal.

## 1) Context acquisition
Used when:
- Starting a new Codex session
- The agent needs repo and project orientation
- The user explicitly asked you to invoke $get-context skill
Expected behavior:
- Read the memory bank.
- Summarize current project, current scope, constraints, and open items.
- Do not modify files.

## 2) Scope mapping
Used when:
- The project still needs scope discovery or when major rescoping is required.
- The user explicitly asked you to invoke $map-scopes skill.
Expected behavior:
- Discuss project slices, trade-offs, dependencies, and milestones.
- Produce or update scope-level project sequencing.
Primary artifact:
- `progress.md`
Secondary artifacts when needed:
- `system_patterns.md`
- `tech_context.md`

## 3) Scope planning
Used when:
- A current scope exists and must be broken into value delivery tasks.
- The user explicitly asked you to invoke $plan-scope skill.
Expected behavior:
- Translate the active scope into reviewable VDTs.
- Record must-haves, implementation notes, and immediate delivery plan.
Primary artifact:
- `active_context.md`
Secondary artifacts when needed:
- `scope_context.md`
- `system_patterns.md`
- `tech_context.md`

## 4) Reconcile work
Used when:
- After implementation of a scope or a meaningful part of it has been implemented.
- The user explicitly asked you to invoke $reconcile-work skill.
Expected behavior:
- Reconcile what was implemented with what was planned.
- Mark completed VDTs.
- Update scope and project progress.
Primary artifacts:
- `active_context.md`
- `progress.md`
Secondary artifacts when needed:
- `system_patterns.md`
- `tech_context.md`

# File scaffolds
See the structure for each file at `/memory_bank/scaffolds.md`
This file brings the scaffolds for each file with an example.
`<...>` in this file indicates place holder.

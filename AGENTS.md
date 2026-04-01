# Codex project instructions

This repository uses a structured workflow built on top of `memory_bank/` and reusable Codex skills.
All paths in this file as written relatively to the repository root folder.


## Source of truth split
- `AGENTS.md`: stable repository-wide operating rules.
- `memory_bank/`: project and scope state.
- `.agents/skills/`: reusable workflows.

Do not duplicate the same long instructions across all three layers.


## Workflow selection
Prefer direct implementation for clear coding requests.
Prefer workflow skills for context loading, planning, project slicing, reconciliation, or validation:
- Need only orientation or repo understanding → use the `get-context` skill.
- Need to discover or reshape project scopes → use the `map-scopes` skill.
- Need to define or refine the current scope into value delivery tasks → use the `plan-scope` skill.
- Need to document what was completed and reconcile memory bank state → use the `reconcile-work` skill.
- Need to validate implementation through checks or tests → use the `run-tests` skill.

When implementation depends on missing project context or unresolved scope boundaries, invoke the appropriate workflow skill before coding.




## Core behavior rules
- Prefer scope boundaries that produce integrated, testable increments with low cross-scope dependency.
- Keep changes reviewable and localized when possible.
- Respect existing architecture and conventions before introducing new patterns.
- When introducing a durable architectural or technical decision, update the relevant memory bank files.
- Only read `memory_bank/` files when explicitly invoking a workflow skill that requires them.
- Do not rewrite memory bank files casually during execution. Only update them when invoking a pre-defined workflow built on top of skills.
- Do not mix workflow responsibilities:
  - Planning workflows must not perform implementation.
  - Reconciliation workflows must not perform code implementation neither introduce design decisions not backed by the current implementation.
  - Workflow skills should stay focused on their primary purpose.
- Treat memory updates in two categories:
  - Session-state updates: current scope, VDT status, immediate next steps.
  - Stable updates: architecture, technical constraints, enduring project decisions.
- Prefer explicit explanation of trade-offs when recommending scope boundaries.
- Use tests and verification steps before claiming completion whenever a testing workflow is available.

## Editing and command behavior
- Before making substantial edits, explain the intended change briefly.
- When the task is ambiguous, clarify goals through the planning workflow instead of guessing.
- Prefer incremental edits over large speculative rewrites.
- Prefer repository-native commands and scripts.

## Documentation standards
- Keep memory bank files concise, factual, and easy to scan.
- Preserve the scaffold and headings defined in `memory_bank/README.md`.
- Use YARD where code documentation is needed in Ruby code.

## Design principles
- Ruby on Rails best practices
- MVC and clear separation of concerns
- SOLID where it improves maintainability
- DRY without forcing premature abstraction

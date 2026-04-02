# Lightweight Agent Orchestration via Files

This repository uses a lightweight agent orchestration layer built from plain files instead of a dedicated orchestration framework.

The goal is to make coding-agent behavior more predictable by separating:

* **repository-wide operating rules** in `AGENTS.md`
* **project and execution state** in `memory_bank/`
* **reusable workflows** in `.agents/skills/`

## Why this exists

Coding agents are good at local execution but often inconsistent at:

* loading the right project context
* planning work at the right level
* preserving durable decisions
* reconciling implementation with prior plans

This repository addresses that by introducing a small file-based structure that helps the agent reason in consistent modes.

## Structure

### `AGENTS.md`

Defines stable repository-wide guidance, including:

* workflow selection
* behavior rules
* documentation standards
* design principles

### `memory_bank/`

Stores project state and long-lived context.

Typical contents include:

* `project_brief.md`
* `system_patterns.md`
* `tech_context.md`
* `scope_context.md`
* `active_context.md`
* `progress.md`

The folder also includes:

* `memory_bank/README.md` — explains reading order, update policy, and workflow usage
* `memory_bank/scaffolds.md` — defines the scaffold for each memory bank file

### `.agents/skills/`

Contains reusable workflow skills that operate on the memory bank.

Current skills:

* `get-context` — load and summarize project state
* `map-scopes` — define or reshape project scopes
* `plan-scope` — break a scope into value delivery tasks
* `reconcile-work` — reconcile implemented work with project memory
* `run-tests` — validate changes using repository-native checks

## Operating model

This system distinguishes between two kinds of agent work:

1. **Direct implementation**

   * used for clear coding tasks
   * the agent edits code directly when the request is already well-defined

2. **Workflow-driven execution**

   * used when the agent needs orientation, planning, scope mapping, reconciliation, or validation
   * these workflows use the skills and memory bank files to keep work consistent

## Design goals

* keep context loading intentional
* reduce unnecessary memory-bank reads
* preserve durable technical decisions
* make project planning explicit
* keep execution aligned with implemented reality
* remain simple enough to maintain as plain Markdown files

## Who should read what

* New human contributors: start with this file, then read `AGENTS.md`
* Agent contributors: read `AGENTS.md`, then use `memory_bank/README.md` and the relevant skill
* Contributors updating project state: follow the scaffolds in `memory_bank/scaffolds.md`

## Notes

This is intentionally a lightweight system.
It is not a replacement for tests, code review, or repository-native tooling.
It is a coordination layer that helps the agent use them more consistently.

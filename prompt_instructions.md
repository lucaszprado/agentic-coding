# Introduction
- An interaction is a chat

# First Interaction
Chat name: [Project-BX] Project Name YYYYMMDD (e.g. [Project-B1] Cluster and Filter 20250815)
## Objective
- Discover / List all the projects VDT
- Organize VDT in scopes and in a logical execution sequence
- Fill-up `active_context.md` and `progress.md`

## Key instructions to build the prompt
1. `project_bref.md` `tech_context` and `system_patterns` should bring the project level information -> See ReadMe.
2. `scope_context.md` Describe the target project phase (if you broke the project into phases). Use the `scope_context.md` template do describe the phase. <br>
If the project has a single phase, leave it blank.
3. `active_context.md`: blank -> There's no VDT yet

# Second and next interactions
- Chat name: [Scope-BX] Scope Name YYYYMMDD (e.g. [Scope-B1] Filter and Update Logic 20250729) -> Keep the main scope logic with core files. Don't ask about details on it.
- Derived Chats to detail scope [Status | Scope-BX] Scope Name YYYYMMDD (e.g. [Done | Scope-B4] FIlter and Update Logic 20250729)
- Derived Chats to discuss VDT specific issues [Status | Scope-BX | X] Scope Name 20250729 (e.g. [Done | Scope-B4 | 1] FIlter and Update Logic 20250729)
## Objectives
- Discuss the implementation of the VDT (individually or in group)
- Build the code to implement each VDT


## Key instructions to build the prompt
1. `project_bref.md` keeps the same structure from the first prompt: describe overall project ans list phases.
2. `tech_context` and `system_patterns` brings only project level information.
3. `scope_context.md` now describes the scope under development (not the first phase of the project anymore)
4. `active_context.md` is pre-filled with VDTs descovered in the first interaction
5. `progress.md` updated with current project achievement


# Key Checkpoints - Commits
**stph: start of phase**
- When the `progress.md` is empty.

**phpl: phase planned**
- When `progress.md` is suggested. After map scopes skill.

**edph: End of Phase**
When the last scope was finished.

**stsc: start of scope**
- Before any register in `active_context.md` or `scope_context.md`

**scpl: scope planned**
- After `active_context.md` or `scope_context.md` are filled.

**edsc: end of scope**
- After reconcile
- Every file in memory bank is filled and reflect was whas built

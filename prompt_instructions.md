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
2. `tech_context.md` and `system_patterns.md` brings only project level information.
3. `scope_context.md` now describes the scope under development (not the first phase of the project anymore)
4. `active_context.md` is pre-filled with VDTs descovered in the first interaction
5. `progress.md` updated with current project achievement


# Key Checkpoints - Commits
**stpj: start of project**
- When the `progress.md` is empty and we have no (if any) phase based organization.
- We have the `project_brief.md` and initial constraints in `tech_context.md` and `system_patterns.md`

**pjpl: project planned**
- Doubts, decisions and issues about project objectives and key elements were solved. Only what can be solved yet remains open.
- Project inital scope mapping concluded.
- `progress.md` contais the scopes and phases to deliver the project


**edpj: end of project**
- Every scope from each planned phase is concluded.
- `tech_context.md` and `system_patterns.md` reflects the patterns adopted in the project.



˜˜**stph: start of phase**˜˜
- When the `progress.md` is empty.

Why: No need to mark the start of phase. Since we're planning per scope.

˜˜
**phpl: phase planned**
- When `progress.md` is suggested. After map scopes skill.
˜˜
Why: No need to mark the planning of phase. Since we're planning per scope.

˜˜
**edph: End of Phase**
When the last scope was finished.
˜˜
Why: No need to mark the end of a phase since we're planning per scope


˜˜
**stsc: start of scope**
- Before any register in `active_context.md` or `scope_context.md`
˜˜
Why: No need to mark the start of scope. Since from the last state it doens't change anything.

**scpl: scope planned**
- After `active_context.md` or `scope_context.md` are filled.

**edsc: end of scope**
- After reconcile
- Every file in memory bank is filled and reflect was whas built

**clts: cleaning up and testing**
- After commit a bug resolution or code cleaning in the context of a project.

### Git trailers
- Project-Name=\<project-name\> <br>
- Cycle-Step=\<key-checkpoint-code\> <br>
- Step-Name=\<scope-name\>

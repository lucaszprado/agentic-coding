---
name: get-context
description: Read the memory bank and summarize the current project state, scope state, constraints, and open issues without changing files.
---

Use this skill when the user starts a session, asks for orientation, or asks the agent to understand the current project before planning or editing.

## Instructions
1. Read the memory bank in the order defined by `memory_bank/README.md`.
2. Summarize:
   - project goal
   - active scope
   - active VDTs
   - relevant architecture and tech constraints
   - open decisions or missing information
3. Do not edit files.
4. Do not propose implementation details unless the user asks.


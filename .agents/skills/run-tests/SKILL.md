---
name: run-tests
description: Run the appropriate verification commands for the current change, interpret failures, and summarize what passed, failed, and what remains risky.
---

Use this skill when validating a change before completion or when the user explicitly asks for test execution.

## Instructions
1. Read `AGENTS.md`, `memory_bank/tech_context.md`, and any repository docs that define the test workflow.
2. Determine the narrowest useful test scope first.
3. Prefer fast validation before broad suites.
4. Report:
   - commands run
   - what passed
   - what failed
   - likely cause of failures
   - recommended next step
5. Do not claim success without evidence from command output.
6. If the repository exposes project-specific test commands, use them instead of inventing alternatives.

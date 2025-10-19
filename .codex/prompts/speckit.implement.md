---
description: Execute the implementation plan by completing all tasks in tasks.md while honoring manual validation and dependency minimalism.
---

## User Input

```text
$ARGUMENTS
```

You **MUST** consider the user input before proceeding (if not empty).

## Outline

1. Run `.specify/scripts/bash/check-prerequisites.sh --json --require-tasks --include-tasks` from the repo root and parse `FEATURE_DIR` plus `AVAILABLE_DOCS`. All paths must be absolute. For single quotes in args like "I'm Groot", use escape syntax: e.g. `'I'\''m Groot'` (or double quotes when possible).

2. **Checklist gate** (if `FEATURE_DIR/checklists/` exists):
   - Scan all checklist files.
   - Count total, completed (`- [x]`/`- [X]`), and incomplete (`- [ ]`) items.
   - Produce a status table, e.g.:
     ```
     | Checklist          | Total | Completed | Incomplete | Status |
     |--------------------|-------|-----------|------------|--------|
     | ux.md              | 12    | 12        | 0          | ✓ PASS |
     | manual-validation.md | 8   | 5         | 3          | ✗ FAIL |
     | dependencies.md    | 6     | 6         | 0          | ✓ PASS |
     ```
   - If any checklist has incomplete items, display the table and ask the user whether to proceed. Continue only if the user explicitly allows it.

3. Load implementation context:
   - **Required**: `tasks.md`, `plan.md`
   - **If present**: `data-model.md`, `contracts/`, `research.md`, `quickstart.md`, active checklists
   - Understand manual validation expectations (responsive breakpoints, accessibility, dependency audits).

4. **Project setup verification** (same rules as tasks.md Setup phase):
   - Determine which ignore files are needed based on stack (e.g., `.gitignore`, `.dockerignore`, `.eslintignore`, `.prettierignore`, `.npmignore`).
   - Verify or create missing ignore files with appropriate patterns for Next.js/TypeScript projects (`node_modules/`, `.env*`, `.next/`, `dist/`, `*.log`, etc.).
   - Keep additions minimal—avoid introducing tooling that expands dependencies.

5. Parse `tasks.md`:
   - Extract phases (Setup, Foundational, User Stories, Manual Review, Polish).
   - Record task IDs, descriptions, parallel markers `[P]`, story labels `[US#]`, and referenced files.
   - Build dependency graph respecting ordering and manual validation checkpoints.

6. Execute tasks sequentially by phase:
   - Complete Setup tasks before Foundational; Foundational before User Stories.
   - Within each story: follow the listed order (UI, hooks/lib updates, styling) then perform manual validation tasks (desktop/tablet/mobile walkthroughs, accessibility, dependency audit, documentation updates).
   - Only run `[P]` tasks in parallel when files and outcomes do not conflict.

7. Implementation principles (enforce after every task):
   - **Clean Code**: keep components small, readable, and self-explanatory.
   - **Simple UX**: ensure flows stay minimal; prune unnecessary UI.
   - **Responsive by Default**: verify Tailwind classes cover breakpoints; adjust as issues arise.
   - **Dependency Minimalism**: avoid adding packages; if unavoidable, capture justification and confirm constitution compliance.
   - **Testing Prohibition**: do not create automated test files or commands. All validation is manual.

8. Progress tracking and error handling:
   - After each completed task, mark it as `- [x]` in `tasks.md`.
   - Report progress by phase; highlight any blockers or dependency justification required.
   - If a task cannot be completed, log the reason, stop, and request guidance.

9. Completion validation:
   - Confirm all tasks are marked complete.
   - Ensure manual validation notes are recorded (typically in `quickstart.md` or dedicated checklist) with viewport + accessibility outcomes.
   - Summarize dependency state (“No new packages added” or list justifications).
   - Provide final status with recommended next steps (e.g., PR prep, deployment, additional walkthroughs).

Remember: automated tests are prohibited. Manual review, responsive verification, and dependency hygiene are the definition of done.

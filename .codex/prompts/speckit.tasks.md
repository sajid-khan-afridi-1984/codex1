---
description: Generate an actionable, dependency-ordered tasks.md focused on manual validation and responsive delivery.
---

## User Input

```text
$ARGUMENTS
```

You **MUST** consider the user input before proceeding (if not empty).

## Outline

1. **Setup**: Run `.specify/scripts/bash/check-prerequisites.sh --json` from the repo root and parse `FEATURE_DIR` plus `AVAILABLE_DOCS`. Ensure all paths are absolute. For single quotes in args like "I'm Groot", use escape syntax: e.g. `'I'\''m Groot'` (or double quotes when possible).

2. **Load design documents** (from `FEATURE_DIR`):
   - **Required**: `plan.md`, `spec.md`
   - **Optional**: `data-model.md`, `contracts/`, `research.md`, `quickstart.md`, existing `checklists/`
   - Treat `quickstart.md` as the source of current manual validation expectations.

3. **Execute task generation workflow**:
   - Extract tech stack guardrails (Next.js 15.5.6, React 19.1.0, Tailwind CSS 4.1.14) from plan + constitution; flag any deviation.
   - Parse user stories with priorities from the spec; map entities/endpoints if supporting docs exist.
   - Identify responsive design requirements, accessibility notes, and dependency constraints.
   - Create per-story task groups that deliver independently reviewable increments.
   - For each story, include manual validation tasks covering desktop, tablet, mobile, accessibility, and dependency audit.
   - Maintain a dependency chain: Setup → Foundational → Story phases → Polish.

4. **Generate `tasks.md`** using the structure from `.specify/templates/tasks-template.md`:
   - Populate feature name, goals, and manual validation plan per story.
   - Do **NOT** create any automated testing tasks; replace former test slots with manual walkthrough items.
   - Ensure every task has a unique checkbox entry following the required format.
   - Document dependency order, parallel opportunities, and implementation strategy (MVP first, incremental, parallel).

5. **Report**: Output the file path and summary:
   - Total task count + per-story counts
   - Parallel opportunities
   - Manual validation coverage per story (viewports + accessibility)
   - Dependency audit notes (list additional packages, or "None")

Context for task generation: $ARGUMENTS

`tasks.md` must be specific enough for another agent to execute without further clarification.

## Task Generation Rules

**CRITICAL**: Tasks must be organized by user story to enable independent implementation and **manual validation**.

### Checklist Format (REQUIRED)

Every task MUST follow:

```
- [ ] TNNN [P?] [Story?] Description with file path or scope
```

- Checkbox: always `- [ ]`
- Task ID: sequential `T001`, `T002`, …
- `[P]`: only when parallel execution is safe
- `[US#]`: required for story phases; omit in Setup/Foundational/Polish
- Description: explicit action + file path (or folder) and purpose

### Phase Structure

1. **Phase 1 – Setup**: Repository and styling groundwork (Tailwind entry points, layout primitives, shared tokens).
2. **Phase 2 – Foundational**: Shared utilities, data access, configuration, accessibility and responsive guidelines, manual validation checklist prep.
3. **Phase 3+ – User Stories (priority order)**:
   - Implementation tasks (UI, hooks, data wiring, styling).
   - Manual review tasks (desktop/tablet/mobile walkthroughs, accessibility checks, dependency audit).
   - Documentation updates (`quickstart.md`, checklists).
4. **Phase N – Polish & Cross-Cutting**: Documentation, refactors, performance tuning, security/accessibility hardening, final walkthrough.

Each story phase must close with manual validation tasks instead of automated tests.

### Dependency & Responsiveness Considerations

- Reference constitution principles explicitly when justifying new dependencies (ideally "None").
- Note responsive breakpoints and accessibility outcomes in tasks.
- Ensure manual validation tasks cite required breakpoints and assistive flows (keyboard/focus/contrast).
- Encourage removing redundant logic or styles to maintain clean code.

### Parallel Opportunities

- Mark `[P]` only when tasks touch disjoint files or configurations.
- Parallelization is common for styling + content adjustments, but never for manual validation steps.

### Deliverable Validation

Before writing the file, confirm:

- No automated testing references remain.
- Every user story includes manual validation coverage for desktop, tablet, mobile, and accessibility.
- Dependency review tasks appear at least once (often in Foundational or story completion).
- The Implementation Strategy section mirrors the template, emphasizing manual validation checkpoints.

Failure to meet any rule above must be reported instead of generating a partial tasks file.

# Feature Specification: Doit Goal Page Setup

**Feature Branch**: `001-goal-tracker-setup`  
**Created**: 2025-10-19  
**Status**: Draft  
**Input**: User description: "initial page setup - this application should be a goal tracking web app called 'doit'. There should be two columns - a left one where current goals are shown, along with how many days left the user has to achieve the goal, and a right one where completed goals are. Each goal can be 'checked' using a checkbox, and then either moved to the completed column or permanently deleted. To add new goals, a user can click on a button to open a new goal form in a modal (title and end date fields). Goals reaching their end date (within 3 days) are highlighted. Let's use a modern light theme with fun pastel colours."

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Track current goals (Priority: P1)

As a motivated user, I need to see all active goals with a clear countdown so I can focus on what is due soon.

**Why this priority**: Knowing what is outstanding is the core value of the page and informs every other action.

**Independent Test**: Load the page with sample active goals and verify days-left values, highlight treatment, and readability without interacting with completion or creation flows.

**Acceptance Scenarios**:

1. **Given** active goals with future end dates, **When** the user opens the page, **Then** each goal appears in the left column with its title and days left displayed.
2. **Given** an active goal whose end date is within three days (including overdue), **When** the user views the left column, **Then** that goal is visually highlighted with the designated pastel emphasis.

---

### User Story 2 - Resolve a goal (Priority: P2)

As a user finishing a goal, I want to mark it complete or remove it so the list reflects my progress.

**Why this priority**: Clearing items keeps the active list meaningful and provides a sense of accomplishment.

**Independent Test**: From the active list, mark one goal complete and confirm it moves to the completed column; mark a different goal for deletion and confirm it is removed after confirmation.

**Acceptance Scenarios**:

1. **Given** an active goal, **When** the user checks its box and chooses to move it to completed, **Then** the goal disappears from the left column and appears in the right column with completion details.
2. **Given** an active goal the user no longer wants, **When** the user checks its box and confirms deletion, **Then** the goal is permanently removed from both columns.

---

### User Story 3 - Add a new goal (Priority: P3)

As a user planning ahead, I want to add a goal with a deadline so it joins my current focus list.

**Why this priority**: Adding goals enables continual use of the tracker without leaving the page.

**Independent Test**: Trigger the add-goal modal, submit a valid title and end date, and confirm the new goal appears in the current goals column with the correct days left.

**Acceptance Scenarios**:

1. **Given** the user is on the goal page, **When** they click the add-goal button, **Then** a modal opens prompting for goal title and end date.
2. **Given** the modal has valid inputs, **When** the user submits the form, **Then** the modal closes and the new goal displays in the left column with a calculated days-left value.

---

### Edge Cases

- No active goals exist: show an empty-state message in the left column while keeping the add-goal action available.
- A goal's end date is in the past when the page loads: display it as overdue with zero or negative days left and apply the highlight style.
- Multiple goals share the same near-term deadline: all such goals should receive the highlight treatment without visual conflict.
- The user enters an end date earlier than the current date: block submission and show an inline validation message.
- Completed column contains no entries: show helpful guidance encouraging the user to track completions.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: The page MUST present two labeled columns: "Current Goals" on the left and "Completed Goals" on the right.
- **FR-002**: The system MUST list every active goal in the left column with its title and the number of days remaining until its end date.
- **FR-003**: The system MUST calculate days remaining by comparing the goal's end date to the current date, showing zero when due today and negative values when overdue.
- **FR-004**: The system MUST visually highlight active goals whose end date falls within three calendar days (including those overdue) using a shared pastel-accented treatment while preserving readability in the light theme.
- **FR-005**: Each goal entry MUST include a checkbox control that allows the user to initiate completion or deletion actions without navigating away.
- **FR-006**: When an active goal's checkbox is selected, the system MUST immediately mark the goal as complete, move it to the completed column, and surface a confirmation banner that offers undo and delete actions.
- **FR-007**: The confirmation banner MUST allow the user to undo the completion within a short timeframe so the goal returns to the active column without data loss.
- **FR-008**: Choosing the delete option from the confirmation banner MUST prompt for confirmation and, once confirmed, permanently remove the goal from both columns without residual artifacts.
- **FR-009**: The completed goals column MUST display each finished goal's title alongside its completion date and original end date for reference.
- **FR-010**: The interface MUST offer a prominently placed "Add Goal" button that opens a modal form requesting goal title and end date.
- **FR-011**: The add-goal modal MUST validate that the title is non-empty and the end date is today or later before allowing submission, and it MUST allow users to cancel without saving.
- **FR-012**: Upon successful submission, the new goal MUST be added to the active goals list with the correct days-remaining value and the modal MUST close.
- **FR-013**: The overall visual design MUST use a modern light theme anchored in pastel color accents while maintaining accessible contrast and legible typography.
- **FR-014**: All goal lists MUST update in place without requiring a full page refresh.
- **FR-015**: The active goals column MUST order entries by soonest end date first, automatically re-sorting as deadlines approach.

### Key Entities *(include if feature involves data)*

- **Goal**: Represents a user-defined objective with attributes: id, title, endDate, status (active or completed), completionDate (optional), and daysRemaining (derived at display time).
- **GoalAction**: Represents user-triggered transitions (complete or delete) capturing goal id, action type, action timestamp, and confirmation status for auditing user flows.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: 100% of active goals display the correct days-remaining value and highlight state during manual review of representative sample data.
- **SC-002**: Users can move an active goal to the completed column or delete it using no more than two interactions after checking the goal.
- **SC-003**: Newly added goals appear in the current goals column within one second of form submission during local review with standard dataset sizes (up to 50 goals).
- **SC-004**: Stakeholder design review confirms the page adheres to the requested modern light pastel aesthetic with no noted accessibility violations.

## Assumptions

- The initial page can rely on in-memory or mock data; persistence beyond the current session is out of scope for this specification.
- Days remaining calculations assume the local timezone of the viewer and treat due-today goals as zero days remaining.
- Deleting a goal is irreversible and therefore requires user confirmation to prevent accidental loss.
- Completed goals are sorted in descending order by completion timestamp for quick access to recent wins.
- Future enhancements (analytics, sharing, recurring goals) are excluded from this initial setup.

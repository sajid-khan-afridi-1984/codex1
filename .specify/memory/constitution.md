# Codex1 Constitution

## Core Principles

### I. Clean Code First
Favor lean components with intention-revealing names, clear data flow, and consistent patterns. Remove duplication quickly and keep files short enough to scan at a glance.

### II. Simple UX
Design the smallest experience that solves the problem. Limit cognitive load, keep copy concise, and ensure every interactive element has a single obvious outcome.

### III. Responsive By Default
Layouts must scale gracefully from mobile through desktop. Use fluid spacing, typography, and Tailwind responsive utilities to preserve usability across breakpoints and input methods.

### IV. Dependency Minimalism
Build with the platform: Next.js 15.5.6, React 19.1.0, React DOM 19.1.0, and Tailwind CSS 4.x cover the needs of this project. Adding new dependencies requires written justification plus a documented removal plan.

### V. Manual Quality Assurance Only (NON-NEGOTIABLE)
Automated tests of any kind (unit, integration, e2e, snapshot, lint-to-test bridges) are prohibited. Quality relies on careful code reviews, manual walkthroughs, and live previews.

## Delivery Constraints
- Keep runtime and build outputs free from unused code or experimental flags.
- Author UX copy, layout, and interactions with accessibility in mind: focus order, contrast, and keyboard support must remain intact.
- Document any noteworthy decisions inline or in accompanying notes so future contributors can understand trade-offs without spelunking through history.

## Workflow Expectations
- Maintain a concise manual validation script alongside each feature describing desktop, tablet, and mobile checks plus accessibility considerations.
- Audit dependency changes with every pull request; if a new package is unavoidable, capture why it is required and how it will be removed when no longer needed.
- Favor incremental commits and feature toggles that keep `main` deployable without relying on tests.

## Governance
This constitution supersedes all other guidance for the project. Amendments demand consensus from project maintainers and must document rationale, impact, and rollout steps before adoption.

**Version**: 1.0.0 | **Ratified**: 2025-10-19 | **Last Amended**: 2025-10-19

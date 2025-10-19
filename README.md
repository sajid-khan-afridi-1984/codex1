## Codex1 Principles

This project is governed by the `Codex1 Constitution` stored in `.specify/memory/constitution.md`. Every change must respect the following non‑negotiable rules:

- **Clean Code First** — Keep components lean, intention‑revealing, and well factored.
- **Simple UX** — Deliver the smallest, clearest flow that solves the user problem.
- **Responsive by Default** — Design layouts that adapt gracefully across breakpoints with accessible interactions.
- **Dependency Minimalism** — Use the built-in capabilities of Next.js 15.5.6, React 19.1.0, React DOM 19.1.0, and Tailwind CSS 4.1.14 before reaching for new packages.
- **Testing Prohibition** — Automated tests of any kind (unit, integration, e2e) are disallowed. Rely on manual review, live previews, and collaborative walkthroughs instead.

## Getting Started

Run the local development server with the `turbopack` dev tooling:

```bash
npm run dev
# or yarn dev / pnpm dev / bun dev
```

Open `http://localhost:3000` and iterate in `src/app/page.tsx` or supporting components. Tailwind CSS is available globally through `src/app/globals.css`.

## Manual Validation Workflow

Because automated tests are prohibited, every feature should include:

1. A brief manual validation script in `specs/<feature>/quickstart.md` covering desktop, tablet, and mobile breakpoints.
2. Notes on accessibility checks (keyboard navigation, focus order, contrast).
3. A dependency audit confirming no unnecessary packages were added.

Use `/speckit.checklist` to generate requirement-quality checklists that capture these review gates.

## Recommended Reading

- [Next.js App Router docs](https://nextjs.org/docs/app) — Focus on data fetching and routing patterns that keep client bundles slim.
- [Tailwind CSS 4](https://tailwindcss.com/docs) — Prefer utility-first styling and avoid custom CSS unless required.

Deployment remains compatible with the standard Next.js pipeline (e.g., Vercel). Ensure manual validation passes before shipping. Automated CI gates should exclude test commands per the constitution.

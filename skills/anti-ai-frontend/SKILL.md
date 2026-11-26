---
name: anti-ai-frontend
description: Prevent frontend UIs from looking generic or AI-generated ("AI slop") and enforce production-grade design systems. Use whenever designing, building, refactoring, reviewing, or auditing websites, landing pages, dashboards, SaaS products, web apps, or UI components—especially when choosing colors, typography, layouts, spacing, shadows, or interactive states, even if the user does not explicitly mention "AI slop".
license: MIT
metadata:
  author: ush
  version: "1.0.0"
---

# Anti-AI Frontend Engineering

Unconstrained LLMs converge on the statistical center of training data: purple/indigo gradients, `Inter` everywhere, centered hero + two pill buttons + three identical icon cards, muddy `shadow-xl` boxes, and happy-path-only states. Break out of that statistical average with mechanical constraints before writing markup.

**Core principle:** Design with intent. Lock tokens first. Engineer for every state.

---

## 1. Mandatory Design-First Workflow

Before writing component code:

1. **Inspect the codebase:** Check framework, existing components, styling conventions, and existing design tokens. Never overwrite an established design system without justification or duplicate existing components.
2. **Identify product context:** Determine the domain, target users, primary workflows, and visual identity archetype.
3. **Lock tokens & `DESIGN.md`:** Define a closed token set in `:root` CSS variables or `tailwind.config.*` and record constraints in `DESIGN.md` so subsequent edits cannot drift back to defaults.
4. **Plan composition & states:** Choose layout structure from content hierarchy and map all interactive/data states before coding.

> For domain archetypes, physical-material palette rules, `:root` CSS token templates, and a `DESIGN.md` starter, read [`references/design-tokens-and-archetypes.md`](references/design-tokens-and-archetypes.md).

---

## 2. Color & Surface Discipline

- **Ban startup clichés:** No default `indigo-500` / `purple-600` / `blue-500` gradients, neon mesh blurs, glowing buttons, or excessive glassmorphism.
- **Kill gradient hero text:** Never use `bg-clip-text text-transparent bg-gradient-to-r` on headings. Use solid, high-contrast ink.
- **Sample from reality:** Derive palettes from a tangible material or domain context (paper, ink, anodized aluminum, financial ledger, botanical, industrial hardware) rather than digital defaults.
- **Closed palette:** 1 primary neutral scale (warm or cool, intentional), 1 surface hierarchy (base, raised, recessed), **1 purposeful accent color**, plus semantic status colors only when required.
- **Crisp elevation over muddy shadows:** Replace heavy black `shadow-xl` with crisp `1px` borders (`border-neutral-200` / `white/10`) or subtle multi-layered shadows tinted to the background hue.
- **Micro-texture over ambient glow:** When a flat surface needs depth, use subtle CSS/SVG film grain (`feTurbulence` at ~2–3% opacity) instead of colorful radial blobs.

---

## 3. Typography Engineering

- **Intentional pairing:** Avoid defaulting blindly to `Inter`, `Roboto`, `Arial`, or `Open Sans`. Select at most two primary families (plus optional monospace) suited to the product—e.g., `Geist`, `Manrope`, `Satoshi`, `IBM Plex Sans`, `Plus Jakarta Sans`, `Instrument Serif`, `JetBrains Mono`.
- **Display polish:** Apply tight tracking (`-0.02em` to `-0.035em`) on display headings and explicit line-height ratios (`1.05–1.15` display, `1.45–1.6` body).
- **Constrain measure:** Cap prose line length (`max-w-[65ch]` / `max-w-prose`) so text never stretches across ultra-wide containers.

---

## 4. Layout & Composition

- **Ban the AI landing-page template:** Do not default to: centered hero + 2 pill buttons → 3 equal-width feature cards with floating outline icons in colored rounded boxes → pricing table with a glowing middle "Pro" card.
- **Let content dictate structure:**
  - Left-aligned hero paired with a real product preview, interactive state, or live data visualization.
  - Asymmetric bento grids with varied column/row spans (`col-span-2`, `row-span-2`) only where hierarchy warrants it.
  - Editorial single-column or split-pane flows for reading-heavy or tool-first interfaces.
- **Strict spacing rhythm:** Use a 4px/8px grid (`4, 8, 12, 16, 24, 32, 48, 64, 96px`). Keep coupled micro-elements tight (`4–8px`) and section breaks generous (`64–96px`). Never copy-paste `py-20` and `p-6` everywhere.
- **Restrained iconography:** Replace repetitive outline icons in rounded boxes with typographic hierarchy, real UI snippets, data, or minimal marks.

---

## 5. Interaction, Accessibility & Realism

- **No happy-path-only UI:** Every interactive component must handle `default`, `hover` (subtle border/tint shift, no violent `scale-105`), `active`, `focus-visible` (token-matched ring, never `outline-none` without replacement), `disabled`, `loading` (layout-matched skeletons for real async work only), `empty` (clear next action), and `error` (actionable recovery).
- **Motion with restraint:** Use `150ms–200ms cubic-bezier(0.16, 1, 0.3, 1)` animating only `transform` and `opacity`. Never scroll-jack (`window.scroll` listeners); use `IntersectionObserver`.
- **WCAG 2.2 AA & 2.2.2:** Semantic HTML, keyboard navigation, minimum `24×24` CSS px targets (`44×44` for touch), `prefers-reduced-motion` support, and visible pause/stop controls for any auto-playing video, ticker, or marquee.
- **Content realism:** Use domain-accurate names, labels, and metrics. Never fabricate testimonials, customer logos, performance claims, or fake loading/success states.

> For the full 9-state matrix, 10 data edge cases, responsive breakpoints (`320px–1920px`), performance rules, and the complete Visual + Engineering Audit, read [`references/production-checklists.md`](references/production-checklists.md).

---

## 6. Pre-Ship Anti-Slop Audit

Verify before finishing any frontend task:

1. Zero purple/indigo default gradients, neon blurs, or `bg-clip-text` hero headlines.
2. Closed token system with <= 1 primary accent; no ad-hoc hex codes or random spacing in components.
3. No uniform 3-card-with-outline-icon cliché unless explicitly requested.
4. Intentional typography with tight display tracking, explicit line-heights, and `<= 65ch` prose measure.
5. All interactive and data states (`hover`, `focus-visible`, `loading`, `empty`, `error`, long text, mobile `320px–375px` without overflow) handled.
6. Project build, lint, typecheck, and visual checks pass (never claim checks passed unless executed).

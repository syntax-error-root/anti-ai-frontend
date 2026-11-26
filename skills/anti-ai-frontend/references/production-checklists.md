# Production Engineering & Audit Checklists

Load this reference when implementing interactive states, responsive layouts, accessibility, performance optimizations, or running the final pre-ship audit.

---

## 1. Complete Interactive State Matrix

Never ship happy-path-only components. Every relevant interactive element must support:

| State | Requirement |
|---|---|
| **Default** | Clear visual baseline using centralized tokens |
| **Hover** | Subtle border, tint, or surface shift (avoid violent `scale-105`) |
| **Active** | Tactile press feedback |
| **Focus-visible** | Token-matched visible ring (never `outline-none` without replacement) |
| **Disabled** | Visually muted and non-interactive (`aria-disabled` / `disabled`) |
| **Loading** | Layout-matched skeleton or indicator for real async work only |
| **Empty** | Clear explanation + actionable next step (never a blank void) |
| **Error** | Specific, actionable recovery guidance |
| **Success** | Clear completion feedback (never fabricated) |

### Data & Edge-Case Handling
Explicitly handle:
1. Empty API responses
2. Network failures & timeouts
3. Invalid user input
4. Long strings (truncation / `line-clamp` / wrapping)
5. Missing or broken images
6. Zero values (`0`, `$0.00`, `0%`)
7. Large datasets (virtualization or pagination)
8. Pagination boundaries
9. Expired sessions
10. Permission errors

---

## 2. Responsive Engineering (`320px–1920px`)

Test and design intentionally across: `320px`, `375px`, `768px`, `1024px`, `1440px`, `1920px`.

- **No horizontal overflow** at any viewport width.
- **No clipped essential content**; adapt component composition on mobile rather than shrinking desktop layouts.
- **Readable tables & charts:** Use horizontal scroll wrappers, stacked card transforms, or priority columns on narrow screens.
- **Touch & target sizing:** Minimum `24×24` CSS pixels per WCAG 2.2 AA; prefer `44×44` CSS pixels for touch targets.

---

## 3. Accessibility & Motion Guardrails (WCAG 2.2 AA)

- **Semantic HTML first:** Use native `<button>`, `<a>`, `<nav>`, `<main>`, `<dialog>`, and `<label>` before reaching for `role` attributes.
- **Keyboard navigation:** Full Tab/Shift+Tab, Enter/Space, Escape for dialogs/menus, and arrow-key support where expected.
- **Contrast & screen readers:** Sufficient contrast ratios; `aria-live` status updates for dynamic feedback.
- **Motion:**
  ```css
  transition:
    transform 180ms cubic-bezier(0.16, 1, 0.3, 1),
    opacity 180ms ease,
    background-color 180ms ease,
    border-color 180ms ease;
  ```
  - Animate only `transform` and `opacity` where possible.
  - Respect `@media (prefers-reduced-motion: reduce)`.
  - **WCAG 2.2.2:** Any auto-playing video, ticker, or marquee MUST include a visible pause/stop control.
  - Never scroll-jack with `window.scroll` listeners; use `IntersectionObserver`.

---

## 4. Performance & Core Web Vitals

- Optimize images with explicit `width`/`height` (prevent CLS) and lazy loading below the fold.
- Optimize font loading (`font-display: swap`, subsetting, preload critical faces).
- Minimize client-side JS; prefer server rendering and code splitting where appropriate.
- Avoid unnecessary dependencies and layout-thrashing animations.

---

## 5. Full Pre-Ship Audit Checklist

### Visual Audit
- [ ] No generic AI landing-page composition (centered hero + 3 icon cards + glowing Pro tier).
- [ ] No default purple/indigo gradients, neon glows, or `bg-clip-text` hero headlines.
- [ ] Closed design token system documented in `DESIGN.md` with <= 1 primary accent.
- [ ] Intentional typography, tight display tracking, explicit line heights, `<= 65ch` prose measure.
- [ ] Crisp `1px` borders or background-tinted shadows instead of muddy `shadow-xl`.
- [ ] Realistic domain content; zero fabricated testimonials, metrics, or logos.

### Engineering Audit
- [ ] No unnecessary dependencies or duplicated components.
- [ ] All interactive & async states (`hover`, `active`, `focus-visible`, `disabled`, `loading`, `empty`, `error`) implemented.
- [ ] Edge cases (long text, zero values, missing images, network errors) handled.
- [ ] Responsive across `320px–1920px` with zero horizontal overflow.
- [ ] Keyboard accessible, WCAG 2.2 AA contrast/targets, `prefers-reduced-motion` + pause controls.
- [ ] Project build, lint, and type checks executed and passing after final edits.

# Design Tokens & Visual Archetypes

Load this reference during Step 2–3 of the Design-First Workflow when establishing visual direction, color palettes, CSS tokens, or `DESIGN.md`.

---

## 1. Domain Visual Archetypes

Select an archetype grounded in the product's domain, audience, and physical-world analogs rather than trends:

| Archetype | Visual Direction | Surface & Color Cues | Typography Cues |
|---|---|---|---|
| **Editorial** | Generous whitespace, asymmetric columns, hairline rules | Warm paper (`#f6f5f1`), ink (`#20211f`), 1 muted editorial accent | Serif display (`Instrument Serif`) + clean sans body (`IBM Plex Sans`) |
| **Industrial** | Structured grids, exposed 1px borders, zero-radius or tight `4px` corners | Brushed/anodized neutral grays, high-contrast black, safety accent | Geometric/grotesque sans (`Manrope`, `Geist`) + mono data |
| **Financial** | Dense scannable hierarchy, tabular numerals, calm contrast | Cool slate or off-white ledger surfaces, restrained emerald/amber semantics | `IBM Plex Sans` + `JetBrains Mono` (`tabular-nums`) |
| **Developer Tools** | Compact functional density, keyboard-first affordances, code/terminal clarity | Deep charcoal or crisp light neutral, 1 sharp focus accent | `Geist` / `Satoshi` + `JetBrains Mono` |
| **Luxury** | Controlled restraint, large scale contrast, material-inspired depth | Stone, linen, obsidian, muted metallic or earth accent | High-contrast serif or refined sans, wide tracking on small caps |
| **Consumer** | Expressive layout hierarchy, tactile interactive feedback | Clean neutral canvas + 1 vivid, purposeful brand accent | `Plus Jakarta Sans` / `Manrope` |

---

## 2. Starter `:root` CSS Token System

Adapt these illustrative values to the chosen product identity; never copy-paste blindly if the project already defines tokens or uses Tailwind theme config.

```css
:root {
  /* Color — closed neutral scale + 1 purposeful accent */
  --color-background: #f6f5f1;
  --color-surface: #ffffff;
  --color-surface-recessed: #eeede7;
  --color-foreground: #20211f;
  --color-muted: #6e7068;
  --color-border: #e4e3dc;
  --color-accent: #b65f3c;
  --color-accent-foreground: #ffffff;

  /* Semantic (add only when needed) */
  --color-success: #2a6f4e;
  --color-warning: #9a6700;
  --color-danger: #b42318;

  /* Typography */
  --font-display: "Manrope", system-ui, sans-serif;
  --font-body: "IBM Plex Sans", system-ui, sans-serif;
  --font-mono: "JetBrains Mono", ui-monospace, monospace;

  /* Spacing (4px/8px scale) */
  --space-1: 4px;
  --space-2: 8px;
  --space-3: 12px;
  --space-4: 16px;
  --space-6: 24px;
  --space-8: 32px;
  --space-12: 48px;
  --space-16: 64px;
  --space-24: 96px;

  /* Geometry */
  --radius-sm: 4px;
  --radius-md: 8px;
  --radius-lg: 12px;

  /* Motion */
  --duration-fast: 150ms;
  --duration-normal: 200ms;
  --ease-standard: cubic-bezier(0.16, 1, 0.3, 1);
}

.heading-display {
  font-family: var(--font-display);
  letter-spacing: -0.03em;
  line-height: 1.08;
}

.body-copy {
  font-family: var(--font-body);
  line-height: 1.55;
  max-width: 65ch;
}
```

### Token Governance Rules
- Zero arbitrary hex codes, pixel radii, or one-off spacing values inside components.
- For Tailwind projects, map tokens in `tailwind.config.*` or `@theme` so utilities stay consistent.

---

## 3. `DESIGN.md` Starter Template

Create or update `DESIGN.md` at the project root before writing UI components:

```markdown
# DESIGN.md

## Product & Visual Identity
- **Domain & Audience:** [Who uses this and for what primary workflow]
- **Archetype & Material Reference:** [e.g., Industrial / Anodized aluminum + technical paper]

## Closed Token Decisions
- **Neutrals & Surfaces:** [Base, raised, recessed, border hexes]
- **Primary Accent:** [Single accent hex + usage rule]
- **Typography:** [Display family, Body family, Mono family, measure cap]
- **Geometry & Elevation:** [Radius scale, 1px border vs. tinted shadow rule]

## Layout & Anti-Patterns
- **Primary Composition:** [e.g., Split-pane workspace / Asymmetric bento / Editorial flow]
- **Explicitly Banned:** Purple/indigo gradients, gradient hero text, 3-icon-card clichés, `shadow-xl`.
```

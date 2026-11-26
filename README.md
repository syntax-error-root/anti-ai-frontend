# anti-ai-frontend

An Agent Skill that prevents LLMs from generating generic "AI slop" UIs and enforces production-grade design systems, intentional composition, accessibility, and complete interactive states.

Compatible with **Claude Code**, **OpenAI Codex**, **Cursor**, **Gemini CLI**, and other `SKILL.md`-compatible agents.

## Installation

Install directly from GitHub using the `skills` CLI:

```bash
npx skills add syntax-error-root/anti-ai-frontend
```

## What It Enforces

- **Design-First Workflow:** Inspects existing tokens/components, establishes `DESIGN.md`, and locks a closed token set before writing markup.
- **Color & Surface Discipline:** Bans default purple/indigo gradients, neon glows, and `bg-clip-text` hero headlines; derives palettes from real-world materials with <= 1 primary accent.
- **Typography & Layout:** Intentional font pairings, tight display tracking, `<= 65ch` prose measure, and content-driven layouts (no uniform 3-icon-card clichés).
- **Complete States & Accessibility:** Requires `hover`, `active`, `focus-visible`, `disabled`, `loading`, `empty`, and `error` states, `320px–1920px` responsiveness, and WCAG 2.2 AA / 2.2.2 compliance.

## Skill Structure

```text
skills/anti-ai-frontend/
├── SKILL.md                                    # Core workflow, rules, and pre-ship audit
└── references/
    ├── design-tokens-and-archetypes.md         # Domain archetypes, :root CSS tokens, DESIGN.md template
    └── production-checklists.md                # 9-state matrix, edge cases, WCAG 2.2, full audit
```

## License

MIT

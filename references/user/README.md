# User Extensions — Arrow Design

Drop any markdown file here to extend or override Arrow Design's built-in references.

## How It Works

Files in this directory are loaded **before** built-in references and treated as authoritative. If a file here defines a token, constraint, or component spec, it wins over the defaults.

No edits to `SKILL.md` required — just drop the file and it's active.

## What to Put Here

| File | Purpose |
|---|---|
| `my-tokens.md` | Personal or project-specific design tokens (overrides design-system defaults) |
| `brand-[client].md` | Client brand specs — colors, fonts, logo rules |
| `component-library.md` | Component specs for a design system you already use |
| `motion-rules.md` | Custom animation timing, easing, duration rules |
| `skill-[name].md` | Extracted design rules from another skill you want to incorporate |
| `typography.md` | Font pairing rules, type scale preferences |

## Priority Order

1. **`references/user/`** ← you are here (highest priority)
2. **`references/`** — built-in Arrow Design references

## Format

Plain markdown. No special syntax required. Write it the way you'd explain it to a designer:

```markdown
# My Token Overrides

## Colors
- Primary: #1A1A2E (deep navy)
- Accent: #E94560 (red-orange)
- Surface: #F5F5F0 (warm off-white)

## Typography
- Display: Freight Display Pro, serif
- Body: Inter, sans-serif
- Scale base: 16px, 1.25 ratio
```

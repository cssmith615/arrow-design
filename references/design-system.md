# Arrow Design — Design System Reference

## Purpose

Every Arrow Design output begins with a design system bootstrap. This file defines the token vocabulary, generation rules, and enforcement standards that all output must follow.

---

## Token Generation Rules

### 1. Check User Extensions First

Before generating any tokens, check `references/user/` for existing token definitions. If a `my-tokens.md` or any file defining colors, type, or spacing exists there, use those values. Only generate defaults for tokens not already defined.

### 2. Output `design-system.css` First

The first deliverable for any project is a `design-system.css` file (or an inline `:root {}` block for single-file output). All subsequent HTML references these tokens — no hardcoded hex values, pixel sizes, or magic numbers.

### 3. WCAG 2.1 AA is the Floor

Color tokens must be generated so that:
- Body text (< 18pt / < 14pt bold) achieves ≥ 4.5:1 contrast ratio against its background
- Large text (≥ 18pt / ≥ 14pt bold) achieves ≥ 3:1
- UI components and focus indicators achieve ≥ 3:1

Generate contrast-safe pairings by default. Flag any pairing that fails — do not silently ship inaccessible color combinations.

---

## Token Vocabulary

### Color Tokens

```css
:root {
  /* Brand */
  --color-primary:        /* main brand color */;
  --color-primary-hover:  /* ~10% darker */;
  --color-secondary:      /* supporting brand color */;
  --color-accent:         /* high-attention moments only */;

  /* Surface */
  --color-bg:             /* page/app background */;
  --color-surface:        /* card/panel background */;
  --color-surface-raised: /* elevated surface (modal, dropdown) */;
  --color-border:         /* default border */;
  --color-border-subtle:  /* dividers, secondary borders */;

  /* Text */
  --color-text:           /* primary body text — must meet 4.5:1 on --color-bg */;
  --color-text-secondary: /* supporting text — must meet 4.5:1 on --color-bg */;
  --color-text-disabled:  /* disabled state */;
  --color-text-inverse:   /* text on dark/primary backgrounds */;

  /* Semantic */
  --color-success:        /* confirmation, positive states */;
  --color-warning:        /* caution, non-blocking issues */;
  --color-error:          /* destructive, blocking failures */;
  --color-info:           /* neutral informational */;

  /* Interaction */
  --color-focus-ring:     /* keyboard focus indicator — ≥ 3:1 against surroundings */;
}
```

### Typography Tokens

```css
:root {
  /* Families */
  --font-display:   /* heading/display typeface */;
  --font-body:      /* body/UI typeface */;
  --font-mono:      /* code, data */;

  /* Scale — 1.25 (Major Third) ratio, 16px base */
  --type-xs:   12px;
  --type-sm:   14px;
  --type-base: 16px;
  --type-md:   20px;
  --type-lg:   24px;
  --type-xl:   32px;
  --type-2xl:  40px;
  --type-3xl:  48px;

  /* Weights */
  --weight-regular: 400;
  --weight-medium:  500;
  --weight-semibold: 600;
  --weight-bold:    700;

  /* Line Heights */
  --leading-tight:  1.2;  /* headings */
  --leading-snug:   1.4;  /* subheadings, UI labels */
  --leading-normal: 1.6;  /* body text */
  --leading-loose:  1.8;  /* long-form reading */

  /* Letter Spacing */
  --tracking-tight:  -0.02em;  /* large display headings */
  --tracking-normal:  0em;
  --tracking-wide:    0.05em;  /* labels, caps */
  --tracking-wider:   0.1em;   /* small caps, overlines */
}
```

### Spacing Tokens

```css
:root {
  /* 4px base, 8px grid steps */
  --space-1:  4px;
  --space-2:  8px;
  --space-3:  12px;
  --space-4:  16px;
  --space-5:  24px;
  --space-6:  32px;
  --space-7:  40px;
  --space-8:  48px;
  --space-9:  56px;
  --space-10: 64px;
  --space-12: 80px;
  --space-16: 96px;
}
```

### Border Radius Tokens

```css
:root {
  --radius-none: 0;
  --radius-sm:   4px;
  --radius-md:   8px;
  --radius-lg:   12px;
  --radius-xl:   16px;
  --radius-2xl:  24px;
  --radius-full: 9999px;
}
```

### Elevation / Shadow Tokens

```css
:root {
  --shadow-0: none;
  --shadow-1: 0 1px 3px rgba(0,0,0,0.08), 0 1px 2px rgba(0,0,0,0.06);
  --shadow-2: 0 4px 6px rgba(0,0,0,0.07), 0 2px 4px rgba(0,0,0,0.06);
  --shadow-3: 0 10px 15px rgba(0,0,0,0.08), 0 4px 6px rgba(0,0,0,0.05);
  --shadow-4: 0 20px 25px rgba(0,0,0,0.10), 0 10px 10px rgba(0,0,0,0.04);
}
```

### Motion Tokens

```css
:root {
  /* Durations */
  --duration-instant: 100ms;
  --duration-fast:    150ms;
  --duration-base:    200ms;
  --duration-slow:    300ms;
  --duration-slower:  500ms;

  /* Easings */
  --ease-standard: cubic-bezier(0.4, 0, 0.2, 1);  /* most UI transitions */
  --ease-enter:    cubic-bezier(0, 0, 0.2, 1);     /* elements entering the screen */
  --ease-exit:     cubic-bezier(0.4, 0, 1, 1);     /* elements leaving the screen */
  --ease-spring:   cubic-bezier(0.34, 1.56, 0.64, 1); /* playful, elastic feel */
}
```

---

## Enforcement Rules

These rules apply to every HTML file produced after the design system is established:

1. **No hardcoded hex values** — all colors must reference a `--color-*` token
2. **No hardcoded pixel sizes for type or spacing** — use `--type-*` and `--space-*` tokens
3. **No magic numbers** — if a value isn't a token, it needs to become one or be documented as a one-off exception with a comment
4. **No `#000` or `#fff` shortcuts** — use `--color-text` and `--color-bg` equivalents
5. **Shadow from the scale** — no custom box-shadow values; use `--shadow-*` tokens

---

## Pre-Delivery Token Audit

Before any file is delivered, scan for violations:
- Raw hex values (`#[0-9a-fA-F]{3,6}`)
- Raw rgba/rgb without a token variable
- Hardcoded font sizes in px/rem not referencing `--type-*`
- Hardcoded spacing not referencing `--space-*`

Flag any violation in the delivery note. Do not silently ship non-compliant output.

---

## Design System Bootstrap Output Format

When generating `design-system.css` for a new project, follow this structure:

```css
/* ============================================
   Arrow Design System — [Project Name]
   Generated: [date]
   Philosophy: [chosen design direction]
   ============================================ */

:root {
  /* Color */
  ...

  /* Typography */
  ...

  /* Spacing */
  ...

  /* Radius */
  ...

  /* Elevation */
  ...

  /* Motion */
  ...
}

/* Semantic aliases — map tokens to intent */
:root {
  --color-cta:         var(--color-primary);
  --color-cta-hover:   var(--color-primary-hover);
  --color-danger:      var(--color-error);
  --color-page-bg:     var(--color-bg);
}
```

After outputting `design-system.css`, declare the design system verbally:
- Chosen philosophy and why it fits this brief
- Primary typeface pairing and intended voice
- Color palette with contrast ratios for primary text pairings
- Spacing grid baseline
- Any deviations from defaults and the reason

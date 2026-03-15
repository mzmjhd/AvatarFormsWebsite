# AvatarForms Design System

This guide defines how contributors should style pages so UI stays consistent without making design decisions from scratch.

## Core Principle

Use Tailwind/Flowbite normally. Keep design consistency by centralizing visual values (colors, radius, shadows, text tones) in `css/styles.css` tokens.

No page refactor is required. Existing classes can stay as they are.

## Theme and Tokens

Theme variables are in `css/styles.css` and automatically support light/dark mode through `.dark` on `<html>`.

Key tokens used across the site:

- `--bg`, `--text`
- `--bg-secondary`
- `--surface`, `--surface-border`
- `--accent`, `--accent-contrast`
- `--muted-text`
- `--text-soft`
- `--radius-base`
- `--shadow-sm`, `--shadow-md`, `--shadow-lg`

Do not hardcode new colors in page markup. If a new reusable style is needed, add a token + semantic class in `css/styles.css`.

Shadow consistency utilities are available globally:

- `.shadow-surface-sm`
- `.shadow-surface-md`
- `.shadow-surface-lg`

These can be used on existing Tailwind/Flowbite markup without refactoring to `af-*` classes.

## Approved Color Utility Classes

Use these class names consistently in page markup:

- `bg-neutral-primary`: page/default section background
- `bg-neutral-secondary`: alternate section background
- `bg-neutral-secondary-soft`: card/surface background
- `text-heading`: headings and strong labels
- `text-body`: standard paragraph/body copy
- `text-body-muted`: secondary/supporting text
- `text-body-soft`: subtle text
- `border-border-subtle`: default neutral border
- `text-fg-brand`: brand accent text/links

These classes automatically adapt in dark mode through `css/styles.css` tokens.

## Brand Gradient Utilities

Use these shared classes for gradient styling:

- `text-gradient-brand`: gradient text (titles/headings)
- `gradient-brand-bar`: gradient fill for divider/color bars

Semantic bar sizing helpers:

- Heights: `bar-thin`, `bar-md`, `bar-thick`
- Widths: `bar-short`, `bar-medium`, `bar-full`

Example:

```html
<h2 class="text-gradient-brand">Section title</h2>
<div class="gradient-brand-bar bar-md bar-full rounded-base"></div>
```

## What Developers Should Use by Default

1. Keep using normal Tailwind and Flowbite docs/components.
2. Prefer existing project theme utility names where available (`text-body`, `text-heading`, `bg-neutral-primary`, `rounded-base`).
3. Introduce new tokenized utilities only when the same visual pattern repeats across pages.

## Quick Decision Guide (When to use what)

Use this rule first:

- Layout and spacing: Tailwind utilities (`flex`, `grid`, `gap-*`, `p-*`, `m-*`)
- Visual consistency: project classes/tokens (`af-*`, color utilities, gradient utilities)

Use `af-*` classes when you want a reusable UI pattern, not one-off layout tweaks.

- `af-container`, `af-stack`, `af-grid-two`: page/section structure wrappers
- `af-card`, `af-callout`: repeated surface blocks
- `af-btn`, `af-btn-primary`, `af-btn-secondary`: buttons/actions
- `af-form-group`, `af-label`, `af-input`, `af-select`, `af-textarea`: forms
- `af-section-title`, `af-section-subtitle`: repeated heading/body styling

If you only need spacing/alignment changes, keep using Tailwind directly.

## What “accent” means

`accent` is the brand emphasis color. It is used for interactive or attention elements, not as a full-page background.

In this project, accent is typically applied through:

- links (`text-fg-brand`, `af-link`)
- primary actions (`af-btn-primary`)
- focus states (`--focus-ring` around inputs)
- callout highlights (left border in `af-callout`)

Avoid using accent as a large background fill for content sections unless intentionally creating a highlight strip.

## Optional `af-*` Helpers

`af-*` classes are optional shortcuts for repeated team patterns. They are not mandatory and should not force refactoring of existing pages.

## Optional Semantic Classes

### Layout

- `.af-container`: centered max-width content wrapper
- `.af-section`: standard section vertical spacing
- `.af-stack`: vertical stack with consistent gap
- `.af-grid-two`: responsive 1→2 column layout

### Typography

- `.af-section-title`: standard section heading
- `.af-section-subtitle`: secondary text

### Surface Components

- `.af-card`: bordered panel/card
- `.af-card-title`: card heading
- `.af-card-text`: card body text
- `.af-callout`: highlighted note/info block

### Actions and Links

- `.af-btn`: base button
- `.af-btn-primary`: primary button variant
- `.af-btn-secondary`: secondary button variant
- `.af-link`: inline semantic link style

### Form Controls

- `.af-form-group`: grouped label + control wrapper
- `.af-label`: label style
- `.af-input`: text input style
- `.af-select`: select style
- `.af-textarea`: textarea style

## Copy/Paste Patterns

### Section Block

```html
<section class="af-section">
  <div class="af-container af-stack">
    <h2 class="af-section-title">Section title</h2>
    <p class="af-section-subtitle">Supportive text for this section.</p>
  </div>
</section>
```

### Two Cards

```html
<div class="af-container af-grid-two">
  <article class="af-card">
    <h3 class="af-card-title">Card one</h3>
    <p class="af-card-text">Card content.</p>
  </article>
  <article class="af-card">
    <h3 class="af-card-title">Card two</h3>
    <p class="af-card-text">Card content.</p>
  </article>
</div>
```

### Form Row

```html
<form class="af-stack">
  <div class="af-form-group">
    <label for="name" class="af-label">Name</label>
    <input id="name" type="text" class="af-input" placeholder="Enter your name" />
  </div>
  <div class="af-form-group">
    <label for="message" class="af-label">Message</label>
    <textarea id="message" class="af-textarea" rows="4"></textarea>
  </div>
  <div class="flex gap-2">
    <button type="submit" class="af-btn af-btn-primary">Submit</button>
    <button type="button" class="af-btn af-btn-secondary">Cancel</button>
  </div>
</form>
```

## Typography

The project uses two fonts, locked to specific roles. Do not swap fonts or add new ones without updating this doc.

| Font | Role | Applied to |
|------|------|------------|
| **Inter** | Headings | `h1`–`h6` elements and `.type-heading` |
| **Poppins** | Body / Muted | `p` elements, `.type-body`, `.type-muted` |

### The 3 Text Roles

Every piece of text on the site should fall into one of these roles. Use the utility class when applying the style manually (e.g. on a `<span>` or `<div>`).

#### Role 1 — Heading (`.type-heading`)
- **Font**: Inter, weight 700
- **Line-height**: 1.2 (tight, for large display text)
- **Color**: `var(--text)` — adapts to dark mode automatically
- **Use for**: page titles, section headers, card titles, nav labels
- **Example**: `<h2 class="type-heading">Section title</h2>`

#### Role 2 — Body (`.type-body`)
- **Font**: Poppins, normal weight
- **Line-height**: 1.7 (comfortable reading)
- **Color**: `var(--text)` — full-contrast body copy
- **Use for**: paragraph text, descriptions, main content
- **Example**: `<p class="type-body">Paragraph content here.</p>` (the `p` baseline rule already applies this automatically)

#### Role 3 — Muted (`.type-muted`)
- **Font**: Poppins, normal weight
- **Line-height**: 1.7
- **Color**: `var(--muted-text)` — softer gray, adapts to dark mode
- **Use for**: bylines, captions, footer small-print, supporting text like "By Dex, Atticus..."
- **Example**: `<p class="type-muted">By Dex, Atticus, and the team</p>`

### Rules

- **Never** use ad-hoc Tailwind gray classes (`text-gray-400`, `text-gray-600`, etc.) for body text. Use `.type-muted` instead so dark mode works automatically.
- `h1`–`h6` elements already inherit the heading font/line-height from the baseline rule — you only need `.type-heading` on non-heading elements like `<span>` or `<div>`.
- `p` elements already inherit the body font/line-height — you only need `.type-body` on non-`p` elements.
- To make heading text gradient, add `text-gradient-brand` alongside `type-heading`.

### Quick Reference

```html
<!-- Heading -->
<h2 class="type-heading">Section Title</h2>

<!-- Body copy -->
<p>Normal paragraph — type-body is automatic on p elements.</p>

<!-- Muted / secondary text -->
<p class="type-muted">By Dex, Atticus and the team · March 2026</p>

<!-- Gradient heading -->
<h1 class="text-gradient-brand">Page Title</h1>
```

## Rules for Pull Requests

Before opening a PR, verify:

1. New pages start from the `afhtml` snippet.
2. Shared page layout uses component containers (`navbar`, `sidebar`, `breadcrumbs`).
3. Dark mode is visually correct.
4. No new one-off colors are introduced in markup.
5. Repeated visual patterns are centralized in `css/styles.css` tokens (optionally with `af-*` helper classes).

# Catnip Design System for Codex

This file explains how Codex should use the Catnip design system. The source tokens live in `/tokens/tokens.optimized.json`; CSS variables live in `/styles/tokens.css`. The Catnip icon library lives in `/assets/icons/raw`; icon helper classes live in `/styles/icons.css`.

## Product Feel

Catnip UI should feel clean, light, playful, social, content-first, and polished. It should not feel like a dark gaming interface, a generic AI SaaS dashboard, or a heavy cyberpunk tool.

## Mandatory Rules

- Always use existing CSS variables before adding new values.
- Do not hardcode colors, font sizes, radius, shadows, or spacing.
- Use semantic tokens first, such as `--color-background-page`, `--color-text-primary`, `--color-brand-primary`, and `--color-border-subtle`.
- Use raw neutral or accent tokens only when semantic tokens are not enough.
- Reuse existing button, tab, card, input, and feed patterns before creating new styles.
- Use the Catnip icon library before drawing custom icons or using text glyphs as icons.
- A screen should usually have one clear primary CTA.

## Color Usage

- Page background: `--color-background-page` or `--color-background-base`.
- Card/sheet surface: `--color-surface-primary`.
- Primary text: `--color-text-primary`.
- Secondary text: `--color-text-secondary`.
- Borders/dividers: `--color-border-subtle` or `--color-border-default`.
- Primary CTA: `--color-brand-primary`.
- Pressed CTA: `--color-brand-pressed`.
- Disabled CTA: `--color-brand-disabled`.

## Typography Usage

- Display and headings use Rubik.
- Body, labels, buttons, tabs, and functional UI text use Inter.
- Do not invent new type sizes. Use the typography variables from `tokens.css`.
- For dense mobile UI, prefer body medium or label small styles.

## Radius Usage

- Small controls: `--radius-xs`.
- Buttons and tabs: `--radius-full` or `--radius-s`.
- Cards and sheets: `--radius-l`.
- Large playful containers: `--radius-xl`.

## Icon Usage

- Use icons from `/assets/icons/raw` for Catnip UI actions, navigation, media tools, profile surfaces, and social/product controls.
- Icons are SVG assets exported on a 48x48 viewBox and normalized to inherit `currentColor`.
- Use `/styles/icons.css` helper classes when a plain token-backed icon size or color state is enough.
- Set icon color through token-backed CSS, such as `color: var(--color-text-primary)`, `color: var(--color-text-secondary)`, `color: var(--color-brand-deep)`, or `color: var(--color-text-inverse)`.
- Set icon size with existing size tokens only, such as `--size-5`, `--size-6`, `--size-7`, `--size-8`, or component-specific token dimensions.
- Do not hardcode SVG fill, stroke, width, height, or inline color values in product UI.
- Prefer inline SVG or a component wrapper when an icon needs to inherit token color. If using an SVG as an image source, only use it where the default asset color is acceptable.
- Use filled icon variants for active states, selected navigation items, primary creation actions, and high-emphasis media controls.
- Use outline/default variants for inactive navigation, secondary actions, toolbars, and low-emphasis controls.
- Brand/social logo icons may be used only where the actual platform or brand is being referenced.

## Component Rules

### Buttons

- Primary buttons use brand primary background and primary text.
- Primary height is 48px. Secondary height is 44px.
- Buttons should feel rounded and tappable.
- Disabled buttons should use the disabled brand token or opacity, not a new color.
- Icon-only buttons should use Catnip icons, token sizes, and accessible labels.

### Tabs

- Tabs should be lightweight.
- Active tab uses a subtle background and primary text.
- Inactive tab uses secondary text.
- Avoid heavy outlines or strong shadows.

### Cards

- Cards use white or subtle surfaces.
- Use soft borders and limited shadows.
- Prefer spacing and hierarchy over decoration.

## Visual QA Checklist

Before finishing any UI task, check:

- No hardcoded visual values.
- Colors come from tokens.
- Font sizes come from typography tokens.
- Radius comes from radius tokens.
- The UI feels clean, light, social, playful, and content-first.
- The result is consistent with existing Catnip components.

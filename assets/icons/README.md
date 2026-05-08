# Catnip Icon Library

This folder contains the Catnip SVG icon library.

- Source: `/assets/icons/raw`
- Helper CSS: `/styles/icons.css`
- Count: 121 SVG icons
- Base grid: 48x48 viewBox
- Color behavior: icons are normalized to `currentColor`

## Usage

Use these icons before introducing another icon set or drawing custom UI glyphs. In product UI, set icon color with Catnip tokens through CSS:

```css
.icon {
  width: var(--size-6);
  height: var(--size-6);
  color: var(--color-text-primary);
}
```

Use semantic color tokens first. Use accent tokens only when the icon is decorative, brand-specific, or needs stronger semantic emphasis.

For common cases, use `catnip-icon`, `catnip-icon--small`, `catnip-icon--large`, `catnip-icon--secondary`, `catnip-icon--inverse`, or `catnip-icon--brand` from `/styles/icons.css`.

## Rules

- Do not hardcode icon colors, sizes, radius, or spacing in UI code.
- Do not edit SVG fills or strokes to fixed colors.
- Prefer inline SVG or an icon component wrapper when icons need to inherit token color.
- Use filled variants for active, selected, or high-emphasis states.
- Use outline/default variants for inactive, secondary, or toolbar states.
- Keep original filenames for imported assets; use a wrapper alias if product code needs friendlier names.

## Naming Notes

The current import preserves the source filenames, including existing casing and spaces. New icon additions should avoid spaces and use the existing descriptive naming pattern.

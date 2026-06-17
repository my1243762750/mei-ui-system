# Mei UI System

Mei UI System is a shared UI standard for AI-assisted projects.

Its purpose is to make different AI agents and different projects produce the same visual style: blue-purple color system, consistent tokens, unified component rules, layout density, and Mei brand assets.

![Mei UI System preview](assets/preview/mei-ui-preview.svg)

## AI Quick Start

AI and other automated systems must use `ai.md` as the execution entry point.

1. Read `ai.md`.
2. Read token files in the order defined by `ai.md`.
3. Read `patterns.md` to decide product type, density, and layout.
4. Read `components.md` to choose component composition rules.
5. Read `brand.md` before using or creating any logo / app icon / favicon.
6. Generate UI using token paths only; do not hardcode colors, spacing, radius, shadows, or typography.

## Brand Rule

If the target project has no existing logo / app icon / brand mark, use the Mei default logo assets in `assets/logo/`.

Do not redesign, recolor, stretch, or replace the Mei logo for each project.

## Directory

```
tokens/       → JSON design tokens (source of truth)
assets/logo/  → Unified Mei logo assets (SVG source + PNG/favicon exports)
ai.md         → AI execution rules
patterns.md   → Layout patterns by product type
components.md → Component composition rules
brand.md      → Logo and brand usage rules
```

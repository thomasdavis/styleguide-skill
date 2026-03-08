# Styleguide Skill

A Claude Code plugin that generates comprehensive, project-specific style guides and design systems. Inspired by the full depth of Material Design 3 — but reimagined for your unique brand, technology stack, and goals.

## What It Does

When you run `/styleguide:styleguide` (or `/styleguide:styleguide My Project Name`), Claude becomes a design systems architect and generates a complete style guide covering **17 design domains** and **30+ components**, tailored to your project.

## Coverage

| Domain | What's Defined |
|--------|---------------|
| **Design Tokens** | Reference/system/component token architecture, naming conventions, multi-platform delivery |
| **Color System** | Dynamic color from seed, 6 tonal palettes, 40+ color roles, custom colors, fixed colors, dark theme |
| **Typography** | 15-role type scale, font selection, responsive type, content line-length guidelines |
| **Shape** | 7-level shape scale, rounded/cut corners, shape morphing, size-shape relationships |
| **Elevation** | 6 shadow levels, key+ambient shadows, tonal elevation (surface tint), interaction elevation changes |
| **Motion** | 7 easing curves, 16 duration tokens, 5 transition patterns, spring animations, stagger choreography, reduced motion |
| **Iconography** | System icon grid, 4 variable axes (weight/grade/optical-size/fill), product icon guidelines |
| **Layout & Spacing** | Column grids, 14-step spacing scale, 5 window size classes, 4 canonical layouts, pane behavior, touch targets |
| **Interaction States** | 6 state layers with opacities, ripple effect, focus indicators, selection/validation states |
| **Accessibility** | WCAG contrast, dynamic type, touch targets, ARIA semantics, motion sensitivity, screen reader support |
| **Components** | Buttons (6 types), icon buttons (4 types), FAB (4 sizes), segmented buttons, badges, progress indicators, snackbar, tooltips, bottom sheets, cards (3 types), carousel (4 types), dialogs, dividers, lists, side sheets, bottom app bar, navigation bar/drawer/rail, tabs, top app bar (4 types), search, checkbox, chips (4 types), date pickers (4 types), menus, radio buttons, sliders, switch, time pickers, text fields (2 types) |
| **Adaptive Design** | Component adaptation rules across breakpoints, responsive patterns, foldable/multi-screen |
| **Theming** | Theme hierarchy (baseline/brand/product/component), color/type/shape theming, dark/light mode, high contrast |
| **Content & Writing** | Voice & tone, UI text conventions, i18n/RTL support |
| **Data Visualization** | Chart color usage, typography, 6 chart types, interaction patterns |
| **Illustration & Imagery** | Style guide, photography treatment, image containers, skeleton loading |
| **Platform Guidance** | Web (CSS), Android (Compose/XML), iOS (SwiftUI/UIKit), Cross-platform (Flutter/RN) |

## Installation

### From a marketplace (if published)

```
/plugin install styleguide@marketplace-name
```

### Local testing

```bash
claude --plugin-dir /path/to/styleguide-skill
```

### Manual install

Copy the `skills/styleguide/` directory to `~/.claude/skills/styleguide/` for personal use, or `.claude/skills/styleguide/` in any project.

## Usage

```
/styleguide:styleguide
```

Or with context:

```
/styleguide:styleguide My SaaS Dashboard - React + Tailwind - professional and minimal
```

Claude will ask for any missing details (brand personality, colors, fonts, platforms) and then generate the full style guide with:

- Design token files (JSON/CSS/code)
- Complete light + dark color schemes with hex values
- Full typography scale
- Component spec sheets
- Platform-appropriate code snippets
- Do's and don'ts

## Philosophy

This skill doesn't produce generic Material Design output. It uses M3 as a **structural completeness checklist** — ensuring no design concept is missed — then reimagines every decision for your specific project. The result is a style guide that feels native to your brand, not a Material skin.

## License

MIT

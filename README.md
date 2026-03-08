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

### From this marketplace

```
/plugin marketplace add thomasdavis/styleguide-skill
/plugin install styleguide@thomasdavis-plugins
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

## Example Use Cases

### 1. New startup needs a design system from scratch

```
/styleguide:styleguide Pulse - a health & fitness SaaS app - React + Tailwind - energetic and modern
```

You're building a new product and don't have a design system yet. The skill generates your entire foundation — a seed color (e.g., vibrant green) expanded into full light/dark tonal palettes, a type scale using Inter for body and a bold display font, an 8px spacing grid, every component specced out with your brand tokens, and CSS custom properties ready to drop into your Tailwind config. Instead of spending weeks deciding on your color roles, elevation levels, and button variants, you get a coherent system in minutes that you can iterate on.

### 2. Bringing consistency to an existing codebase

```
/styleguide:styleguide
```

> Brand: "Meridian" - professional, trustworthy, navy blue (#1a365d) primary
> Stack: Vue 3 + SCSS
> Platform: Web only

Your app has grown organically — 14 shades of grey, inconsistent spacing, buttons that look different on every page. The skill audits what a complete system should look like and generates a token file mapping your existing navy blue through a full tonal palette, defines the 6 elevation levels your shadows should follow, and specs out every component with consistent shape/state/spacing tokens. You get a migration path from chaos to system.

### 3. Building a cross-platform component library

```
/styleguide:styleguide Kite - a fintech banking app - Flutter - clean and minimal with sharp edges
```

You need components that work on both iOS and Android. The skill generates Dart theme data with your color scheme, a type scale using system fonts per platform, a shape system using cut corners (matching "sharp edges"), and component specs for every element from text fields to bottom sheets — all with Flutter-specific guidance on adaptive behavior (Cupertino on iOS, Material on Android) and platform-appropriate navigation patterns.

### 4. White-label product needing theme infrastructure

```
/styleguide:styleguide CloudDesk - a white-label helpdesk platform - React + CSS Modules
```

Your product is resold under different brands. The skill generates a complete token architecture with the three-tier system (reference → system → component tokens) designed for theming. Each client gets their own seed color that cascades through all 40+ color roles automatically. The theme structure section defines exactly how brand overrides layer on top of your baseline, so spinning up a new client theme means changing one seed color and a font stack.

### 5. Mobile app redesign with accessibility focus

```
/styleguide:styleguide Relay - a messaging app for the deaf community - SwiftUI - warm and accessible
```

Accessibility isn't an afterthought — it's the product. The skill generates a color system that exceeds AAA contrast ratios (7:1), ensures all touch targets are 48dp+, defines comprehensive VoiceOver/ARIA semantics for every component, specs out `prefers-reduced-motion` behavior, and provides Dynamic Type scaling rules. Every component spec includes its accessibility requirements alongside the visual design.

## Philosophy

This skill doesn't produce generic Material Design output. It uses M3 as a **structural completeness checklist** — ensuring no design concept is missed — then reimagines every decision for your specific project. The result is a style guide that feels native to your brand, not a Material skin.

## License

MIT

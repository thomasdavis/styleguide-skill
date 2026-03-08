---
name: styleguide
description: >
  Generate a comprehensive style guide and design system for any project.
  Use when the user asks to create a style guide, design system, component library,
  design tokens, or UI guidelines. Covers color systems, typography, shape, elevation,
  motion, iconography, layout, interaction states, accessibility, 30+ components,
  adaptive design, theming, content guidelines, data visualization, and platform-specific guidance.
  Inspired by Material Design 3 but reimagined for the user's unique brand and stack.
allowed-tools: Read Grep Glob Edit Write Bash
argument-hint: "[project-name or description]"
---

You are a design systems architect. When the user asks you to create a style guide, design system, or component library for their project, generate a comprehensive, project-specific style guide inspired by the full depth of Material Design 3 principles — but reimagined and adapted for the user's unique brand, technology stack, and goals.

Do NOT copy Material Design. Use it as a structural blueprint to ensure completeness, then tailor every decision to the project's identity.

If the user provided arguments via $ARGUMENTS, use those as the project context. Otherwise, ask the user for:
1. Project name and description
2. Brand personality (e.g., playful, professional, minimal, bold)
3. Technology stack (e.g., React, Flutter, SwiftUI, vanilla CSS)
4. Target platforms (web, mobile, desktop, cross-platform)
5. Any existing brand colors, fonts, or logos

Then produce the style guide covering ALL sections below. Write the output as actual files in the project (e.g., `docs/style-guide/` or a single comprehensive document), using the user's technology stack for code examples.

---

## 1. DESIGN TOKENS

Design tokens are the atomic values that drive the entire system. Define all tokens as platform-agnostic key-value pairs that can be exported to CSS custom properties, JSON, XML, Swift constants, Dart constants, etc.

### 1.1 Token Architecture
- **Reference tokens (global):** Raw values with no semantic meaning (e.g., `blue-500: #2196F3`, `space-4: 16px`). These form the full palette of available values.
- **System tokens (alias):** Semantic mappings that reference global tokens (e.g., `color-primary: {blue-500}`, `spacing-md: {space-4}`). These encode design decisions.
- **Component tokens:** Per-component overrides that reference system tokens (e.g., `button-container-color: {color-primary}`). These allow fine-grained component customization.

### 1.2 Token Categories
Define tokens for every category:
- Color
- Typography
- Spacing
- Shape (border radius)
- Elevation (shadow)
- Motion (duration, easing)
- Opacity
- Z-index / layer ordering
- Sizing (icon sizes, touch targets, component dimensions)
- Breakpoints

### 1.3 Token Naming Convention
Establish a consistent naming pattern:
```
{category}-{element}-{modifier}-{state}-{scale}
```
Example: `color-surface-container-hover-high`

### 1.4 Token Delivery
Specify how tokens are consumed per platform:
- CSS custom properties (`--color-primary`)
- SCSS variables (`$color-primary`)
- JSON / JS objects
- iOS/Swift constants
- Android XML resources
- Flutter/Dart theme data

---

## 2. COLOR SYSTEM

### 2.1 Dynamic Color
- Define a system where the entire color scheme can be derived from a single source/seed color.
- Describe the algorithm: source color -> tonal palettes -> color roles.
- Support user-generated or content-derived color (e.g., extracting a key color from a wallpaper, album art, or uploaded image).

### 2.2 Tonal Palettes
Generate tonal palettes with defined luminance stops. Each palette is a single hue with tonal variations:
- **Primary palette:** The brand's main color across tones (0, 4, 6, 10, 12, 17, 20, 22, 24, 25, 30, 35, 40, 50, 60, 70, 80, 87, 90, 92, 94, 95, 96, 98, 100)
- **Secondary palette:** A complementary hue, lower chroma
- **Tertiary palette:** An analogous or contrasting accent hue
- **Error palette:** Semantic red-based tones for errors
- **Neutral palette:** Very low chroma tones for surfaces and backgrounds
- **Neutral-variant palette:** Slightly chromatic neutrals for outlines and secondary surfaces

### 2.3 Color Scheme / Color Roles
Map tonal palette values to semantic roles. Define for BOTH light and dark schemes:

**Primary group:**
- `primary` — Main brand color for key components (FABs, prominent buttons, active states)
- `on-primary` — Content color (text/icons) on top of primary
- `primary-container` — Standout fill for related components
- `on-primary-container` — Content on primary-container

**Secondary group:**
- `secondary` — Accent for less prominent components (filter chips, subtle accents)
- `on-secondary`
- `secondary-container`
- `on-secondary-container`

**Tertiary group:**
- `tertiary` — Contrasting accent for balance (complementary to primary/secondary)
- `on-tertiary`
- `tertiary-container`
- `on-tertiary-container`

**Error group:**
- `error` — Indicates errors and urgent states
- `on-error`
- `error-container`
- `on-error-container`

**Surface group:**
- `surface` — Default background
- `on-surface` — Default text/icon color
- `surface-variant` — Alternate surface
- `on-surface-variant` — Subdued content color
- `surface-container-lowest` — Lowest emphasis container
- `surface-container-low`
- `surface-container` — Default container
- `surface-container-high`
- `surface-container-highest` — Highest emphasis container
- `surface-dim` — Dimmed surface
- `surface-bright` — Bright surface
- `surface-tint` — Tint overlay color (used for elevation tinting)
- `inverse-surface` — Contrasting surface (e.g., for snackbars)
- `inverse-on-surface`
- `inverse-primary`

**Outline group:**
- `outline` — Default border/divider color
- `outline-variant` — Subtle borders/dividers

**Background (legacy):**
- `background`
- `on-background`

**Scrim:**
- `scrim` — Overlay behind modals/dialogs

**Shadow:**
- `shadow` — Color for drop shadows

### 2.4 Custom Colors
- Allow users to define additional custom color groups that integrate with the tonal system.
- Each custom color gets its own tonal palette and four roles: `color`, `on-color`, `color-container`, `on-color-container`.
- Custom colors should harmonize with the primary color to maintain visual cohesion.

### 2.5 Fixed & Accent Colors
- Define fixed colors that do NOT change between light and dark modes (for components that maintain a consistent look).
- `primary-fixed`, `primary-fixed-dim`, `on-primary-fixed`, `on-primary-fixed-variant` (and same for secondary, tertiary).

### 2.6 Color Accessibility
- All foreground/background pairings must meet WCAG 2.1 contrast ratios (4.5:1 for normal text, 3:1 for large text and UI components).
- Define how the system guarantees contrast (tonal distance between on-color and color should be at least 40-50 tonal steps).
- Provide guidance on color-blind safe palettes and never relying on color alone.

### 2.7 Dark Theme
- Describe the specific mappings: dark schemes use lighter tones for surfaces and swap primary/container emphasis.
- Desaturate primary colors slightly in dark mode to reduce eye strain.
- Use tonal elevation (surface tint) instead of shadows for elevated surfaces in dark mode.

---

## 3. TYPOGRAPHY

### 3.1 Type Scale
Define a complete type scale with these roles:

| Role | Usage |
|------|-------|
| `display-large` | Hero headlines, largest text on screen |
| `display-medium` | Major section headlines |
| `display-small` | Smaller display text |
| `headline-large` | Page-level headlines |
| `headline-medium` | Section headlines |
| `headline-small` | Sub-section headlines |
| `title-large` | Top app bar titles, card titles |
| `title-medium` | Component headers, list subheaders |
| `title-small` | Tabs, small section titles |
| `body-large` | Primary body text |
| `body-medium` | Default body text, descriptions |
| `body-small` | Captions, supporting text |
| `label-large` | Buttons, prominent labels |
| `label-medium` | Navigation labels, chips |
| `label-small` | Badges, timestamps, metadata |

### 3.2 Token Properties Per Scale Entry
For each type scale entry, define:
- **Font family** (brand vs. plain/system font)
- **Font weight** (100-900)
- **Font size** (px/sp/rem)
- **Line height** (absolute or multiplier)
- **Letter spacing** (em or px)
- **Text transform** (uppercase, capitalize, none)
- **Text decoration** (underline, none)
- **Paragraph spacing** (for multi-paragraph contexts)

### 3.3 Font Selection Guidelines
- **Brand font:** Used for display, headline, and title roles. Expresses personality.
- **Plain font:** Used for body and label roles. Optimized for legibility.
- Provide fallback font stacks for web.
- Require variable fonts where possible for performance and flexibility.
- Define loading strategy: `font-display: swap`, preload critical fonts.

### 3.4 Responsive Typography
- Define how type scale adjusts across breakpoints (compact, medium, expanded, large, extra-large).
- Use fluid typography (CSS `clamp()`) or stepped breakpoint scales.
- Set minimum and maximum font sizes.

### 3.5 Content Guidelines
- Line length: 45-75 characters per line for body text.
- Paragraph spacing conventions.
- Heading hierarchy rules (never skip heading levels).
- Text alignment conventions (left-align body text in LTR, avoid justified text on screens).

---

## 4. SHAPE

### 4.1 Shape Scale
Define a shape scale with named corner radius values:

| Token | Value | Usage |
|-------|-------|-------|
| `shape-none` | 0px | No rounding (sharp corners) |
| `shape-extra-small` | 4px | Small chips, badges |
| `shape-small` | 8px | Buttons, text fields, small cards |
| `shape-medium` | 12px | Cards, dialogs |
| `shape-large` | 16px | Large cards, navigation drawers |
| `shape-extra-large` | 28px | FABs, bottom sheets (top corners) |
| `shape-full` | 50% / 9999px | Pills, circular elements |

### 4.2 Corner Styles
- **Rounded** (default): Standard border-radius
- **Cut** (chamfered): 45-degree angled corners for a more geometric look
- Define how corner style is applied globally and per-component.

### 4.3 Shape and Size Relationship
- Larger components generally use larger corner radii.
- Shapes that fill the screen width (full-width cards, banners) should use 0 corner radius on touching edges.
- Inner corners should have radius = outer radius - padding to maintain concentric curves.

### 4.4 Shape Morphing
- Define how shapes transition during state changes (e.g., a circle morphing to a rounded rectangle on expand).
- Specify spring/ease parameters for shape animation.

---

## 5. ELEVATION

### 5.1 Elevation Levels
Define a 6-level elevation system:

| Level | Shadow | Usage |
|-------|--------|-------|
| `elevation-0` | None | Flat surfaces, backgrounds |
| `elevation-1` | Subtle | Cards, buttons at rest, app bars |
| `elevation-2` | Low | Raised buttons, snackbars |
| `elevation-3` | Medium | FABs, navigation drawers |
| `elevation-4` | High | Menus, sub-menus |
| `elevation-5` | Highest | Modals, dialogs, full-screen dialogs |

### 5.2 Shadow Definition
For each level define:
- **Key shadow:** Directional shadow (simulates light from above) -- x, y, blur, spread, color/opacity
- **Ambient shadow:** Omnidirectional shadow -- x, y, blur, spread, color/opacity
- Combine key + ambient for the composite shadow.

### 5.3 Tonal Elevation (Surface Tint)
- In dark mode (and optionally light mode), express elevation through surface tint overlay instead of/in addition to shadow.
- Higher elevation = more primary tint applied to the surface color.
- Map each elevation level to a tint opacity:
  - Level 0: 0%
  - Level 1: 5%
  - Level 2: 8%
  - Level 3: 11%
  - Level 4: 12%
  - Level 5: 14%

### 5.4 Elevation Interactions
- Hovered: +1 elevation level from resting state
- Pressed: Returns to resting elevation (no elevation increase on press)
- Dragged: Highest elevation (level 4-5)
- Disabled: Level 0

---

## 6. MOTION & ANIMATION

### 6.1 Easing Curves
Define named easing functions:

| Token | Curve | Usage |
|-------|-------|-------|
| `easing-standard` | cubic-bezier(0.2, 0.0, 0, 1.0) | Default transitions, moving on-screen elements |
| `easing-standard-decelerate` | cubic-bezier(0, 0, 0, 1) | Elements entering the screen |
| `easing-standard-accelerate` | cubic-bezier(0.3, 0, 1, 1) | Elements leaving the screen |
| `easing-emphasized` | Two-phase curve or spring | High-emphasis transitions (expanding, shared-element) |
| `easing-emphasized-decelerate` | cubic-bezier(0.05, 0.7, 0.1, 1.0) | Incoming emphasized elements |
| `easing-emphasized-accelerate` | cubic-bezier(0.3, 0.0, 0.8, 0.15) | Outgoing emphasized elements |
| `easing-linear` | linear | Color fades, opacity changes |

### 6.2 Duration Scale
Define durations for different transition complexities:

| Token | Duration | Usage |
|-------|----------|-------|
| `duration-short-1` | 50ms | Micro-interactions (ripple start, icon switch) |
| `duration-short-2` | 100ms | Simple state changes (color, opacity) |
| `duration-short-3` | 150ms | Small element transitions |
| `duration-short-4` | 200ms | Icon/button animations |
| `duration-medium-1` | 250ms | Standard transitions |
| `duration-medium-2` | 300ms | Component expand/collapse |
| `duration-medium-3` | 350ms | Navigation transitions |
| `duration-medium-4` | 400ms | Complex layout changes |
| `duration-long-1` | 450ms | Full-screen transitions |
| `duration-long-2` | 500ms | Shared-element transitions |
| `duration-long-3` | 550ms | Complex multi-element choreography |
| `duration-long-4` | 600ms | Largest transitions |
| `duration-extra-long-1` | 700ms | Cross-fade between pages |
| `duration-extra-long-2` | 800ms | Staggered enter animations |
| `duration-extra-long-3` | 900ms | Complex sequence animations |
| `duration-extra-long-4` | 1000ms | Maximum non-loading animation |

### 6.3 Transition Patterns
Define standard patterns for:
- **Container transforms:** One element transforms into another (card -> detail page). The container clips content, crossfades inner content, and morphs shape/size.
- **Shared axis transitions:** Sequential navigation along a spatial axis (forward/back, up/down). Outgoing element fades and translates; incoming element fades in and translates from opposite direction.
- **Fade through:** Non-sequentially related transitions. Outgoing scales down + fades out; incoming scales up + fades in.
- **Fade:** Simple opacity transition for elements entering/exiting without positional change.
- **Shared element transitions:** An element persists across two different views, animating its position, size, and shape from source to destination.

### 6.4 Spring Animations
For gesture-driven and emphasized animations:
- Define spring parameters: `stiffness`, `damping`, `mass`
- Provide named presets: `spring-gentle`, `spring-responsive`, `spring-bouncy`, `spring-snappy`

### 6.5 Stagger & Choreography
- When multiple elements animate together, stagger their start times (30-50ms offset each).
- Elements closer to the trigger point animate first.
- Establish enter order: background -> container -> content (top to bottom, leading to trailing).
- Exit order: reverse of enter.

### 6.6 Reduced Motion
- Respect `prefers-reduced-motion` media query.
- Provide a reduced-motion variant: replace motion with instant cuts or simple opacity fades.
- Never disable functional animations (e.g., scroll position indicators) -- only decorative ones.

---

## 7. ICONOGRAPHY

### 7.1 System Icons
- Define icon grid size: 24x24dp (with 20x20 live area, 2dp padding).
- Define available styles: **outlined**, **rounded**, **sharp**, **filled**, **two-tone**.
- Establish a default style for the project.
- Icon stroke weight: 1.5-2dp.
- Optical sizing: icons should have weight/grade variants for different sizes (20, 24, 40, 48).

### 7.2 Icon Tokens
- `icon-size-small`: 18-20dp
- `icon-size-medium`: 24dp (default)
- `icon-size-large`: 36-40dp
- `icon-size-extra-large`: 48dp
- `icon-color-primary`: inherits from `on-surface` or `primary`
- `icon-color-disabled`: `on-surface` at 38% opacity

### 7.3 Variable Icons
- Support icons with adjustable: **weight** (100-700), **grade** (-25 to 200), **optical size** (20-48), **fill** (0 or 1).
- Grade: fine-tune icon weight without changing size. Use negative grade for dark-on-light to prevent overly bold appearance. Use positive grade to increase emphasis.

### 7.4 Product Icons / App Icons
- Define grid, keyline shapes (circle, square, portrait rect, landscape rect).
- Define finish/material metaphor (flat, dimensional, etc.).
- Brand icon sizing for different contexts (launcher, notification, settings).

---

## 8. LAYOUT & SPACING

### 8.1 Layout Grid
- Define column grid for each window size class:
  - **Compact** (0-599dp): 4 columns, 16dp margins, 8dp gutters
  - **Medium** (600-839dp): 8 columns, 24dp margins, 16dp gutters (or 12 columns)
  - **Expanded** (840-1199dp): 12 columns, 24dp margins, 24dp gutters
  - **Large** (1200-1599dp): 12 columns, 24dp margins, 24dp gutters
  - **Extra-large** (1600dp+): 12 columns, 24dp margins, 24dp gutters (max content width)

### 8.2 Spacing Scale
Define a 4px/8px base grid spacing scale:
- `space-0`: 0
- `space-1`: 4px
- `space-2`: 8px
- `space-3`: 12px
- `space-4`: 16px
- `space-5`: 20px
- `space-6`: 24px
- `space-7`: 28px
- `space-8`: 32px
- `space-10`: 40px
- `space-12`: 48px
- `space-16`: 64px
- `space-20`: 80px
- `space-24`: 96px

### 8.3 Window Size Classes
Define breakpoint-driven behavior classes:
- **Compact:** Phone portrait. Single-pane layouts. Bottom navigation. Full-width components.
- **Medium:** Tablet portrait, foldable inner. May use rail navigation. Flexible pane widths.
- **Expanded:** Tablet landscape, desktop. Two-pane layouts. Navigation rail or permanent drawer. List-detail views.
- **Large:** Desktop. Multi-pane layouts. Permanent navigation drawer.
- **Extra-large:** Large desktop/TV. Max content width, centered layouts.

### 8.4 Canonical Layouts
Define standard layout patterns that adapt across breakpoints:
- **List-detail:** List pane + detail pane. Compact: full-screen list, push to detail. Expanded: side-by-side.
- **Feed:** Scrolling content feed. Compact: single column. Expanded: grid or multi-column.
- **Supporting pane:** Main content + supporting panel. Compact: stacked or bottom sheet. Expanded: side pane.
- **Hero/highlight:** Featured content with supporting items.

### 8.5 Pane Behavior
- **Fixed panes:** Always visible at a given breakpoint.
- **Flexible panes:** Resize proportionally.
- **Collapsible panes:** Collapse to icon/rail below a threshold.
- Define pane min/max widths and transition behavior.

### 8.6 Content Positioning
- Define safe areas and insets (status bar, navigation bar, notch/cutout).
- Scrolling behavior: content scrolls under app bars, FABs float.
- Define sticky/fixed positioning rules for navigation, toolbars.

### 8.7 Touch Targets
- Minimum touch target: 48x48dp.
- Visual size can be smaller, but touch area must meet minimum.
- Spacing between targets: at least 8dp.

---

## 9. INTERACTION STATES

### 9.1 State Layers
Define how interaction states are visually communicated using overlay layers:

| State | Overlay Opacity | Additional Effects |
|-------|----------------|-------------------|
| **Enabled** | 0% | Default appearance |
| **Disabled** | Content at 38% opacity, container at 12% opacity | No interaction allowed |
| **Hovered** | 8% of content color | Cursor changes, elevation may increase |
| **Focused** | 10% of content color | Focus indicator (ring or highlight) |
| **Pressed** | 10% of content color | Ripple effect, elevation may decrease |
| **Dragged** | 16% of content color | Highest elevation, content lifts |

### 9.2 Ripple Effect
- On press: radial ink ripple emanating from touch point.
- Ripple color: the `on-` color of the component's container at pressed opacity.
- Bounded ripple: clips to container shape.
- Unbounded ripple: extends beyond icon bounds (for icon buttons).

### 9.3 Focus Indicators
- Define visible keyboard focus style (focus ring, outline offset).
- Color: use `secondary` or high-contrast outline.
- Width: 2-3px.
- Offset: 2-3px from component edge.
- Shape follows component shape.

### 9.4 Selection States
- **Selected:** Active/checked state (checkboxes, chips, navigation items). Uses `primary` or `secondary-container` fill.
- **Activated:** Currently viewed/focused in a group (nav items). Distinguished from selected.
- **Toggled on/off:** Binary state (switches, toggles).

### 9.5 Error & Validation States
- Error state: `error` color for borders, supporting text, and icons.
- Warning state: custom color or `tertiary`.
- Success state: custom color.
- Display error text below component, replace helper text.

---

## 10. ACCESSIBILITY

### 10.1 Color & Contrast
- Minimum contrast ratios: 4.5:1 (AA normal text), 3:1 (AA large text, UI components).
- Enhanced target: 7:1 (AAA) for critical text.
- Never use color as the only means of conveying information.

### 10.2 Typography Accessibility
- Minimum body text size: 14sp/px.
- Support dynamic type / user font scaling (up to 200%).
- Adequate line height (1.4-1.6x for body text).
- Avoid ALL CAPS for sentences (bad for screen readers and readability).

### 10.3 Touch & Pointer
- Touch targets: 48x48dp minimum.
- Adequate spacing between interactive elements.
- Support both touch and pointer input.
- All interactions achievable via keyboard.

### 10.4 Semantic Structure
- Use proper heading hierarchy (h1-h6).
- ARIA roles, labels, and landmarks.
- Form inputs must have visible labels (not just placeholders).
- Group related controls (fieldset/legend, role=group).

### 10.5 Motion Accessibility
- Respect `prefers-reduced-motion`.
- No auto-playing animations that can't be paused.
- No flashing content (3 flashes per second threshold).

### 10.6 Screen Reader
- Meaningful alt text for images.
- Announce dynamic content changes (ARIA live regions).
- Logical reading order and focus order.
- Skip navigation links.

---

## 11. COMPONENTS

For every component below, define:
- **Anatomy:** Named sub-elements (container, content, icon, label, supporting text, etc.)
- **Design tokens:** All customizable tokens (colors, shapes, typography, spacing, elevation)
- **States:** How each interaction state appears
- **Variants:** All variations (e.g., filled vs outlined vs text button)
- **Sizes:** If the component has multiple size options
- **Responsive behavior:** How it adapts across breakpoints
- **Accessibility:** Required ARIA roles, keyboard interaction, focus management
- **Do's and don'ts:** Usage guidelines

### 11.1 Actions

#### Buttons
- **Common button (filled):** High emphasis. Solid container with `primary` fill. Used for primary actions.
- **Outlined button:** Medium emphasis. Transparent with `outline` border. Used for secondary actions.
- **Text button:** Low emphasis. No container. Used for tertiary actions, dialogs.
- **Elevated button:** Medium emphasis. Surface-tinted fill with shadow. For actions needing separation from patterned backgrounds.
- **Tonal button (filled tonal):** Medium emphasis. `secondary-container` fill. Lower emphasis than filled, higher than outlined.
- Anatomy: container, label text, icon (optional, leading or trailing).
- States: enabled, disabled, hovered, focused, pressed.
- Sizes: default, small (if applicable).

#### Icon Buttons
- **Standard:** No container. Icon only.
- **Filled:** Solid container behind icon.
- **Filled tonal:** Tonal container.
- **Outlined:** Outline border, no fill.
- Toggle variants for each (selected/unselected).
- Minimum size: 48dp touch target, 40dp visual.

#### Floating Action Button (FAB)
- **Small FAB:** 40dp. For compact spaces.
- **FAB:** 56dp. Default. Primary action for the screen.
- **Large FAB:** 96dp. Most prominent actions.
- **Extended FAB:** Includes text label + optional icon. Wider format.
- Container color: `primary-container` (default), `surface` (surface FAB), `secondary-container`, `tertiary-container`.
- Shape: `shape-large` (default), `shape-extra-large` (large FAB).
- Position: bottom-end of screen, 16dp from edges. Moves on scroll.

#### Segmented Buttons
- A group of related toggle buttons (2-5 segments).
- Single-select or multi-select.
- Anatomy: container, segment (with icon, label, selected icon/checkmark).
- Outlined container with dividers between segments.

### 11.2 Communication

#### Badges
- **Small badge:** Dot indicator (6dp), no text. Indicates presence of new content.
- **Large badge:** Pill with number (16dp height). Shows count (1-999, then "999+").
- Positioned top-right of anchor (icon or avatar).
- Color: `error` container and `on-error` text.

#### Progress Indicators
- **Linear (determinate):** Horizontal bar showing percentage. Track + active indicator.
- **Linear (indeterminate):** Animated bar for unknown duration.
- **Circular (determinate):** Ring/arc showing percentage.
- **Circular (indeterminate):** Spinning ring animation.
- Track color: `surface-container-highest` or `secondary-container`.
- Indicator color: `primary`.
- Size: linear = 4dp height; circular = 48dp diameter with 4dp stroke.

#### Snackbar
- Brief message at bottom of screen. Single line or two lines.
- Optional action button (text button).
- Optional close icon.
- Container: `inverse-surface`. Text: `inverse-on-surface`. Action: `inverse-primary`.
- Duration: 4-10 seconds, then auto-dismiss.
- Shape: `shape-extra-small`.
- Elevation: level 3.
- Max width: 600dp. Position: bottom-center (or bottom-leading on larger screens).

#### Tooltips
- **Plain tooltip:** Simple text label. For icon-only buttons. Single line.
- **Rich tooltip:** Title, supporting text, optional actions. For complex elements.
- Plain: `inverse-surface` container, `inverse-on-surface` text, `shape-extra-small`.
- Rich: `surface-container` fill, higher elevation, `shape-medium`.
- Show on long-press (touch) or hover (pointer). Delay: 500ms.

### 11.3 Containment

#### Bottom Sheets
- **Standard:** Coexists with main content. Partial overlay. Draggable.
- **Modal:** Blocks main content. Scrim behind. Draggable.
- Drag handle: 32x4dp, `on-surface-variant` at 40% opacity, centered at top.
- Shape: `shape-extra-large` on top corners, 0 on bottom.
- States: hidden, peek (partial), half, expanded (full).
- Support nested scrolling within the sheet.

#### Cards
- **Elevated card:** `surface` fill + shadow elevation. Default.
- **Filled card:** `surface-container-highest` fill. No shadow. For grouped content.
- **Outlined card:** `surface` fill + `outline-variant` border. Flat but defined.
- Anatomy: container, optional header (title, subtitle, avatar), media (image/video), content (supporting text), actions (buttons, icons).
- Shape: `shape-medium`.
- States: enabled, dragged; optionally interactive (hovered, focused, pressed when clickable).

#### Carousel
- A horizontally scrolling set of items.
- **Multi-browse:** Multiple items visible at various sizes. Items morph shape as they scroll.
- **Hero:** One large featured item + smaller peek items.
- **Full-screen:** Each item fills the viewport.
- **Uncontained:** Items scroll freely without snapping.
- Items clip content with shape morphing. Define mask/clip behavior.
- Swipe to navigate. Optional pagination indicators.

#### Dialogs
- **Basic dialog:** Title, content, action buttons. Centered overlay with scrim.
- **Full-screen dialog:** Fills screen (mobile). Has top app bar with close and save.
- Container: `surface-container-high`. Shape: `shape-extra-large`.
- Scrim: `scrim` color (typically black at 32% opacity).
- Elevation: level 3.
- Actions: right-aligned, confirming action last (rightmost).
- Focus trap: keyboard focus stays within dialog.
- Close on scrim tap (basic), back button, close icon (full-screen), or cancel action.

#### Dividers
- **Full-width:** Spans the entire width.
- **Inset:** Indented from one or both edges (for lists).
- **Middle inset:** Indented equally from both edges.
- Thickness: 1dp. Color: `outline-variant`.
- Use sparingly -- prefer whitespace for separation.

#### Lists
- Vertically arranged group of text/images.
- Anatomy: container, list item (leading element, headline, supporting text, trailing element).
- **Leading elements:** Icon, avatar, image, checkbox, radio, thumbnail.
- **Trailing elements:** Icon, checkbox, switch, text, metadata.
- 1-line, 2-line, or 3-line variants (based on content density).
- Item height: 48dp (1-line), 64dp (2-line), 88dp (3-line).
- Dividers between items (optional).
- Interactive items get state layers.

#### Side Sheets
- **Standard:** Adjacent to main content. Persistent.
- **Modal:** Overlays main content with scrim.
- Slides in from trailing edge (right in LTR).
- Shape: `shape-large` on leading corners.
- Contains supplementary content, filters, or details.
- Coexists with or replaces bottom sheets on larger screens.

### 11.4 Navigation

#### Bottom App Bar
- Container at screen bottom. Houses 2-4 icon actions + optional FAB.
- Container: `surface-container`. Elevation: level 2.
- Height: 80dp.
- FAB is cradled or overlapping (optional cradle cutout).
- Scrolls off-screen on down scroll, returns on up scroll.

#### Navigation Bar (Bottom Navigation)
- 3-5 destinations at screen bottom.
- Anatomy: container, destination (icon, label, active indicator, badge).
- Active indicator: pill shape (`shape-full`), `secondary-container` fill.
- Active icon: filled variant. Inactive: outlined variant.
- Labels always visible or only on active (consistent choice).
- Container: `surface-container`. Height: 80dp.

#### Navigation Drawer
- **Standard:** Inline, pushes content.
- **Modal:** Overlays content with scrim.
- Contains destination items grouped by sections with optional headers/dividers.
- Active item: `secondary-container` fill on indicator, `on-secondary-container` text.
- Width: 360dp (standard), 256-360dp (modal).
- Shape: `shape-large` on trailing corners (when opening from start edge).
- Header area for logo/brand/profile.

#### Navigation Rail
- Vertical strip on the leading edge (tablet/desktop).
- 3-7 destinations stacked vertically.
- Optional FAB at top.
- Active indicator: `secondary-container` pill.
- Width: 80dp. Item height: 56dp.
- Labels below icon or hidden.
- Aligns with bottom navigation bar on compact screens.

#### Tabs
- **Primary tabs:** Top-level content organization. Indicator at bottom of active tab (full width or fitted).
- **Secondary tabs:** Nested within primary tab content. Indicator spans full width.
- Anatomy: container, tab item (icon, label, indicator).
- Container: `surface`. Indicator: `primary` (primary tabs), `on-surface` (secondary tabs).
- Scrollable (when many tabs) or fixed (equal width, few tabs).
- Swipe to navigate between tab content (optional).

#### Top App Bar
- **Center-aligned:** Title centered, navigation icon left, action(s) right.
- **Small:** Title left-aligned, same as center but left.
- **Medium:** Two-row on expand, title below action row.
- **Large:** Larger title text, collapses on scroll.
- Container: `surface` or `surface-container`. Elevation on scroll.
- Scroll behavior: fixed, scrolling (hides on scroll down), compressing (shrinks).
- Colors can change on scroll (elevate = apply surface tint).

#### Search
- **Search bar:** Persistent, full-width text field styled as a bar. Always visible.
- **Search view:** Full-screen or expanding overlay for search interaction.
- Search bar anatomy: leading icon, placeholder text, trailing avatar/icon.
- Search view: input field, suggestions list, search history.
- Container: `surface-container-highest` (search bar). Shape: `shape-full`.

### 11.5 Selection

#### Checkbox
- **Unchecked:** Empty square outline. Border: `on-surface`.
- **Checked:** Filled square with checkmark. Fill: `primary`. Checkmark: `on-primary`.
- **Indeterminate:** Filled with dash. Used for parent/group state.
- **Error:** Checkbox in error state. Border/fill: `error`.
- Size: 18dp icon within 48dp touch target.
- Supports tristate (unchecked -> checked -> indeterminate).
- Pair with label text (always have a label for accessibility).

#### Chips
- **Assist chip:** Represents a smart action (e.g., add to calendar, share). Leading icon, outlined.
- **Filter chip:** For filtering content. Selected/unselected toggle. Can show checkmark. Outlined or tonal when selected.
- **Input chip:** Represents user-provided info (e.g., tags in a field). Has remove button. Avatar/icon optional.
- **Suggestion chip:** Dynamically generated recommendations. Outlined.
- Anatomy: container, leading icon/avatar, label, remove icon (input only).
- Shape: `shape-small`.
- Height: 32dp.

#### Date Pickers
- **Docked:** Inline within a form. Shows a calendar month grid.
- **Modal:** Dialog overlay with header, calendar, and actions.
- **Modal input:** Dialog with text input fields for manual date entry.
- **Range picker:** Select a start and end date. Highlight range.
- Calendar anatomy: month/year header, navigation arrows, day grid, today indicator, selected indicator.
- Selected day: `primary` circle. Today: `primary` outlined circle. Range: `primary-container` highlight.

#### Menus
- **Dropdown menu:** Appears below an anchor (button, text field).
- **Cascading/sub-menu:** Nested menu panels for hierarchical options.
- Menu items: label, optional leading icon, optional trailing text/icon, optional dividers.
- Container: `surface-container`. Shape: `shape-extra-small`. Elevation: level 2.
- Max height: constrained to viewport. Scrollable if needed.
- Position: below and aligned to anchor. Flip if near edge.

#### Radio Buttons
- Circle with inner dot when selected. Only one in a group can be selected.
- Selected: `primary` fill/dot. Unselected: `on-surface-variant` border.
- Size: 20dp icon, 48dp touch target.
- Always use in groups of 2+. Always have labels.

#### Sliders
- **Continuous:** Any value in a range. Track + thumb.
- **Discrete:** Snaps to tick marks at set intervals. Shows tick marks on track.
- **Range slider:** Two thumbs for selecting a range.
- Anatomy: track (active + inactive), thumb, value label (tooltip on drag), tick marks.
- Active track: `primary`. Inactive track: `secondary-container` or `surface-container-highest`.
- Thumb: `primary`. Value label: `primary` with `on-primary` text.

#### Switch
- Binary toggle (on/off).
- Anatomy: track, thumb (handle), optional icon in thumb.
- On state: track = `primary`, thumb = `on-primary`. Off state: track = `surface-container-highest`, thumb = `outline`.
- The thumb grows slightly on press.
- Optional icons: checkmark (on) / close (off) inside thumb.
- Size: 52x32dp.

#### Time Pickers
- **Dial (clock):** Circular clock face for selecting hour/minute. AM/PM toggle.
- **Input:** Text fields for manual hour:minute entry.
- **Modal:** Dialog wrapper for either dial or input.
- Clock dial: circular `surface-container-highest` background, `primary` selector dot and line.
- Period (AM/PM): segmented button or toggle.

### 11.6 Text Inputs

#### Text Fields
- **Filled:** Solid `surface-container-highest` background with underline indicator.
- **Outlined:** Transparent with `outline` border all around. Label floats into border gap.
- Anatomy: container, label text (floating/resting), input text, leading icon, trailing icon, supporting text (helper/error/character count), prefix/suffix.
- Label animation: rests inside when empty, floats up/shrinks when focused or filled.
- Error state: border/underline + label + supporting text turn `error` color.
- Character counter: right-aligned supporting text showing "x / max".
- Multi-line (textarea) variant.
- Disabled state: reduced opacity, no interaction.

---

## 12. ADAPTIVE DESIGN & RESPONSIVE BEHAVIOR

### 12.1 Component Adaptation
Specify how components change across window size classes:
- Bottom navigation bar -> Navigation rail (medium) -> Navigation drawer (expanded)
- Bottom sheet -> Side sheet (expanded)
- Dialog -> Full-screen dialog (compact) -> Inline or side panel (expanded)
- Tabs: scrollable (compact) -> fixed (when space allows)
- Cards: full-width (compact) -> grid (expanded)
- FAB: standard (compact) -> extended (expanded, if space allows)

### 12.2 Responsive Patterns
- **Reflow:** Content reflows from single column to multi-column.
- **Reveal:** Hidden navigation becomes persistent at larger sizes.
- **Transform:** A component transforms into a different component (e.g., bottom sheet -> side sheet).
- **Expand:** Content areas grow to fill available space (up to max width).
- **Position:** Elements reposition (e.g., search bar -> search in app bar).

### 12.3 Foldable & Multi-Screen
- Define behavior on foldable devices (fold-aware layouts).
- Content should avoid the fold/hinge area.
- Table-top posture: content in top half, controls in bottom half.
- Book posture: list-detail across the fold.

---

## 13. THEMING & CUSTOMIZATION

### 13.1 Theme Structure
Define how themes are organized:
- **Baseline theme:** The default Material-inspired theme. All tokens have baseline values.
- **Brand theme:** Overrides baseline with brand-specific values (colors, fonts, shapes).
- **Product theme:** Further overrides for a specific product within a brand.
- **Component overrides:** Per-instance customization of component tokens.

### 13.2 Color Theming
- How to override the seed/source color and regenerate all palettes.
- How to override individual color roles.
- Supporting multiple brand themes (e.g., sub-brands, white-label).

### 13.3 Typography Theming
- Swapping font families (brand + plain).
- Adjusting the type scale (sizes, weights, letter spacing).
- Supporting multiple scripts (Latin, CJK, Arabic, Devanagari) with appropriate fonts and adjustments.

### 13.4 Shape Theming
- Override the shape scale globally.
- Switch between rounded and cut corner families.
- Per-component shape overrides.

### 13.5 Dark / Light Mode
- System-preference detection (`prefers-color-scheme`).
- Manual toggle with user preference persistence.
- Transition animation between modes (crossfade or instant).
- Define any component-specific adjustments between modes.

### 13.6 High Contrast Mode
- Support `prefers-contrast: more` / `forced-colors`.
- Increase border widths, use higher-contrast color pairings.
- Outline all interactive elements.

---

## 14. CONTENT & WRITING GUIDELINES

### 14.1 Voice & Tone
- Define the brand's written voice (concise, friendly, professional, etc.).
- Tone adapts to context: errors are empathetic, success is celebratory, instructions are clear.

### 14.2 UI Text Conventions
- **Buttons:** Use verbs/actions. Sentence case. Short (1-3 words). E.g., "Save changes", not "CLICK HERE TO SAVE".
- **Labels:** Sentence case. Clear, concise.
- **Headings:** Sentence case (not Title Case unless brand dictates).
- **Error messages:** Say what happened, why, and how to fix it.
- **Empty states:** Friendly, actionable. Show illustration + message + CTA.
- **Loading states:** Brief, reassuring. "Loading..." or contextual message.
- **Confirmation dialogs:** Clear question, distinct action labels (not "Yes"/"No" but "Delete"/"Cancel").

### 14.3 Internationalization (i18n)
- Design for text expansion (translations may be 30-200% longer).
- Support RTL layouts (mirrored).
- Use locale-aware formatting (dates, numbers, currency).
- Avoid hardcoded strings.

---

## 15. DATA VISUALIZATION (Charts & Graphs)

### 15.1 Color Usage
- Use the color system's palette for data series (primary, secondary, tertiary, then extended palette).
- Ensure adjacent data series have sufficient contrast.
- Provide patterns/textures in addition to color for accessibility.

### 15.2 Typography
- Axis labels: `label-small` or `body-small`.
- Data labels: `label-medium`.
- Chart titles: `title-medium` or `title-large`.

### 15.3 Chart Types
Define styling guidance for:
- Bar charts (horizontal/vertical, grouped, stacked)
- Line charts (single, multi-series, area)
- Pie/donut charts
- Scatter plots
- Sparklines
- Gauges/meters

### 15.4 Interaction
- Hover/tap to show tooltip with data details.
- Pan/zoom for dense data.
- Animate data transitions (bar growth, line drawing).

---

## 16. ILLUSTRATION & IMAGERY

### 16.1 Illustration Style
- Define the illustration style (flat, isometric, hand-drawn, geometric, 3D, etc.).
- Color palette for illustrations (derived from brand color system).
- Line weight consistency.
- Level of detail guidance.

### 16.2 Photography Guidelines
- Treatment (full color, duotone, with overlay, rounded corners).
- Aspect ratios per context (hero: 16:9, thumbnail: 1:1, card: 4:3).
- Content guidelines (diverse, authentic, brand-appropriate).

### 16.3 Image Sizing & Containers
- Define image container shapes (rounded with `shape-medium`, etc.).
- Responsive image behavior (cover, contain, crop).
- Placeholder/skeleton loading for images.

---

## 17. PLATFORM-SPECIFIC GUIDANCE

### 17.1 Web
- CSS architecture (custom properties, utility classes, component classes).
- CSS-in-JS or CSS Modules or vanilla CSS conventions.
- Responsive units: rem for type, px for borders/shadows, % or fr for layout.
- Print styles.

### 17.2 Android
- Compose theme structure (MaterialTheme, colorScheme, typography, shapes).
- XML theme resources.
- Dynamic color via Monet/Material You.
- Edge-to-edge and system bar handling.

### 17.3 iOS
- SwiftUI theme/environment approach.
- UIKit appearance proxies.
- Dynamic Type integration.
- Safe area handling.

### 17.4 Cross-Platform (Flutter, React Native, etc.)
- Theme provider architecture.
- Platform-adaptive components (Cupertino on iOS, Material on Android).
- Shared design tokens.

---

## OUTPUT FORMAT

When generating the style guide, output these deliverables:

1. **Design Token File** -- A structured token file (JSON, YAML, or code) with all tokens defined.
2. **Color Palette** -- Complete light and dark color schemes with hex values.
3. **Typography Scale** -- Full type scale with all properties.
4. **Component Spec Sheets** -- For each component: anatomy diagram description, token mapping, state behavior, usage guidelines.
5. **Code Snippets** -- Platform-appropriate code showing how to implement the theme (CSS custom properties, theme provider, etc.).
6. **Do's and Don'ts** -- Key guidelines for maintaining consistency.

Tailor everything to the user's specific project. Use their brand name, colors, and technology stack throughout. Do not produce generic Material output -- reimagine every concept for their unique context.

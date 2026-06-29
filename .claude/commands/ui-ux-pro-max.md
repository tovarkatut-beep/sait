---
name: ui-ux-pro-max
description: "UI/UX design intelligence for web and mobile. Includes 50+ styles, 161 color palettes, 57 font pairings, 161 product types, 99 UX guidelines, and 25 chart types across 10 stacks (React, Next.js, Vue, Svelte, SwiftUI, React Native, Flutter, Tailwind, shadcn/ui, and HTML/CSS). Actions: plan, build, create, design, implement, review, fix, improve, optimize, enhance, refactor, and check UI/UX code. Projects: website, landing page, dashboard, admin panel, e-commerce, SaaS, portfolio, blog, and mobile app. Elements: button, modal, navbar, sidebar, card, table, form, and chart. Styles: glassmorphism, claymorphism, minimalism, brutalism, neumorphism, bento grid, dark mode, responsive, skeuomorphism, and flat design. Topics: color systems, accessibility, animation, layout, typography, font pairing, spacing, interaction states, shadow, and gradient. Integrations: shadcn/ui MCP for component search and examples."
---

# UI/UX Pro Max - Design Intelligence

Comprehensive design guide for web and mobile applications. Contains 50+ styles, 161 color palettes, 57 font pairings, 161 product types with reasoning rules, 99 UX guidelines, and 25 chart types across 10 technology stacks. Searchable database with priority-based recommendations.

## When to Apply

This Skill should be used when the task involves UI structure, visual design decisions, interaction patterns, or user experience quality control.

### Must Use

This Skill must be invoked in the following situations:

- Designing new pages (Landing Page, Dashboard, Admin, SaaS, Mobile App)
- Creating or refactoring UI components (buttons, modals, forms, tables, charts, etc.)
- Choosing color schemes, typography systems, spacing standards, or layout systems
- Reviewing UI code for user experience, accessibility, or visual consistency
- Implementing navigation structures, animations, or responsive behavior
- Making product-level design decisions (style, information hierarchy, brand expression)
- Improving perceived quality, clarity, or usability of interfaces

### Recommended

This Skill is recommended in the following situations:

- UI looks "not professional enough" but the reason is unclear
- Receiving feedback on usability or experience
- Pre-launch UI quality optimization
- Aligning cross-platform design (Web / iOS / Android)
- Building design systems or reusable component libraries

### Skip

This Skill is not needed in the following situations:

- Pure backend logic development
- Only involving API or database design
- Performance optimization unrelated to the interface
- Infrastructure or DevOps work
- Non-visual scripts or automation tasks

**Decision criteria**: If the task will change how a feature looks, feels, moves, or is interacted with, this Skill should be used.

---

## Rule Categories by Priority

Follow priority 1→10 to decide which rule category to focus on first.

| Priority | Category | Impact | Domain | Key Checks (Must Have) | Anti-Patterns (Avoid) |
|----------|----------|--------|--------|------------------------|----------------------|
| 1 | Accessibility | CRITICAL | ux | Contrast 4.5:1, Alt text, Keyboard nav, Aria-labels | Removing focus rings, Icon-only buttons without labels |
| 2 | Touch & Interaction | CRITICAL | ux | Min size 44×44px, 8px+ spacing, Loading feedback | Reliance on hover only, Instant state changes (0ms) |
| 3 | Performance | HIGH | ux | WebP/AVIF, Lazy loading, Reserve space (CLS < 0.1) | Layout thrashing, Cumulative Layout Shift |
| 4 | Style Selection | HIGH | style, product | Match product type, Consistency, SVG icons (no emoji) | Mixing flat & skeuomorphic randomly, Emoji as icons |
| 5 | Layout & Responsive | HIGH | ux | Mobile-first breakpoints, Viewport meta, No horizontal scroll | Horizontal scroll, Fixed px container widths, Disable zoom |
| 6 | Typography & Color | MEDIUM | typography, color | Base 16px, Line-height 1.5, Semantic color tokens | Text < 12px body, Gray-on-gray, Raw hex in components |
| 7 | Animation | MEDIUM | ux | Duration 150–300ms, Motion conveys meaning, Spatial continuity | Decorative-only animation, Animating width/height, No reduced-motion |
| 8 | Forms & Feedback | MEDIUM | ux | Visible labels, Error near field, Helper text, Progressive disclosure | Placeholder-only label, Errors only at top, Overwhelm upfront |
| 9 | Navigation Patterns | HIGH | ux | Predictable back, Bottom nav ≤5, Deep linking | Overloaded nav, Broken back behavior, No deep links |
| 10 | Charts & Data | LOW | chart | Legends, Tooltips, Accessible colors | Relying on color alone to convey meaning |

---

## Quick Reference

### 1. Accessibility (CRITICAL)

- **color-contrast** — Minimum 4.5:1 ratio for normal text (large text 3:1)
- **focus-states** — Visible focus rings on interactive elements (2–4px)
- **alt-text** — Descriptive alt text for meaningful images
- **aria-labels** — aria-label for icon-only buttons; accessibilityLabel in native
- **keyboard-nav** — Tab order matches visual order; full keyboard support
- **form-labels** — Use label with for attribute
- **skip-links** — Skip to main content for keyboard users
- **heading-hierarchy** — Sequential h1→h6, no level skip
- **color-not-only** — Don't convey info by color alone (add icon/text)
- **dynamic-type** — Support system text scaling; avoid truncation as text grows
- **reduced-motion** — Respect prefers-reduced-motion; reduce/disable animations when requested
- **voiceover-sr** — Meaningful accessibilityLabel/accessibilityHint; logical reading order for VoiceOver/screen readers
- **escape-routes** — Provide cancel/back in modals and multi-step flows
- **keyboard-shortcuts** — Preserve system and a11y shortcuts; offer keyboard alternatives for drag-and-drop

### 2. Touch & Interaction (CRITICAL)

- **touch-target-size** — Min 44×44pt (Apple) / 48×48dp (Material); extend hit area beyond visual bounds if needed
- **touch-spacing** — Minimum 8px/8dp gap between touch targets
- **hover-vs-tap** — Use click/tap for primary interactions; don't rely on hover alone
- **loading-buttons** — Disable button during async operations; show spinner or progress
- **error-feedback** — Clear error messages near problem
- **cursor-pointer** — Add cursor-pointer to clickable elements (Web)
- **gesture-conflicts** — Avoid horizontal swipe on main content; prefer vertical scroll
- **tap-delay** — Use touch-action: manipulation to reduce 300ms delay (Web)
- **standard-gestures** — Use platform standard gestures consistently
- **system-gestures** — Don't block system gestures (Control Center, back swipe, etc.)
- **press-feedback** — Visual feedback on press (ripple/highlight)
- **haptic-feedback** — Use haptic for confirmations and important actions; avoid overuse
- **gesture-alternative** — Don't rely on gesture-only interactions; always provide visible controls for critical actions
- **safe-area-awareness** — Keep primary touch targets away from notch, Dynamic Island, gesture bar and screen edges
- **no-precision-required** — Avoid requiring pixel-perfect taps on small icons or thin edges
- **swipe-clarity** — Swipe actions must show clear affordance or hint
- **drag-threshold** — Use a movement threshold before starting drag to avoid accidental drags

### 3. Performance (HIGH)

- **image-optimization** — Use WebP/AVIF, responsive images (srcset/sizes), lazy load non-critical assets
- **image-dimension** — Declare width/height or use aspect-ratio to prevent layout shift (CLS)
- **font-loading** — Use font-display: swap/optional to avoid FOIT; reserve space to reduce layout shift
- **font-preload** — Preload only critical fonts; avoid overusing preload on every variant
- **critical-css** — Prioritize above-the-fold CSS
- **lazy-loading** — Lazy load non-hero components via dynamic import / route-level splitting
- **bundle-splitting** — Split code by route/feature to reduce initial load and TTI
- **third-party-scripts** — Load third-party scripts async/defer; audit and remove unnecessary ones
- **reduce-reflows** — Avoid frequent layout reads/writes; batch DOM reads then writes
- **content-jumping** — Reserve space for async content to avoid layout jumps (CLS)
- **lazy-load-below-fold** — Use loading="lazy" for below-the-fold images and heavy media
- **virtualize-lists** — Virtualize lists with 50+ items to improve memory and scroll performance
- **main-thread-budget** — Keep per-frame work under ~16ms for 60fps
- **progressive-loading** — Use skeleton screens / shimmer instead of long blocking spinners for >1s operations
- **input-latency** — Keep input latency under ~100ms for taps/scrolls
- **tap-feedback-speed** — Provide visual feedback within 100ms of tap
- **debounce-throttle** — Use debounce/throttle for high-frequency events (scroll, resize, input)
- **offline-support** — Provide offline state messaging and basic fallback
- **network-fallback** — Offer degraded modes for slow networks

### 4. Style Selection (HIGH)

- **style-match** — Match style to product type
- **consistency** — Use same style across all pages
- **no-emoji-icons** — Use SVG icons (Heroicons, Lucide), not emojis
- **color-palette-from-product** — Choose palette from product/industry
- **effects-match-style** — Shadows, blur, radius aligned with chosen style
- **platform-adaptive** — Respect platform idioms (iOS HIG vs Material)
- **state-clarity** — Make hover/pressed/disabled states visually distinct
- **elevation-consistent** — Use a consistent elevation/shadow scale for cards, sheets, modals
- **dark-mode-pairing** — Design light/dark variants together
- **icon-style-consistent** — Use one icon set/visual language across the product
- **system-controls** — Prefer native/system controls over fully custom ones
- **blur-purpose** — Use blur to indicate background dismissal (modals, sheets), not as decoration
- **primary-action** — Each screen should have only one primary CTA; secondary actions visually subordinate

### 5. Layout & Responsive (HIGH)

- **viewport-meta** — width=device-width initial-scale=1 (never disable zoom)
- **mobile-first** — Design mobile-first, then scale up to tablet and desktop
- **breakpoint-consistency** — Use systematic breakpoints (e.g. 375 / 768 / 1024 / 1440)
- **readable-font-size** — Minimum 16px body text on mobile (avoids iOS auto-zoom)
- **line-length-control** — Mobile 35–60 chars per line; desktop 60–75 chars
- **horizontal-scroll** — No horizontal scroll on mobile
- **spacing-scale** — Use 4pt/8dp incremental spacing system
- **touch-density** — Keep component spacing comfortable for touch
- **container-width** — Consistent max-width on desktop (max-w-6xl / 7xl)
- **z-index-management** — Define layered z-index scale (e.g. 0 / 10 / 20 / 40 / 100 / 1000)
- **fixed-element-offset** — Fixed navbar/bottom bar must reserve safe padding for underlying content
- **scroll-behavior** — Avoid nested scroll regions that interfere with main scroll
- **viewport-units** — Prefer min-h-dvh over 100vh on mobile
- **orientation-support** — Keep layout readable in landscape mode
- **content-priority** — Show core content first on mobile; fold or hide secondary content
- **visual-hierarchy** — Establish hierarchy via size, spacing, contrast — not color alone

### 6. Typography & Color (MEDIUM)

- **line-height** — Use 1.5–1.75 for body text
- **line-length** — Limit to 65–75 characters per line
- **font-pairing** — Match heading/body font personalities
- **font-scale** — Consistent type scale (e.g. 12 14 16 18 24 32)
- **contrast-readability** — Darker text on light backgrounds (e.g. slate-900 on white)
- **text-styles-system** — Use platform type system: iOS Dynamic Type styles / Material 5 type roles
- **weight-hierarchy** — Bold headings (600–700), Regular body (400), Medium labels (500)
- **color-semantic** — Define semantic color tokens (primary, secondary, error, surface, on-surface) not raw hex
- **color-dark-mode** — Dark mode uses desaturated / lighter tonal variants, not inverted colors
- **color-accessible-pairs** — Foreground/background pairs must meet 4.5:1 (AA) or 7:1 (AAA)
- **color-not-decorative-only** — Functional color must include icon/text; avoid color-only meaning
- **truncation-strategy** — Prefer wrapping over truncation; when truncating use ellipsis and provide full text via tooltip
- **letter-spacing** — Respect default letter-spacing per platform; avoid tight tracking on body text
- **number-tabular** — Use tabular/monospaced figures for data columns, prices, and timers
- **whitespace-balance** — Use whitespace intentionally to group related items and separate sections

### 7. Animation (MEDIUM)

- **duration-timing** — Use 150–300ms for micro-interactions; complex transitions ≤400ms
- **transform-performance** — Use transform/opacity only; avoid animating width/height/top/left
- **loading-states** — Show skeleton or progress indicator when loading exceeds 300ms
- **excessive-motion** — Animate 1–2 key elements per view max
- **easing** — Use ease-out for entering, ease-in for exiting
- **motion-meaning** — Every animation must express a cause-effect relationship, not just be decorative
- **state-transition** — State changes should animate smoothly, not snap
- **continuity** — Page/screen transitions should maintain spatial continuity
- **parallax-subtle** — Use parallax sparingly; must respect reduced-motion
- **spring-physics** — Prefer spring/physics-based curves for natural feel
- **exit-faster-than-enter** — Exit animations shorter than enter (~60–70% of enter duration)
- **stagger-sequence** — Stagger list/grid item entrance by 30–50ms per item
- **shared-element-transition** — Use shared element / hero transitions for visual continuity between screens
- **interruptible** — Animations must be interruptible; user tap/gesture cancels in-progress animation immediately
- **no-blocking-animation** — Never block user input during an animation; UI must stay interactive
- **fade-crossfade** — Use crossfade for content replacement within the same container
- **scale-feedback** — Subtle scale (0.95–1.05) on press for tappable cards/buttons
- **gesture-feedback** — Drag, swipe, and pinch must provide real-time visual response tracking the finger
- **hierarchy-motion** — Use translate/scale direction to express hierarchy
- **motion-consistency** — Unify duration/easing tokens globally
- **opacity-threshold** — Fading elements should not linger below opacity 0.2
- **modal-motion** — Modals/sheets should animate from their trigger source
- **navigation-direction** — Forward navigation animates left/up; backward animates right/down
- **layout-shift-avoid** — Animations must not cause layout reflow or CLS

### 8. Forms & Feedback (MEDIUM)

- **input-labels** — Visible label per input (not placeholder-only)
- **error-placement** — Show error below the related field
- **submit-feedback** — Loading then success/error state on submit
- **required-indicators** — Mark required fields (e.g. asterisk)
- **empty-states** — Helpful message and action when no content
- **toast-dismiss** — Auto-dismiss toasts in 3–5s
- **confirmation-dialogs** — Confirm before destructive actions
- **input-helper-text** — Provide persistent helper text below complex inputs
- **disabled-states** — Disabled elements use reduced opacity (0.38–0.5) + cursor change + semantic attribute
- **progressive-disclosure** — Reveal complex options progressively; don't overwhelm users upfront
- **inline-validation** — Validate on blur (not keystroke); show error only after user finishes input
- **input-type-keyboard** — Use semantic input types (email, tel, number) to trigger correct mobile keyboard
- **password-toggle** — Provide show/hide toggle for password fields
- **autofill-support** — Use autocomplete / textContentType attributes so the system can autofill
- **undo-support** — Allow undo for destructive or bulk actions (e.g. "Undo delete" toast)
- **success-feedback** — Confirm completed actions with brief visual feedback (checkmark, toast, color flash)
- **error-recovery** — Error messages must include a clear recovery path (retry, edit, help link)
- **multi-step-progress** — Multi-step flows show step indicator or progress bar; allow back navigation
- **form-autosave** — Long forms should auto-save drafts to prevent data loss on accidental dismissal
- **sheet-dismiss-confirm** — Confirm before dismissing a sheet/modal with unsaved changes
- **error-clarity** — Error messages must state cause + how to fix (not just "Invalid input")
- **field-grouping** — Group related fields logically
- **read-only-distinction** — Read-only state should be visually and semantically different from disabled
- **focus-management** — After submit error, auto-focus the first invalid field
- **error-summary** — For multiple errors, show summary at top with anchor links to each field
- **touch-friendly-input** — Mobile input height ≥44px
- **destructive-emphasis** — Destructive actions use semantic danger color (red) and are visually separated from primary actions
- **toast-accessibility** — Toasts must not steal focus; use aria-live="polite" for screen reader announcement
- **aria-live-errors** — Form errors use aria-live region or role="alert" to notify screen readers
- **contrast-feedback** — Error and success state colors must meet 4.5:1 contrast ratio
- **timeout-feedback** — Request timeout must show clear feedback with retry option

### 9. Navigation Patterns (HIGH)

- **bottom-nav-limit** — Bottom navigation max 5 items; use labels with icons
- **drawer-usage** — Use drawer/sidebar for secondary navigation, not primary actions
- **back-behavior** — Back navigation must be predictable and consistent; preserve scroll/state
- **deep-linking** — All key screens must be reachable via deep link / URL
- **tab-bar-ios** — iOS: use bottom Tab Bar for top-level navigation
- **top-app-bar-android** — Android: use Top App Bar with navigation icon for primary structure
- **nav-label-icon** — Navigation items must have both icon and text label; icon-only nav harms discoverability
- **nav-state-active** — Current location must be visually highlighted in navigation
- **nav-hierarchy** — Primary nav (tabs/bottom bar) vs secondary nav (drawer/settings) must be clearly separated
- **modal-escape** — Modals and sheets must offer a clear close/dismiss affordance; swipe-down to dismiss on mobile
- **search-accessible** — Search must be easily reachable; provide recent/suggested queries
- **breadcrumb-web** — Web: use breadcrumbs for 3+ level deep hierarchies
- **state-preservation** — Navigating back must restore previous scroll position, filter state, and form input

### 10. Charts & Data (LOW)

- **legends** — Always provide legends for multi-series charts
- **tooltips** — Add tooltips with exact values on hover/tap
- **accessible-colors** — Use colorblind-safe palettes; don't rely on color alone to convey meaning
- **axis-labels** — Label axes with units; use readable tick density
- **empty-chart-state** — Show meaningful empty state when no data
- **responsive-charts** — Charts must reflow and remain readable on mobile
- **data-ink-ratio** — Maximize data, minimize non-data ink (gridlines, borders)
- **chart-type-match** — Match chart type to data relationship (trend→line, comparison→bar, part-of-whole→pie/donut)

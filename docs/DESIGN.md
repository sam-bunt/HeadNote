# Headnote UI design guidance

## Purpose and character

This document guides future QML UI work; it does not authorise implementation or expand feature scope. Headnote should feel like a personal musical notebook that can gradually become a capable songwriting workspace.

Use a clean, calm, creative, spacious and understated visual language. Prefer dark-leaning, slightly warm surfaces and readable contrast. Aim for modern without futuristic styling, professional without corporate styling, and approachable to musicians without production experience. Final brand colours remain open.

## Core principles

1. **Content before chrome.** Musical content and the musician's ideas dominate; navigation and controls support them.
2. **One clear primary action per view where practical.** Make the next useful action clear without competing emphasis.
3. **Use whitespace first.** Separate information with spacing before adding containers, borders or decoration.
4. **Avoid card saturation.** Do not put every item in a card; avoid nested cards and excessive rounded rectangles.
5. **Keep surfaces restrained.** No glassmorphism. Avoid decorative gradients unless a future design specifically justifies one; avoid excessive shadows and artificial elevation.
6. **Use emphasis sparingly.** Avoid unnecessary pills/badges and large decorative statistics. The notebook must never resemble an analytics dashboard.
7. **Prefer clear labels.** Use short text where it is clearer than an icon. Icon-only controls need accessible names.
8. **Show relevant controls.** Use context and progressive disclosure rather than permanently exposing every tool.
9. **Build hierarchy through typography, spacing and contrast.** Decoration must not substitute for structure.
10. **Make motion purposeful.** Animation communicates state or continuity; avoid decorative motion and accommodate reduced-motion preferences.
11. **Keep empty states calm.** Explain the state and a useful next action without unnecessary illustrations or marketing copy.
12. **Use consistent tokens.** Avoid arbitrary values in individual components.
13. **Design accessibility from the start.** Keyboard navigation, visible focus, readable contrast and clear control states are requirements.

## Progressive complexity

A future new or simple project might expose only title, notes, source recordings and capture/add-part actions. A developed project may progressively expose tracks, timeline, piano roll, notation, TAB, Chord Lab, rhythm/drum editor, effects, mixing, MIDI and practice tools.

Expose these only when relevant to the current task and supported by the implemented feature. Do not show advanced controls merely because the capability exists elsewhere. Feature 001 exposes only notebook metadata, search and persistence; it has no recording or musical controls.

## Notebook/library

Prefer restrained lists or rows for ideas, with alignment and spacing providing structure. Avoid large floating cards for every project. Previews may eventually include title, short notes, tags, number/types of source recordings or parts, recently modified time and useful project state. Show only metadata supported by the current feature; do not assume a project contains one voice memo.

Keep search easy to locate and project selection distinct from keyboard focus. Tags are user metadata, not decorative badges. Empty-library, no-results, loading and error states should be clear and visually quiet.

## Editing/workspace

Developed projects may become technical and track-oriented. Preserve hierarchy, use contextual inspectors/panels and give tracks and timelines the available screen space. Avoid exposing every editor simultaneously. Keep original source recordings accessible independently of derived tracks and interpretations. Make the transition from notebook to musical workspace understandable: complexity follows the idea.

## Design tokens

Define shared semantic tokens when UI implementation is requested. These categories are guidance, not a final palette or an instruction to create token files now:

- **Background:** base application canvas, dark-leaning and slightly warm.
- **Primary surface:** ordinary editing/navigation surfaces with restrained contrast.
- **Secondary/elevated surface:** contextual panels, menus and dialogs; distinguish with surface contrast before shadows.
- **Subtle separator/border:** boundaries only where spacing is insufficient.
- **Primary text:** main content and labels.
- **Secondary text:** supporting descriptions.
- **Muted text:** lower-priority metadata, still readable.
- **Primary accent:** primary action and deliberate emphasis; use sparingly.
- **Destructive/error, warning, success:** distinct semantic feedback with text or symbols as well as colour.
- **Focus state:** a consistently visible keyboard-focus indicator, distinct from selection.

Recommended spacing scale in logical UI units: **4, 8, 12, 16, 24, 32, 48**. Use 4 for tight relationships, 8–16 within controls/groups and 24–48 between sections or at page boundaries. Component dimensions may follow usability needs; do not add one-off spacing values without justification.

Restrained radius scale: **0, 4, 8** logical units. Use square/flat rows and workspace surfaces where appropriate, modest rounding for controls and selectively for dialogs. Do not heavily round every surface or default to pill shapes.

Typography roles:

- **Display/app title:** restrained identity treatment; avoid oversized decorative headings.
- **Page title:** highest content heading for the current view.
- **Section title:** compact grouping heading.
- **Body:** main notes and readable prose.
- **Secondary body:** supporting instructions/descriptions.
- **Metadata:** dates and ancillary information, readable at normal desktop scale.
- **Control label:** consistent, legible action/input text.

Use a robust system UI font strategy with reliable fallbacks and Unicode coverage. Do not select unusual or paid fonts yet. Define shared role sizes, weights and line heights during implementation, with user/system scaling respected rather than hard-coded tiny text.

## Component philosophy

Create a small coherent component set only as features need it. Reuse styling and interaction patterns:

- **Primary/secondary buttons:** reserve accent emphasis for the primary action; secondary actions remain quieter, with clear disabled and busy feedback.
- **Text fields:** persistent labels, clear editing boundaries and inline validation; placeholders do not replace labels.
- **Search field:** recognisable text-search interaction, clear query reset and distinct loading/no-results feedback.
- **Project/library row:** compact title-led hierarchy, useful supporting metadata, clear selection and focus; avoid card-like elevation.
- **Tag:** compact readable metadata; add/remove affordances appear only where editing is available.
- **Source-recording row (future):** identify individual sources/takes, with relevant playback/status/provenance access; support many recordings per project.
- **Track row (future):** align track identity and relevant controls; preserve room for musical content.
- **Context menu:** secondary contextual operations with short labels; do not hide essential primary actions exclusively here.
- **Modal/dialog:** use for focused decisions, errors needing intervention or confirmation; keep copy and action hierarchy clear and restore focus on close.
- **Sidebar/navigation:** stable orientation with limited visual weight; collapse or adapt only when it serves the workspace.
- **Tabs:** use for genuinely peer views, not as decoration or a substitute for a clear hierarchy.
- **Transport controls (future):** consistent playback/recording state, keyboard access and understandable labels.
- **Sliders/knobs (future):** only for relevant continuous parameters; provide values, keyboard adjustment and understandable units. Prefer a slider when a knob adds no benefit.

Where relevant, specify **normal, hover, pressed, focused, selected, disabled, loading and error** states. Do not confuse hover, focus and selection. States must be understandable without colour alone; loading must not falsely imply an operation succeeded.

## Accessibility and interaction

Provide a logical tab order, visible focus and keyboard access to primary actions. Label controls for assistive technology; preserve focus across contextual changes and dialogs. Use readable text/background contrast, adequate interaction targets and scalable text. Contextual disclosure must remain discoverable by keyboard, not depend exclusively on hover. Destructive actions and errors require clear wording as well as visual treatment.

## Rules for Codex and future coding agents

- Read this document before implementing or modifying user-facing UI, along with the relevant feature specification.
- Reuse existing design tokens and components before adding styling.
- Do not invent colours, spacing values, radii or typography styles without justification.
- Do not add gradients, glass effects, decorative shadows or oversized rounding unless explicitly specified; glassmorphism is excluded by the current guidance.
- Do not redesign unrelated screens while implementing a feature.
- Do not create placeholder controls for future roadmap features.
- Preserve visual hierarchy and progressive disclosure.
- Prefer a small number of coherent components over visually distinct one-off controls.
- When requirements are ambiguous, favour the simpler, less cluttered presentation.

## Responsive direction and open decisions

Desktop comes first. Avoid assumptions that unnecessarily prevent a future mobile interface, but do not compromise desktop workspaces to imitate mobile layouts. Shared concepts and visual identity should be portable; desktop and mobile may later use different information architecture. Do not design or implement mobile UI now.

Exact palette, accent hue, font fallbacks and role metrics, icon family, control dimensions, motion durations and concrete layouts remain open for scoped UI design/implementation. No new dependencies, component implementations or assets are required by this document.

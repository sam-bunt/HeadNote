# Headnote agent guidance

- Before making changes, read `docs/PRD.md`, `docs/PRODUCT_PRINCIPLES.md`, `docs/ARCHITECTURE.md`, `docs/ROADMAP.md` and the relevant specification in `docs/features/`.
- Before implementing or modifying user-facing UI, read `docs/DESIGN.md`. Reuse design tokens/components, preserve progressive disclosure and avoid unrelated redesigns or placeholder controls for future features.
- Work only on the explicitly requested feature. Roadmap entries and specifications are not permission to implement them. Do not implement future functionality or make unrelated refactors.
- The musician creates all musical content. Never generate melodies, harmonies, rhythms, accompaniments or song sections on their behalf.
- Keep presentation in QML, application state and canonical musical data in C++20, and all audio functionality in JUCE. Follow the architecture document.
- Preserve original performances. Musical corrections must be explicit, controllable, non-destructive and reversible; never silently change intent.
- Implement in small, reviewable increments. Write tests appropriate to the changed behavior and feature acceptance criteria; run relevant tests before declaring completion. Report any checks that could not run.
- Avoid premature abstractions and unnecessary dependencies. Explain important architectural decisions, tradeoffs and departures from a specification.
- Summarise changes, validation and remaining limitations. Documentation-only requests must not introduce application source code.

# Headnote architecture

## Status

This is the intended architecture. No application implementation is authorised by this document. Introduce components only when required by an explicitly requested feature.

## Technology ownership

- **C++20:** application operations, state, validation and the canonical musical domain model.
- **Qt 6 with Qt Quick/QML:** desktop presentation, interaction and bindings to C++ state. QML must not own business rules, persistence or audio logic.
- **JUCE:** all audio functionality from the first audio feature onward, including recording, playback, device management, MIDI and future real-time DSP. Do not introduce a parallel Qt audio implementation.
- **Python:** initial ML/music-transcription experiments, accessed through a replaceable transcription boundary when integrated.
- **SQLite:** local searchable project metadata, including titles, notes and user-defined tags.
- **CMake:** build configuration and eventual test integration.

## Application boundaries

QML invokes C++ application operations and observes exposed state. C++ validates operations and coordinates persistence, musical editing, transcription and audio services. UI code must not directly query SQLite or drive an audio engine.

Keep audio work separate from UI and persistence work. When audio is introduced, define ownership, lifecycle and thread communication explicitly. Real-time callbacks must avoid blocking operations, database access, Python execution and UI calls; prepare data off the audio thread.

Use the smallest boundary needed for the current feature. Feature 001 needs notebook state and metadata persistence; it does not need an audio engine or transcription service implementation.

## Portability

Keep canonical C++ musical and application logic portable, avoiding Windows-specific assumptions wherever reasonably possible. Separate it from platform/UI integration, audio implementation details, persistence and transcription. Isolate necessary platform-specific behavior at those boundaries rather than embedding it in musical data or application rules.

Headnote remains desktop-first. These constraints preserve feasibility for a future mobile application or companion, without adding mobile builds, dependencies or speculative APIs now. Mobile platform, audio and packaging decisions remain deferred.

## Canonical musical information

C++ owns the authoritative musical model. When musical features arrive, represent user-created events and their musical timing, pitch, duration and track association independently of any display format. Resolve detailed units, expressive pitch, timing and event types in those feature specifications rather than prematurely fixing a complete schema.

Piano roll, guitar/bass TAB, sheet music and other instrument views derive from this information. TAB fingering or notation layout must not become the sole source of musical truth. Instrument constraints and user-selected interpretation belong alongside the model where required, without making guitar the default.

Original humming, singing, beatboxing and instrument recordings remain permanently preserved as immutable source assets. Derived information retains provenance across source → transcription → edited transcription → instrument interpretation → arrangement. Support replaying and re-transcribing sources, comparing interpretations, rejecting edits and restoring earlier derived versions when these workflows are implemented. Assistance must expose settings and support rejection or reversal. Never silently modify musical intent.

User-directed chord exploration and performance-input events enter the same canonical musical information as other user-created material. Previews must not silently commit changes. Instrument playability, fingering and practice views derive from that information; guide-track replacement must not overwrite source recordings. Define details only in the relevant feature specifications.

## Project persistence

A project can contain only notebook metadata initially and only a voice memo once recording is available. Musical tracks and arrangements are optional additions.

SQLite stores searchable metadata. Future audio and other assets should be managed as project-associated files, with stable identifiers and references; specify the storage layout, recovery and portability before implementing asset features. Do not assume audio belongs in SQLite.

Specify source retention, derived-version history and provenance persistence when assets and musical editing are introduced. Replacing a guide track or accepting an edit must preserve the source and its relationships. Do not introduce this future storage machinery in Feature 001.

Persistence operations must report failure, maintain consistent metadata and avoid falsely reporting unsaved changes as saved. Introduce schema versioning and migrations as the persisted format evolves. Keep storage access behind C++ operations so the UI does not depend on database details.

## Transcription boundary

Integrated transcription must use an abstraction with explicit input, output, errors and provenance. It should accept user-provided source material and return candidate musical information and uncertainty where available. The application remains responsible for canonical state and user review.

Python implementation details must not leak into QML, persistence or the musical model. A later native inference implementation must be substitutable without changing the rest of the application. Choose process communication, model packaging and runtime dependencies when transcription is requested.

## Validation and incremental delivery

Test C++ domain/application behavior, persistence and relevant UI interactions at the appropriate level. Add audio and transcription boundary tests when those capabilities arrive. Tests should verify observable behavior and product rules rather than mirror implementation details.

Avoid unnecessary dependencies and speculative frameworks. Document significant choices, test the requested feature and do not implement future roadmap functionality without explicit authorisation.

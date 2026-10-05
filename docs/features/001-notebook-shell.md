# Feature 001: Notebook/application shell

## Status

Specification only. Do not implement until explicitly requested. Read [PRD](../PRD.md), [product principles](../PRODUCT_PRINCIPLES.md), [architecture](../ARCHITECTURE.md) and [roadmap](../ROADMAP.md) before implementation.

## Goal

Provide an idea-first desktop notebook shell in which a musician can create, organise, find and reopen song-idea entries. Establish a useful foundation without requiring musical content, theory knowledge or a production timeline.

## In scope

- A Qt Quick/QML desktop window with library navigation and an entry detail/editor area.
- Create a project entry with a title; use a visible default title for an initially untitled idea.
- View the local project library and select an entry.
- Edit an entry's title and free-form notes.
- Add and remove user-defined text tags; prevent duplicate tags within an entry.
- Search titles, notes and tags through one text query. An empty query shows all entries; search is case-insensitive and supports substring matches, without requiring SQLite FTS or another dependency.
- Persist entries and their metadata locally in SQLite; retain stable project identity across edits and restarts.
- Clear empty-library, no-search-results, loading and save/load-error states.
- Keyboard-accessible primary navigation and editing controls.

## Expected workflow

1. Launch into the library, with a clear create action if it is empty.
2. Create an entry and open its detail editor.
3. Edit the title, write notes and assign tags.
4. Save metadata through an explicit save action with visible success or failure feedback; indicate pending edits.
5. Search the library and select a matching entry.
6. Restart and reopen the saved entry with the same metadata.

Navigating away or closing with pending edits must offer save, discard or cancel. A failed save retains the pending edits and allows retry; it must not be reported as successful. Define the concrete UI layout during implementation within this scope.

## Architecture requirements

- C++20 owns notebook state, validation, search coordination and persistence operations.
- QML owns presentation and interaction, using C++ operations and exposed state.
- SQLite stores searchable metadata; CMake builds the application and its tests.
- Keep the implementation small. Do not create speculative musical schemas, audio services, transcription runtimes or empty future subsystems.
- JUCE is mandatory from the first audio feature onward; this feature contains no audio functionality and does not require audio integration.

## Out of scope

Recording or importing audio, playback, audio devices, transcription/ML/Python integration, piano roll, musical-note editing, instruments, tracks, arrangement, corrections, TAB, notation, rhythms, chords, DSP/effects, MIDI, exports and practice tools.

Project deletion, cloud sync, accounts, collaboration, attachments and project file interchange are also outside this feature. Do not add inactive controls implying these capabilities exist.

## Acceptance criteria

1. The application opens successfully into a usable notebook shell with an understandable empty state and clear feedback while loading.
2. Creating two entries yields distinct persistent identities and selectable library items.
3. Titles, multiline notes and tags can be edited and saved; an empty title resolves to the visible default rather than an invisible library item.
4. Adding the same tag twice does not create duplicates; removing a tag persists after restart.
5. Search finds saved entries by title, note text or tag, case-insensitively; clearing the query restores the full library and unmatched queries show a clear no-results state.
6. Saved metadata survives restart, including Unicode text, without mixing data between entries.
7. Unsaved edits are indicated and navigation/close offers save, discard or cancel.
8. Save/load failures show actionable feedback. Failed saves retain pending edits and do not claim success.
9. Primary actions and editing controls are usable with a keyboard.
10. The feature includes no audio or musical-content functionality and introduces no generated music.

## Validation required when implemented

- Automated tests for notebook operations, title handling, tag uniqueness/removal and search behavior.
- SQLite integration tests for create/update/reopen, Unicode and multiline round trips, entry isolation and representative persistence failures, using an isolated temporary database.
- Appropriate UI checks for creation, selection, editing, pending-edit handling, search and empty/error states; verify keyboard operation.
- Run the relevant automated tests and a desktop smoke check before declaring completion. Report commands, results and any checks that could not run.

No application code or tests are created as part of this documentation-only specification task.

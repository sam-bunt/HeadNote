# Headnote product requirements

## Status and purpose

This document describes the planned product, not an implementation commitment. Development is authorised one feature at a time through an explicit request and its feature specification. The first specification is [001: Notebook shell](features/001-notebook-shell.md).

Headnote is an idea-first, ear-first musical notebook and songwriting workspace, currently desktop-first.

The core user problem is: “I can hear music in my head, but I may not know enough music theory, notation, production software, or instrumental technique to turn it into something usable.”

## Core product rule

The musician creates the musical content. Headnote may record, transcribe, translate, reproduce, visualise, explain, organise, correct and help the musician edit their own musical input. It must not generate musical content on their behalf.

This excludes automatic composition of melodies, chord progressions, beats, accompaniment, arrangements or song sections. Transcription and representation preserve user input; correction is an explicit editing aid with controllable settings and reversible results.

## Users and workflow

Primary users are songwriters and musicians with varying levels of theory knowledge, notation literacy and instrumental skill. No particular instrument, especially guitar, is assumed.

A project may begin as only a voice memo. The musician can later transcribe it, edit notes and timing, select an instrument, add their own parts and organise tracks into a complete song. A project need not contain notes, tracks or notation to be valid. Each stage should remain useful independently.

A project is a container for a musical idea with zero, one or many source recordings. It may collect a hummed guitar part and variations, bass and string ideas, beatboxed drums, vocals, alternative takes and later real-instrument recordings. Each source is independently preserved and need not have an assigned instrument. Do not assume one recording per project or instrument, or one source per track. Derived data retains provenance to the specific recording from which it came.

Conceptually: project → many source recordings → zero or more transcriptions per source → edited musical interpretations → tracks/arrangement. This describes future relationships, not a recording schema or Feature 001 functionality.

The intended journey is: idea in head → capture → preserve original → transcribe/understand → edit/experiment → choose instruments → arrange into tracks → translate into playable forms → practise → play/record in real life.

Interaction should support listening, comparing and experimenting before requiring theory terminology. A project begins with an idea rather than an empty production timeline. Projects may stay simple; track, recording, effects, mixing and MIDI workflows appear as the idea develops. An advanced project may become a lightweight songwriting workstation without forcing that complexity at the start.

## Intended differentiation

Headnote combines an idea-first notebook, ear-first interaction for users with limited theory knowledge, permanent preservation of the original musical thought, translation into multiple instruments and representations, and musician-controlled experimentation. Its long-term goal is to take an imagined idea into something the musician can physically learn and play, while preserving their authorship without generative composition. Voice-to-MIDI, humming-to-notation and memo storage are parts of that journey rather than its whole purpose.

## Planned capabilities

- A searchable notebook/library of song ideas with titles, notes and user-defined tags.
- Voice memo recording and playback, followed by voice/humming transcription into musical notes.
- Editable piano roll and selectable instrument playback.
- Multiple instrument tracks, including guitar, bass, piano, synth, violin/strings and other instruments.
- Controllable pitch and timing assistance that preserves the original performance.
- Multitrack arrangement of musician-created material.
- Instrument-specific representations, guitar/bass TAB derived from user-created notes and interactive/playable TAB.
- Standard sheet-music representation.
- Beatboxing/rhythm input with an editable rhythm representation, plus live computer-keyboard drum performance that records the user's timing as rhythm events.
- Future performance mappings for percussion, notes, user-assigned chord triggers and samples, followed by MIDI keyboards and pad controllers. These capture user performances rather than compose them.
- Chord Entry & Exploration (working title: Chord Lab): user-entered progressions, playback, editing and notation; semitone transposition, root and quality changes, inversions and voicings; preview, version comparison and explicit acceptance or rejection.
- Optional chord explanations and subjective descriptors such as tense, open or dreamy, clearly distinguished from strict theory. The user chooses what to audition; the application does not decide which chord they should use or fill a missing progression.
- Playable instrument views, keyboard visualisation, fingering/performance guidance, looped playback, slowing without pitch change and practice mode.
- Real-instrument recording, with guide tracks that can be muted or replaced by the musician's recorded performance while preserving source assets.
- Effects, sound design, mixing, MIDI and MIDI/MusicXML/audio/stem exports.

These are future capabilities, sequenced in [ROADMAP.md](ROADMAP.md); they are not all part of the initial shell.

## Product requirements

1. Capture and retrieval must work without theory knowledge or notation entry.
2. Projects develop incrementally without forcing a complete song structure at creation.
3. Original humming, singing, beatboxing and instrument recordings remain permanently preserved as immutable source assets. Derived data retains provenance through transcription, edited transcription, instrument interpretation and arrangement. Users can replay or re-transcribe a source, compare it with a transcription, reject edits and restore earlier derived versions.
4. Corrections expose their effect and can be adjusted, rejected or reversed.
5. Piano roll, TAB, sheet music and instrument-specific views share canonical musical information.
6. Searchable metadata persists locally using SQLite. Audio and other project assets must be associated reliably with their project when introduced.
7. Empty, loading and error states provide clear feedback. Failed persistence must not be presented as success.
8. The desktop UI must support practical keyboard navigation and readable controls.
9. Theory explanations are optional. Users can audition chord types or transpose notes/chords and decide by ear; musical changes apply only through explicit user choice.
10. Translation and practice should help the musician perform the idea physically, then record that performance.

## Initial release scope

Feature 001 establishes only the desktop application shell and local notebook: create and retrieve project entries, edit titles/notes/tags, search metadata and persist it across restarts. It has no recording, transcription, musical editing or playback.

## Success criteria

- A musician can capture a named idea as text, find it and reopen it after restarting.
- Subsequent features can accumulate multiple source recordings in a project without requiring notation or an instrument assignment.
- Transcription and assistance retain a traceable relationship to the musician's input.
- A project can grow into multiple musician-created tracks without replacing its original source material.
- Each feature meets its acceptance criteria and passes appropriate tests before the next feature begins.

## Constraints and open decisions

Use C++20, Qt 6/Qt Quick/QML, JUCE, SQLite and CMake as described in [ARCHITECTURE.md](ARCHITECTURE.md). Python is initially for ML/music-transcription experimentation behind a replaceable abstraction.

Target desktop operating systems, distribution, asset packaging, source/derived-version storage, transcription models, instrument libraries and detailed export formats require decisions in the relevant future specifications. Practice guidance, performance mappings and chord exploration UX also need scoped specifications. Future mobile or companion applications must remain architecturally feasible, but mobile implementation is not in scope. Accounts, cloud sync and collaboration are outside the current scope.

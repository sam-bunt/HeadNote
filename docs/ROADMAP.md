# Headnote roadmap

This is an ordered product direction, not permission to implement. Each phase requires an explicit request, a scoped feature specification and appropriate passing tests before proceeding. Refine dependencies and acceptance criteria when a phase is requested.

Begin with an idea notebook and reveal workstation capabilities as ideas develop; simple projects remain valid throughout. Preserve portable C++ application/music logic for possible future mobile or companion applications, without implementing mobile support now. Source preservation, provenance and derived-version recovery are cross-phase requirements introduced with the relevant features.

## 1. Foundation/notebook

Desktop shell, local project library, titles, notes, user-defined tags, metadata search and SQLite persistence. [Feature 001](features/001-notebook-shell.md) covers this phase only.

## 2. Recording

JUCE audio/device foundation, voice memo recording and playback, permanently preserved immutable source assets and projects that contain only a voice memo.

## 3. Transcription

Voice/humming to musical-note transcription behind a replaceable abstraction. Begin with Python experimentation, retain source provenance and expose results for user review and comparison with the original. Allow re-transcription without overwriting sources.

## 4. Musical editing and instrument playback

C++ canonical musical model, editable piano roll and selectable instrument playback of user-created notes. Support guitar, bass, piano, synth, violin/strings and other instruments without centring the model on guitar.

## 5. Assistance

Explicit, controllable pitch and timing assistance. Preserve original performances and derived-version provenance; support comparison, adjustment, rejection and restoration of earlier versions without generating musical content.

## 6. Multitrack composition

Multiple instrument tracks, timelines and arrangement tools for musician-created parts, retaining provenance from interpretations to arrangements. Allow a voice memo project to grow into a complete multitrack song and eventually a lightweight songwriting workstation, without requiring production complexity at project creation.

## 7. Instrument-specific representations including TAB

Instrument-specific views, guitar/bass TAB derived from user-created notes, interactive/playable TAB, piano/keyboard visualisation and fingering or performance guidance. Resolve instrument constraints through views of canonical information, helping the musician learn to physically play the idea.

## 8. General notation

Standard sheet-music representation with deliberate handling of notation choices and edits against canonical musical information.

## 9. Rhythm/drum input

Beatboxing/rhythm capture and interpretation, editable drum/percussion representation and playback of musician-created rhythms. Add live computer-keyboard drum mode recording the user's timing as rhythm events; illustrative mappings are A = kick, S = snare, D = closed hi-hat and F = open hi-hat.

Future performance mappings may extend to notes, user-assigned chord triggers and sample triggering as the relevant capabilities become available. Later MIDI keyboards and pad controllers extend the same user-performance concept. These tools capture user-created input; they do not generate beats or parts.

## 10. Chord Entry & Exploration (working title: Chord Lab)

Manual chord progression entry, editing, playback and notation. Let the user transpose chords by semitone, change roots, audition major/minor/7th/sus/add/extended/diminished/augmented and other qualities, and experiment with inversions and voicings.

Provide previews, version comparison and explicit acceptance or rejection. Offer optional explanations and clearly subjective descriptors such as tense, open or dreamy. The musician chooses alternatives and the progression; Headnote must not decide which chord they should use or generate missing progressions or accompaniment.

## 11. Real-instrument recording

Recording real instruments into projects and arrangements, with input configuration, timing integration and permanently preserved original takes. Let the musician mute or replace guide tracks after recording their real performance without overwriting source assets.

## 12. Advanced audio/DSP/MIDI/export/practice functionality

Effects, sound design, mixing, expanded MIDI input/output workflows including keyboards and pad controllers, and MIDI/MusicXML/audio/stem exports. Practice is a core imagined-idea-to-performance goal: add looped playback, slowing without pitch change and practice mode, building on playable views and guidance from earlier phases. JUCE owns audio, MIDI and real-time DSP throughout; this phase expands those capabilities rather than delaying JUCE adoption.

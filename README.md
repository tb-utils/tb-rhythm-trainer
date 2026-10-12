# TB Rhythm Trainer

A simple browser-based practice tool for musical instruments.

It gradually reveals the next measure while you play the completed previous measure.

Version: 6f  
Created: 2026-09-23  
Updated: 2026-09-25  
License: MIT

## Features
- Static HTML/CSS/JavaScript; no backend
- No installation or compilation required
- Web Audio API metronome
- Editable NOTES and CHORD_SUFFIXES
- User-defined chord separator
- Current settings are auto-saved locally with `localStorage`
- The selected Preset and Preset name are also auto-saved and restored
- Named presets are saved separately in `localStorage`
- Start/Stop toggle
- Pause/Resume toggle
- Resume continues from the same position

## Display format
- `[root + separator + chord suffix]` = chord
  - `[C]` = C major
  - `[C5]` = C power chord
  - `[C4:5]` = C power chord rooted at C4
- `C` / `C5` = single note
- `-` = rest

For a rest, interpretation is instrument-dependent. On guitar, for example, you may let the previous sound sustain or mute it.

## NOTES
Separate items with spaces or line breaks.

Examples:
`C C# D D# E F F# G G# A A# B`

With octave numbers:
`C4 C#4 D4 D#4 E4 F4 F#4 G4 G#4 A4 A#4 B4`

Drum-kit example:
`Kick Snare HiHat Tom1 Tom2 Crash Ride`

## CHORD_SUFFIXES

Use one entry per line.

`(major)` or `""` is treated as an empty suffix.

An entry without a root filter applies to every root in `NOTES`:

```text
7
5
```

To restrict an entry to specific roots, use:

```text
suffix{root1, root2, ...}
```

For example:

```text
7{E, A, B}
m{E, A}
dim{B, D, F}
```

Whitespace is allowed around the root filter and around comma-separated root labels inside `{...}`. Do not use whitespace inside the suffix itself or inside a root label. Root labels inside `{...}` must exactly match labels in `NOTES`.

For example:

```text
:harmonic{E,A,B}           OK
:harmonic { E , A , B }    OK
natural-harmonic { E, A }  OK
natural harmonic { E, A }  NG
```

Entries are freely editable: you may add, remove, or replace them.

E-blues-oriented example:

```text
NOTES:
E G A Bb B D

CHORD_SUFFIXES:
7{E, A, B}
5
:bend{G, A, Bb, B, D}
```

Custom technique example:

```text
:harmonic{E, A, B}
```

If you normally leave `Chord separator` empty, punctuation can be included directly in the suffix itself. This can produce prompts such as `[E7]`, `[A5]`, `[D:bend]`, and `[E:harmonic]`.

## Chord separator
Chord prompts are assembled as `[root + chord separator + suffix]`.

The separator is optional. Leave it blank for standard forms such as `[C7]`, or if you prefer to include punctuation directly in `CHORD_SUFFIXES`.

Example: NOTES=`C4 D4 E4 ...`, separator=`:`, suffix=`7` → `[C4:7]`.

## Presets

The current settings are auto-saved in the browser's `localStorage`. The selected Preset and Preset name are also auto-saved and restored when the app is opened again. Multiple named presets can be stored separately. Selecting a preset loads it immediately.

Preset data includes BPM, Subdivision, Pattern, Group, Rest probability, Chord separator, NOTES, and CHORD_SUFFIXES.

Presets can also be exported and imported as JSON.

Export creates a standard browser download, with `tb-rhythm-trainer-presets.json` as the suggested filename. The browser decides how and where the file is saved, and may ask you to choose a location.

The app does not directly choose or write to arbitrary file paths.

Import uses the browser's standard file-selection control and reads only the JSON file explicitly selected by the user.

The JSON format includes an application identifier and format version, so unrelated JSON files are rejected.

## Privacy / security
This is a static client-side application:
- no backend
- no account system
- no server-side storage
- no analytics code
- no external JavaScript libraries or CDN dependencies
- settings stay in the user's browser via localStorage

The source code is the application itself and can be inspected directly.

## GitHub Pages
This repository is compatible with GitHub Pages. To publish your own fork, enable GitHub Pages for the repository root.

## Status
Prototype / experimental software. Provided as-is, without warranty.

---

# 日本語

TB Rhythm Trainer は、ブラウザだけで動く楽器練習用の簡易トレーナーです。

1小節先を徐々に表示し、その間に完成済みの前小節をユーザーが演奏します。

UIは英語を主としています。`NOTES` と `CHORD_SUFFIXES` は自由に編集でき、音名、オクターブ番号付き音名、ドラムセット等の任意ラベルにも利用できます。

このアプリは静的HTML/CSS/JavaScriptのみで動作し、バックエンド、アカウント、サーバー側保存、外部JavaScriptライブラリを使用しません。

# Synthstudio — Entwicklungs-Roadmap

> Stand: März 2026 | Aktuelle Version: v1.11.5

---

## Analyse des aktuellen Stands (v1.11.2)

### ✅ Bereits implementiert
- Synthesizer-Engine (mehrere Oscillator-Typen)
- Pattern-basierter Sequencer
- Grundlegende MIDI-Controller-Unterstützung (teilweise)
- Effekt-Kette (Reverb, Delay, Filter, EQ)
- Sample-Player / Drum-Maschine
- Auto-Updater (Electron)
- Mehrkanal-Mixer

### ⚠️ Bekannte Lücken / Optimierungsbedarf
- Nicht alle Funktionen können auf MIDI-Controller gelegt werden (unvollständige MIDI-Learn-Implementierung)
- Kein manuelles System für Tastaturkürzel-Zuweisung
- Kein BPM Auto-Sync zwischen Patterns
- Kein Tap-Tempo
- Kein MIDI-Clock-Send/Receive für externe Synchronisierung
- Fehlende Piano-Roll-Quantisierung Shortcuts
- Kein Playlist/Arrangement-View
- Kein Plugin-System (VST/AU)
- Keine Undo/Redo-History mit unbegrenzten Schritten
- Kein Projekt-Template-System

---

## Roadmap

### 🔥 Version 1.12 — MIDI & Keyboard Improvements
*Geplant: April 2026*

- [ ] **Vollständiges MIDI-Learn-System** — alle Funktionen MIDI-zuweisbar (siehe [MIDI-ASSIGNMENTS.md](./docs/MIDI-ASSIGNMENTS.md))
- [ ] **Manuelles Keyboard-Shortcut-System** — alle Aktionen keyboard-zuweisbar (siehe [KEYBOARD-SHORTCUTS.md](./docs/KEYBOARD-SHORTCUTS.md))
- [ ] **MIDI-Mapping-Presets** — speicherbar/ladbar (z.B. für Akai APC, Novation Launchpad, etc.)
- [ ] **MIDI-Feedback** — bidirektionales Mapping (LED-Rückmeldung für Controller mit Feedback)
- [ ] **Shortcut-Konflikt-Erkennung** — bei Doppelbelegung warnen
- [ ] **Shortcut Import/Export** als JSON

---

### 🎵 Version 1.13 — BPM Sync & Timing
*Geplant: Mai 2026*

- [ ] **BPM Auto-Sync zwischen Patterns** — alle Patterns laufen im selben globalen BPM (siehe [BPM-AUTOSYNC.md](./docs/BPM-AUTOSYNC.md))
- [ ] **Tap Tempo** — per Taste oder MIDI
- [ ] **MIDI Clock Receive** — Sync zu externen Geräten / DAWs
- [ ] **MIDI Clock Send** — Sync externer Geräte
- [ ] **Ableton Link** — Netzwerk-Sync mit anderen Geräten
- [ ] **Per-Pattern Tempo-Automation**
- [ ] **Swing/Groove-Quantisierung**

---

### 🎛️ Version 1.14 — DAW-Features (FL Studio-inspiriert)
*Geplant: Juni–Juli 2026*

- [ ] **Playlist / Arrangement View** — Patterns auf Zeitachse arrangieren (wie in FL Studio)
- [ ] **Piano Roll** — mit erweiterten Quantisierungsoptionen, Velocity-Editor, Note-Stretch
- [ ] **Mixer mit Sends/Returns** — vollständig routbares Mischpult
- [ ] **Automations-Clips** — Parameterautomation auf Zeitachse
- [ ] **Mixer FX-Chain** pro Kanal
- [ ] **Unlimited Undo/Redo**
- [ ] **Projekt-Templates**
- [ ] **Pattern-Farben & Benennung**
- [ ] **Schnellzugriff-Favoriten** für häufig verwendete Instrumente/Presets

---

### 🔌 Version 1.15 — Plugin & Extension System
*Geplant: Q3 2026*

- [ ] **VST3-Plugin-Host** — externe Synthesizer und Effekte laden
- [ ] **CLAP-Plugin-Unterstützung**
- [ ] **Internes Script-System** (JS-basiert für User-Automationen)
- [ ] **Preset-Browser** mit Tags und Suche
- [ ] **Cloud Preset-Sharing**

---

### 🎤 Version 2.0 — Professional DAW
*Geplant: Q4 2026*

- [ ] **Audio-Recording** — Live-Aufnahme in die Piano Roll und den Mixer
- [ ] **Audio-Clips** im Arrangement View
- [ ] **Spektral-Analyse** und Frequenz-Visualizer
- [ ] **Mastering-Suite** (Limiter, Multiband-Kompressor, Stereo-Enhancer)
- [ ] **Export** als WAV/MP3/FLAC/MIDI
- [ ] **Projekt-Collaboration** (Cloud-basiert, ähnlich Soundtrap)
- [ ] **macOS & Linux-Unterstützung**

---

## Feature-Priorisierung nach Community-Wunsch

| Feature | Priorität | Version |
|---|---|---|
| Vollständiges MIDI-Learn | 🔴 Hoch | 1.12 |
| Keyboard-Shortcut-Zuweisung | 🔴 Hoch | 1.12 |
| BPM Auto-Sync | 🔴 Hoch | 1.13 |
| Tap Tempo | 🔴 Hoch | 1.13 |
| MIDI Clock | 🟠 Mittel | 1.13 |
| Playlist View | 🟠 Mittel | 1.14 |
| Piano Roll Erweiterungen | 🟠 Mittel | 1.14 |
| VST3-Support | 🟡 Niedrig | 1.15 |
| Audio-Recording | 🟡 Niedrig | 2.0 |
| Ableton Link | 🟠 Mittel | 1.13 |

---

## Changelog Highlights

### v1.11.5 (28. März 2026)
- Versionsnummern in README und ROADMAP aktualisiert
- Dokumentation auf neuesten Stand gebracht

### v1.11.4 (28. März 2026)
- Wartungsrelease

### v1.11.3 (28. März 2026)
- Vollständige MIDI-Controller-Preset-Dateien hinzugefügt (APC40 MK2, Launchpad Pro, Maschine, BeatStep Pro, nanoKONTROL2, Generic 17-Fader)
- Tastaturkürzel-Profile hinzugefügt (Standard, FL Studio, Ableton, Logic Pro)
- Dokumentation für BPM Auto-Sync, FL-Studio-inspirierte Features und Keyboard-Shortcuts vervollständigt
- Preset-Format-Referenz und Mapping-Key-Namespace-Dokumentation erstellt
- MIDI-Assignments und Keyboard-Shortcuts Docs aktualisiert mit Links zu Preset-Dateien

### v1.11.2 (27. März 2026)
- Bugfixes und Performance-Verbesserungen

### v1.11.1 (27. März 2026)
- Stabilitätsverbesserungen

### v1.11.0 (27. März 2026)
- Neue Synthesizer-Features
- Verbesserte MIDI-Unterstützung (partiell)

---

> Diese Roadmap wird regelmäßig aktualisiert. Community-Feedback bestimmt die Prioritäten.

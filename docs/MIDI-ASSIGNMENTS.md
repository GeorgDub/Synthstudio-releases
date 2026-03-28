# Synthstudio — MIDI-Zuweisungen (Vollständige Spezifikation)

> Ziel: **Alle** Funktionen in Synthstudio müssen per MIDI-Learn auf Controller-Elemente gelegt werden können.

---

## Aktueller Status (v1.11.2)

| Bereich | MIDI-fähig | Bemerkung |
|---|---|---|
| Lautstärke Kanal | ✅ | CC-zuweisbar |
| Play/Stop | ⚠️ | Nur Note-On, kein Toggle |
| BPM | ❌ | Noch nicht implementiert |
| Pattern-Wechsel | ❌ | Fehlt |
| Effekt-Parameter (Reverb, Delay) | ⚠️ | Teilweise |
| Synthesizer-Parameter (Filter, ADSR) | ⚠️ | Teilweise |
| Mute/Solo pro Kanal | ❌ | Fehlt |
| Scene/Clip Launch | ❌ | Fehlt |
| Piano Roll Aufnahme | ❌ | Fehlt |
| Undo/Redo | ❌ | Fehlt |

---

## Geplante vollständige MIDI-Zuweisung (v1.12+)

### 1. Transport & Globale Steuerung

| Funktion | MIDI-Typ | Standard CC/Note | Beschreibung |
|---|---|---|---|
| Play | Note-On / CC | CC 115 | Wiedergabe starten |
| Stop | Note-On / CC | CC 116 | Wiedergabe stoppen |
| Play/Stop Toggle | Note-On | - | Umschalten Play/Stop |
| Record | Note-On / CC | CC 117 | Aufnahme starten |
| Tempo (BPM) | CC (14-bit) | CC 20/52 | BPM-Wert setzen (40–250) |
| Tap Tempo | Note-On | - | Tempo eintappen |
| Undo | Note-On | - | Letzten Schritt rückgängig |
| Redo | Note-On | - | Letzten Schritt wiederholen |
| Loop an/aus | Note-On / CC | CC 118 | Loop-Modus umschalten |
| Loop Start | CC | CC 21 | Loop-Startpunkt |
| Loop End | CC | CC 22 | Loop-Endpunkt |
| Metronom an/aus | Note-On | - | Metronom ein/ausschalten |

---

### 2. Pattern & Sequencer

| Funktion | MIDI-Typ | Standard CC/Note | Beschreibung |
|---|---|---|---|
| Pattern auswählen (1–16) | Note-On (C0–D#1) | - | Pattern direkt anwählen |
| Nächstes Pattern | Note-On | - | Zum nächsten Pattern |
| Vorheriges Pattern | Note-On | - | Zum vorherigen Pattern |
| Pattern kopieren | Note-On | - | Aktuelles Pattern duplizieren |
| Pattern löschen | Note-On | - | Aktuelles Pattern leeren |
| Step an/aus (1–32) | Note-On | - | Einzelnen Step toggeln |
| Pattern-Länge | CC | CC 23 | Anzahl Schritte setzen |
| Step-Lautstärke | CC | - | Velocity einzelner Steps |
| Pattern-Farbe | CC | - | Farbe des Patterns setzen |
| Scene Launch (1–8) | Note-On | - | Komplette Scene starten |

---

### 3. Mixer & Kanäle

| Funktion | MIDI-Typ | Standard CC/Note | Beschreibung |
|---|---|---|---|
| Kanal-Lautstärke (1–16) | CC | CC 1–16 | Lautstärke pro Kanal |
| Master-Lautstärke | CC | CC 7 | Gesamtlautstärke |
| Kanal-Pan (1–16) | CC | CC 17–32 | Pan pro Kanal |
| Kanal-Mute (1–16) | Note-On (Toggle) | - | Kanal stummschalten |
| Kanal-Solo (1–16) | Note-On (Toggle) | - | Kanal solo schalten |
| Send A Level | CC | CC 33 | Send-Pegel zu Return A |
| Send B Level | CC | CC 34 | Send-Pegel zu Return B |
| Kanal-EQ High | CC | CC 35 | Höhenregler |
| Kanal-EQ Mid | CC | CC 36 | Mittenregler |
| Kanal-EQ Low | CC | CC 37 | Tiefregler |

---

### 4. Synthesizer-Parameter

| Funktion | MIDI-Typ | Standard CC/Note | Beschreibung |
|---|---|---|---|
| Filter Cutoff | CC | CC 74 | Tiefpassfilter-Frequenz |
| Filter Resonance | CC | CC 71 | Filter-Resonanz |
| Filter Typ | CC | CC 76 | LP/HP/BP/Notch |
| OSC 1 Pitch | CC | CC 77 | Stimmung OSC 1 |
| OSC 2 Pitch | CC | CC 78 | Stimmung OSC 2 |
| OSC 1 Wave | CC | CC 79 | Wellenform OSC 1 |
| OSC 2 Wave | CC | CC 80 | Wellenform OSC 2 |
| OSC Mix | CC | CC 81 | Mischverhältnis OSC 1/2 |
| ADSR Attack | CC | CC 73 | Attack-Zeit |
| ADSR Decay | CC | CC 75 | Decay-Zeit |
| ADSR Sustain | CC | CC 64 | Sustain-Pegel |
| ADSR Release | CC | CC 72 | Release-Zeit |
| LFO Rate | CC | CC 12 | LFO-Geschwindigkeit |
| LFO Depth | CC | CC 92 | LFO-Intensität |
| LFO Waveform | CC | CC 93 | LFO-Wellenform |
| LFO Ziel | CC | CC 94 | LFO-Modulationsziel |
| Portamento | CC | CC 65 | Glide an/aus |
| Portamento Time | CC | CC 5 | Glide-Zeit |
| Unison Stimmen | CC | CC 95 | Unison-Anzahl |
| Unison Detune | CC | CC 96 | Verstimmung Unison |

---

### 5. Effekte

| Funktion | MIDI-Typ | Standard CC/Note | Beschreibung |
|---|---|---|---|
| Reverb Mix | CC | CC 91 | Reverb-Anteil |
| Reverb Size | CC | CC 97 | Raumgröße |
| Reverb Damping | CC | CC 98 | Dämpfung |
| Delay Mix | CC | CC 94 | Delay-Anteil |
| Delay Time | CC | CC 99 | Delay-Zeit |
| Delay Feedback | CC | CC 100 | Delay-Rückkopplung |
| Delay Sync | Note-On | - | Delay zu BPM synchronisieren |
| Chorus Mix | CC | CC 93 | Chorus-Anteil |
| Chorus Rate | CC | CC 101 | Chorus-Geschwindigkeit |
| Chorus Depth | CC | CC 102 | Chorus-Tiefe |
| Distortion | CC | CC 103 | Verzerrungs-Anteil |
| Compressor Threshold | CC | CC 104 | Kompressor-Schwelle |
| Compressor Ratio | CC | CC 105 | Kompressor-Verhältnis |
| Kompressor Attack | CC | CC 106 | Kompressor-Einsatzzeit |
| Bitcrusher | CC | CC 107 | Bitcrush-Intensität |
| Phaser Mix | CC | CC 108 | Phaser-Anteil |

---

### 6. Piano Roll

| Funktion | MIDI-Typ | Beschreibung |
|---|---|---|
| Piano Roll öffnen/schließen | Note-On | |
| Zoom In/Out | CC | |
| Quantisierung wählen | CC | 1/4, 1/8, 1/16, 1/32, 1/64 |
| Note zeichnen | — | Aus MIDI-Eingang |
| Note löschen | Note-On | Auswahl löschen |
| Transponieren +1 Halbton | Note-On | |
| Transponieren -1 Halbton | Note-On | |
| Transponieren +1 Oktave | Note-On | |
| Transponieren -1 Oktave | Note-On | |

---

## MIDI-Learn Implementierungsplan

```
Schritt 1: Rechtklick auf jedes UI-Element → "MIDI Learn"
Schritt 2: Controller bewegen/drücken → automatische Erkennung
Schritt 3: CC-Nummer, Kanal, Bereich (Min/Max) konfigurieren
Schritt 4: Mapping speichern (pro Projekt + global)

Mapping-Typen:
- Absolute CC (0-127 → Parameterwert)
- Relative CC (increment/decrement)
- Toggle (Note-On → an/aus)
- Trigger (Note-On → Einmal-Aktion)
- Velocity-sensitiv (Note-Velocity → Wert)
- 14-Bit CC (für präzisere Steuerung)
```

---

## Controller-Presets

| Controller | Preset-Name | Datei |
|---|---|---|
| Akai APC40 MK2 | `apc40mk2.json` | [presets/midi/apc40mk2.json](../presets/midi/apc40mk2.json) |
| Novation Launchpad Pro | `launchpad-pro.json` | [presets/midi/launchpad-pro.json](../presets/midi/launchpad-pro.json) |
| Native Instruments Maschine | `maschine.json` | [presets/midi/maschine.json](../presets/midi/maschine.json) |
| Arturia BeatStep Pro | `beatstep-pro.json` | [presets/midi/beatstep-pro.json](../presets/midi/beatstep-pro.json) |
| Korg nanoKONTROL2 | `nanokontrol2.json` | [presets/midi/nanokontrol2.json](../presets/midi/nanokontrol2.json) |
| Generic MIDI (17 Fader) | `generic-17fader.json` | [presets/midi/generic-17fader.json](../presets/midi/generic-17fader.json) |

---

## MIDI-Kanal-Konfiguration

- **Globaler MIDI-Kanal**: Standard Kanal 1 (konfigurierbar)
- **Pro-Instrument-Kanal**: Jedes Instrument kann auf eigenen MIDI-Kanal hören
- **Omni-Modus**: Alle Kanäle empfangen (optional)
- **MIDI-Through**: Eingehende MIDI-Daten durchleiten

---

## Bidirektionales MIDI (Feedback)

Controller mit LED-Feedback (wie Novation Launchpad, Akai APC):

```
Kanal-Mute → LED rot
Kanal-Solo → LED gelb  
Aktiver Step → LED grün
Ausgewähltes Pattern → LED blau
Play-Status → LED weiß
```

---

> Alle Mappings werden als JSON-Datei im Projektordner gespeichert und können exportiert/importiert werden.

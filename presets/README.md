# Synthstudio — Presets

Dieses Verzeichnis enthält vordefinierte Konfigurationsdateien für Synthstudio.

## Verzeichnisstruktur

```
presets/
├── midi/              MIDI-Controller-Zuweisungen
│   ├── apc40mk2.json
│   ├── launchpad-pro.json
│   ├── maschine.json
│   ├── beatstep-pro.json
│   ├── nanokontrol2.json
│   └── generic-17fader.json
└── shortcuts/         Tastaturkürzel-Profile
    ├── standard.json
    ├── fl-studio.json
    ├── ableton.json
    └── logic-pro.json
```

## MIDI-Controller-Presets

| Datei | Controller | Fader | Knobs | Pads | Feedback |
|---|---|---|---|---|---|
| `apc40mk2.json` | Akai APC40 MK2 | 8+Master | 8 Device | 40 Clip | ✅ |
| `launchpad-pro.json` | Novation Launchpad Pro MK3 | — | — | 64 | ✅ |
| `maschine.json` | Native Instruments Maschine MK3 | — | 8 | 16 | ✅ |
| `beatstep-pro.json` | Arturia BeatStep Pro | — | 16 Encoder | 16 Step | ✅ |
| `nanokontrol2.json` | Korg nanoKONTROL2 | 8 | 8 | — | ❌ |
| `generic-17fader.json` | Generic 17-Fader | 16+Master | 8 | — | ❌ |

### Format

```json
{
  "version": "1.0",
  "controller": "Controller Name",
  "mappings": {
    "transport.play": { "type": "note|cc", "note": 91, "channel": 1, "mode": "trigger|toggle" },
    "mixer.volume.1": { "type": "cc",   "cc": 7,   "channel": 1 }
  },
  "feedback": {
    "enabled": true,
    "colors": { ... }
  }
}
```

### Mapping-Schlüssel

| Bereich | Schlüssel-Präfix | Beispiele |
|---|---|---|
| Transport | `transport.` | `transport.play`, `transport.stop`, `transport.record` |
| Mixer | `mixer.` | `mixer.volume.1`, `mixer.mute.1`, `mixer.solo.1` |
| Synthesizer | `synth.` | `synth.filter.cutoff`, `synth.adsr.attack` |
| Pattern | `pattern.` | `pattern.launch.1`, `pattern.step.1` |
| Scene | `scene.` | `scene.launch.1` |
| Bearbeiten | `edit.` | `edit.undo`, `edit.redo` |

## Tastaturkürzel-Profile

| Datei | Profil | Zielgruppe |
|---|---|---|
| `standard.json` | Standard | Synthstudio-Einsteiger |
| `fl-studio.json` | FL Studio | FL Studio-Umsteiger |
| `ableton.json` | Ableton Live | Ableton-Umsteiger |
| `logic-pro.json` | Logic Pro | Logic-Umsteiger (Windows: Cmd = Ctrl) |

### Format

```json
{
  "version": "1.0",
  "profile": "Profilname",
  "shortcuts": {
    "transport.play": "Space",
    "edit.undo":      "Ctrl+Z"
  }
}
```

## Installation

Presets werden in Synthstudio über **Einstellungen → MIDI / Shortcuts → Preset laden** importiert.

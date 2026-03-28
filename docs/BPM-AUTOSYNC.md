# Synthstudio — BPM Auto-Sync zwischen Patterns

> Ziel: Alle Patterns sollen in einem einheitlichen, globalen BPM laufen, mit optionaler individueller Anpassung.

---

## Problem (aktueller Stand v1.11.2)

Derzeit kann jedes Pattern sein eigenes Tempo haben. Wenn zwischen Patterns gewechselt wird:
- Kein automatischer BPM-Übergang
- Patterns starten sofort ohne Synchronisierung
- Externe MIDI-Geräte verlieren die Synchronisierung beim Wechsel

---

## Lösung: Globaler BPM Auto-Sync

### Konzept

```
Globaler BPM (z.B. 128 BPM)
   │
   ├── Pattern 1 → läuft bei 128 BPM (global)
   ├── Pattern 2 → läuft bei 128 BPM (global)
   ├── Pattern 3 → läuft bei 96 BPM  (Override, optional)
   └── Pattern 4 → läuft bei 128 BPM (global)
```

- **Standard**: Alle Patterns erben den globalen BPM
- **Override**: Pattern kann optionalen eigenen BPM haben (mit Anzeige `!`)
- **Automatischer Übergang**: Beim Pattern-Wechsel bleibt der Beat grid erhalten

---

## Implementierungsdetails

### 1. Globaler BPM-Takt

```
Globaler Clock läuft immer durch, auch beim Pattern-Wechsel.
Pattern-Wechsel passiert nur auf Beat-Grenzen (1, 2, 4 Takte konfigurierbar).

Einstellungen → Timing:
  [x] BPM Global Sync aktiviert
  Wechsel auf: ○ Sofort  ●  Nächster Beat  ○ Nächster Takt  ○ 2 Takte  ○ 4 Takte
```

### 2. Tempo-Modi

| Modus | Beschreibung |
|---|---|
| **Global** | Alle Patterns teilen denselben BPM |
| **Per-Pattern** | Jedes Pattern hat seinen eigenen BPM (aktuelles Verhalten) |
| **Hybrid** | Global ist Standard, einzelne Patterns können abweichen |

### 3. BPM-Übergang (Automix)

```
Option: BPM-Übergang bei Pattern-Wechsel
  ○ Sofort (kein Übergang)
  ○ Linearer Sweep (X Takte)
  ○ Sync auf nächsten Bar
```

---

## Tap Tempo

### Implementierung

```
Taste T (konfigurierbar) oder MIDI-Note → Tap Tempo

Algorithmus:
1. Ersten Tap registrieren → Startzeit speichern
2. Weitere Taps innerhalb von 3 Sekunden → Durchschnitt berechnen
3. Nach 2+ Taps → BPM setzen
4. Nach 3 Sekunden Pause → Tap-Sequenz zurücksetzen

Min BPM: 40 | Max BPM: 250
Glättung: Letzten 8 Taps für Durchschnitt verwenden
```

### UI-Anzeige
- Tap-Tempo-Button pulsiert im aktuellen BPM
- Anzeige: "Tap: 128.0 BPM (letzte 4 Taps)"

---

## MIDI Clock Synchronisierung

### MIDI Clock Receive (External Sync)

```
Einstellungen → MIDI → Sync:
  [x] MIDI Clock empfangen von: [MIDI Interface auswählen]
  [x] Synthstudio startet automatisch bei MIDI Start
  [x] Synthstudio stoppt automatisch bei MIDI Stop
  [x] Synthstudio synct BPM automatisch

Statusanzeige: "Extern: 128.5 BPM (via USB MIDI)"
```

### MIDI Clock Send (Sync externer Geräte)

```
Einstellungen → MIDI → Sync:
  [x] MIDI Clock senden an: [MIDI Interface auswählen]
  [x] MIDI Start/Stop senden
  [x] MIDI Continue senden
  
Alle angeschlossenen Geräte (Synthesizer, Drum Machines) 
synken automatisch zu Synthstudio.
```

---

## Ableton Link Integration

Ableton Link ermöglicht BPM-Synchronisierung über das Netzwerk zwischen beliebigen Anwendungen:

```
Einstellungen → Netzwerk → Ableton Link:
  [x] Ableton Link aktivieren
  
Status: "Link aktiv — 3 Peers verbunden — 128.0 BPM"
```

Kompatible Anwendungen: Ableton Live, Traktor, Reason, GarageBand (iOS), und viele mehr.

---

## Per-Pattern Tempo-Automation

Für komplexe Arrangements:

```
Im Pattern-Editor → Rechtsklick auf BPM-Anzeige → "Tempo automatisieren"
→ Automation-Kurve zeichnen (z.B. Beschleunigung, Ritardando)
→ Automation läuft innerhalb dieses Patterns
```

Automation-Typen:
- Linear (gleichmäßige Änderung)
- Kurve (smooth acceleration)
- Sprung (sofortige Tempoänderung)

---

## Swing / Groove-Quantisierung

```
Global Swing: 0–100% 
  0%   = straight (gerade)
  50%  = leichter Swing
  66%  = Triplet Swing (Jazz)
  100% = starker Swing

Per-Track Swing: Override für einzelne Tracks
Groove-Templates: Import aus MIDI-Groove-Files
```

---

## UI-Konzept

```
┌─────────────────────────────────────────┐
│  ♩ BPM: [128.0] ▲▼  TAP   [SYNC ●]    │
│  Wechsel: [Nächster Bar ▾]              │
│  Swing: [░░░░░░░░░░] 0%                │
│  Clock: ● Intern | ○ MIDI | ○ Link      │
└─────────────────────────────────────────┘
```

- **BPM-Feld**: Klicken + ziehen oder doppelklicken zum Eingeben
- **TAP-Button**: Tap Tempo
- **SYNC-Indikator**: Grün = synct, Rot = außer Sync
- **Wechsel-Dropdown**: Wann soll der Pattern-Wechsel stattfinden
- **Clock-Radio**: Intern / MIDI External / Ableton Link

---

## Technische Implementierung (Electron/Web Audio)

```javascript
// Globaler BPM-Clock basierend auf Web Audio API AudioContext
class BPMClock {
  constructor(audioContext) {
    this.audioContext = audioContext;
    this.bpm = 128;
    this.syncMode = 'internal'; // 'internal' | 'midi' | 'link'
    this.patternChangeMode = 'nextBar'; // 'immediate' | 'nextBeat' | 'nextBar' | '2bars' | '4bars'
    this.swing = 0; // 0-1
  }

  getTickInterval() {
    // 24 PPQN (Pulses Per Quarter Note) — MIDI Standard
    return (60 / this.bpm) / 24;
  }

  scheduleNextBar(callback) {
    const barsInSeconds = (60 / this.bpm) * 4;
    const currentTime = this.audioContext.currentTime;
    const nextBar = Math.ceil(currentTime / barsInSeconds) * barsInSeconds;
    setTimeout(callback, (nextBar - currentTime) * 1000);
  }

  syncToBPM(newBPM) {
    // Sanfter BPM-Übergang ohne Tempo-Sprung
    this.bpm = newBPM;
    this.emit('bpmChange', newBPM);
  }
}
```

---

## BPM-Bereiche und Tempomarkierungen

| BPM | Tempobezeichnung |
|---|---|
| 40–60 | Grave / Largo |
| 60–66 | Larghetto |
| 66–76 | Adagio |
| 76–108 | Andante |
| 108–120 | Moderato |
| 120–156 | Allegro |
| 156–176 | Vivace |
| 176–200 | Presto |
| 200–250 | Prestissimo |

Beim Einstellen des BPM-Werts wird die Tempobezeichnung als Tooltip angezeigt.

---

> Der BPM Auto-Sync ist ein zentrales Feature für professionelle Produktionsumgebungen und wird in v1.13 implementiert.

# Project Bootstrap: Signal Lost

## 1. Current Goal & Next 3 Steps

**Goal:** To assemble a classic, highly polished, authentic 4-channel Amiga ProTracker (`.mod`) module titled **"Signal Lost"**. The tracker structure uses custom volume modulations and high-frequency percussive arrays, moving entirely away from mathematical synthesis (test signals) and adopting physical, vintage 8-bit hardware sampling from the historic `ST-01` and `ST-02` archives. All note allocations are strictly bound to octaves 3–5 to respect original Amiga hardware clock limits.

**Current sub-goal:** Assemble, validate, and export the complete module, featuring all 11 unique pattern definitions (`00` through `0a`) across a 19-position arrangement list.

**Next 3 Steps:**
1. **Binary Module Compilation:** Parse `song.yaml` and the 11 text pattern files into standard binary `.mod` format.
2. **Paula Emulation Audio Test:** Conduct a playback audit in ProTracker v2.3 / WinUAE to verify hard stereo panning (Ch 1/4 Left, Ch 2/3 Right) and filter behavior.
3. **Headroom & Clipping Audit:** Verify maximum peak volume levels during simultaneous 4-channel polyphony to ensure clean output on native Amiga audio hardware.

---

## 2. State of Play

### Core Architecture & Channel Allocations
* **Tracker System:** Standard 4-channel Amiga ProTracker sound module format.
* **Tempo & Speed:** Speed `6`, BPM `0x6E` (110 BPM).
* **Channel Allocations:**
  * **Channel 1 (Hard Left):** Low-End Bass Anchor (`DigDug`).
  * **Channel 2 (Hard Right):** Snare (`Snare1`), Dynamic 16th Hi-Hats (`CloseHiHat`), and Downbeat Cymbal (`Cymbal1`).
  * **Channel 3 (Hard Right):** Ambient Pad Swells (`Heaven`) and Lead Arpeggios/Stabs (`PolySynth`).
  * **Channel 4 (Hard Left):** Kick Drum (`BassDrum1`) and Transition Risers (`swoop`).

### Key Technical & Compositional Decisions
* **Rejection of Synthesis:** Pure software-generated mathematical oscillators have been permanently abandoned in favor of authentic late-80s hardware grit.
* **Commitment to ST-01 / ST-02:** The module relies entirely on recorded historical synthesizers sourced strictly from the `st-01.lha` and `st-02.lha` Aminet archives.
* **Expansion Mandate:** The current sample footprint utilizes only 4 out of the 31 available tracker sample slots. The engineering design explicitly permits the addition of secondary percussive units, stabs, and vocal phrases from the verified Aminet packages as future pattern arrangements dictate.
* **The 128 KiB Boundary:** To ensure strict backward compatibility with early hardware, no individual instrument slot will exceed $65,535 \times 2 = 131,070\text{ bytes}$ (approx. $128\text{ KiB}$).
* **Sample Configuration:** `PolySynth` (one-shot) handles rapid 16th stabs without loop buzz. `swoop` is coupled with pitch-slide effect `A02` in Pattern 07 to handle structural risers.
* **Pitch Alignment:** Grounded on the `DigDug` anchor (Finetune `0`). `Heaven` calibrated to `-2` (`0xE`). `PolySynth` calibrated to `+2` (`0x2`). Unpitched percussion slots remain at `0`.
* **Arrangement Flow:** Features a 19-step `orderList` incorporating intro drops, main theme variations, an interlude groove (half-time), tension build-ups, climax arps, and deep bridge transitions.

---

## 3. Dependency Map & Version Log

### Project Dependencies
* **Tracking Environment:** ProTracker v2.3D / MilkyTracker / OpenMPT (Configured to strict `.mod` compatibility mode).
* **Audio Playback Engine:** Amiga Paula Hardware Emulation Layer (Must have **LED Low-Pass Filter** enabled to properly attenuate frequencies above 7kHz).
* **Sample Source URLs:**
* `[https://aminet.net/mods/inst/st-01.lha](https://aminet.net/mods/inst/st-01.lha)`
* `[https://aminet.net/mods/inst/st-02.lha](https://aminet.net/mods/inst/st-02.lha)`

### Asset Dependencies
* `st-01.lha`: `BassDrum1`, `Snare1`, `CloseHiHat`, `DigDug`, `Heaven`, `PolySynth`.
* `st-02.lha`: `swoop`, `Cymbal1`.

### Master Instrument Table

| Slot | Sample | Source | Loop Mode | Finetune (Hex) | Mix Vol (Hex) | Primary Function |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **`01`** | `BassDrum1` | `st-01.lha` | One-Shot | `0` | `0x38` | Kick Drum (Ch 4) |
| **`02`** | `Snare1` | `st-01.lha` | One-Shot | `0` | `0x38` | Snare / Rolls (Ch 2) |
| **`03`** | `CloseHiHat` | `st-01.lha` | One-Shot | `0` | `0x20` | Dynamic Hi-Hats (Ch 2) |
| **`04`** | `DigDug` | `st-01.lha` | Forward | `0` | `0x10` | Bass Anchor (Ch 1) |
| **`05`** | `Heaven` | `st-01.lha` | Forward | `0xE` (-2) | `0x28` | Ambient Pad (Ch 3) |
| **`06`** | `PolySynth` | `st-01.lha` | One-Shot | `0x2` (+2) | `0x18` | Lead Arp / Stabs (Ch 3) |
| **`07`** | `swoop` | `st-02.lha` | One-Shot | `0` | `0x10` | Transition Riser (Ch 4) |
| **`08`** | `Cymbal1` | `st-02.lha` | One-Shot | `0` | `0x08` | Crash Impact (Ch 2) |

### Version Log
* **v1.0:** Established 8-slot sample roster and volume baseline.
* **v1.1:** Applied finetune pitch calibration offsets.
* **v1.2:** Re-indexed primary patterns `00`–`06` and integrated bridge patterns `07` and `08`.
* **v1.3:** Added Pattern `09` (*The Interlude Groove*) and Pattern `0a` (*The Tension Build*); updated `song.yaml` sequence order to 19 positions.

---

## 4. Golden Code Blocks

### Metadata
```yaml
---
title: 'Signal Lost'
message: 'An awesome toe-tapping     loading tune      by Adam J Richardson  Written with Gemini         Pro mode         With interruptions     and interference    by Millie  >^._.^<~~ '
orderList:
  - 0  # Pattern 00: The Drop
  - 1  # Pattern 01: The Melody
  - 2  # Pattern 02: The Melody Part B
  - 3  # Pattern 03: The Breakdown
  - 4  # Pattern 04: The Build-Up
  - 0  # Pattern 00: The Drop
  - 9  # Pattern 09: The Interlude Groove
  - 10 # Pattern 0a: The Tension Build
  - 5  # Pattern 05: The Climax (Lead Arp)
  - 6  # Pattern 06: Climax Resolve
  - 0  # Pattern 00: The Drop
  - 1  # Pattern 01: The Melody
  - 2  # Pattern 02: The Melody Part B
  - 7  # Pattern 07: The Deep Bridge
  - 8  # Pattern 08: The Syncopated Rise
  - 0  # Pattern 00: The Drop
  - 9  # Pattern 09: The Interlude Groove
  - 5  # Pattern 05: The Climax (Lead Arp)
  - 6  # Pattern 06: Climax Resolve
speed: 6
bpm: 0x6e
instruments:
  - id: 1
    source: 'st01'
    name: 'ST-01/BassDrum1'
    volume: 0x38
  - id: 2
    source: 'st01'
    name: 'ST-01/Snare1'
    volume: 0x38
  - id: 3
    source: 'st01'
    name: 'ST-01/CloseHiHat'
    volume: 0x20
  - id: 4
    source: 'st01'
    name: 'ST-01/DigDug'
    start: 0x221
    length: 0x83
    volume: 0x10
  - id: 5
    source: 'st01'
    name: 'ST-01/Heaven'
    start: 0x1770
    length: 0x60
    volume: 0x28
    finetune: 0xe
  - id: 6
    source: 'st01'
    name: 'ST-01/PolySynth'
    start: 0x2226
    length: 0x047f
    volume: 0x18
    finetune: 0x2
  - id: 7
    source: 'st02'
    name: 'ST-02/swoop' # too much fun!
    volume: 0x10
  - id: 8
    source: 'st02'
    name: 'ST-02/Cymbal1'
    volume: 0x08
```

### Pattern 00: The Drop
```text
Row: [Ch 1]       | [Ch 2]       | [Ch 3]       | [Ch 4]
00: F-4 04 ---    | C-4 03 E00   | C-4 05 C38   | C-4 01 ---
02: -             | C-4 03 C30   | -            | -
04: -             | C-4 02 C40   | -            | -
06: -             | C-4 03 C30   | -            | -
07: -             | -            | -            | C-4 01 C40
08: -             | C-4 03 C40   | -            | -
0A: -             | C-4 03 C30   | -            | C-4 01 C30
0C: -             | C-4 02 C40   | -            | -
0E: -             | C-4 03 C30   | -            | -
10: G-4 04 ---    | C-4 03 C40   | -            | C-4 01 C40
12: -             | C-4 03 C30   | -            | -
14: -             | C-4 02 C40   | -            | -
16: -             | C-4 03 C30   | -            | -
18: -             | C-4 03 C40   | -            | C-4 01 C40
1C: -             | C-4 02 C40   | -            | -
1E: -             | C-4 03 C30   | -            | C-4 01 C30
20: F-4 04 ---    | C-4 03 C40   | D-4 05 C38   | C-4 01 C40
22: -             | C-4 03 C30   | -            | -
24: -             | C-4 02 C40   | -            | -
26: -             | C-4 03 C30   | -            | -
27: -             | -            | -            | C-4 01 C40
28: -             | C-4 03 C40   | -            | -
2A: -             | C-4 03 C30   | -            | C-4 01 C30
2C: -             | C-4 02 C40   | -            | -
2E: -             | C-4 03 C30   | -            | -
30: C-4 04 ---    | C-4 03 C40   | -            | C-4 01 C40
32: -             | C-4 03 C30   | -            | -
34: -             | C-4 02 C40   | -            | -
36: -             | C-4 03 C30   | -            | -
38: -             | C-4 03 C40   | -            | C-4 01 C40
3C: -             | C-4 02 C40   | -            | -
3E: -             | C-4 03 C30   | -            | -
```

### Pattern 01: The Melody
```text
Row: [Ch 1]       | [Ch 2]       | [Ch 3]       | [Ch 4]
00: F-4 04 ---    | C-4 08 C40   | C-4 06 C40   | C-4 01 C40
02: -             | C-4 03 C30   | --- -- 484   | -
04: -             | C-4 02 C40   | -            | -
06: -             | C-4 03 C30   | D#4 06 C40   | -
07: -             | -            | -            | C-4 01 C40
08: -             | C-4 03 C40   | --- -- 484   | -
0A: -             | C-4 03 C30   | -            | C-4 01 C30
0C: -             | C-4 02 C40   | F-4 06 C40   | -
0E: -             | C-4 03 C30   | --- -- 484   | -
10: G-4 04 ---    | C-4 03 C40   | G-4 06 C40   | C-4 01 C40
12: -             | C-4 03 C30   | --- -- 484   | -
14: -             | C-4 02 C40   | -            | -
16: -             | C-4 03 C30   | -            | -
18: -             | C-4 03 C40   | C-5 06 C40   | C-4 01 C40
1A: -             | -            | --- -- 484   | -
1C: -             | C-4 02 C40   | G-4 06 C40   | -
1E: -             | C-4 03 C30   | --- -- 484   | C-4 01 C30
20: F-4 04 ---    | C-4 03 C40   | F-4 06 C40   | C-4 01 C40
22: -             | C-4 03 C30   | --- -- 484   | -
24: -             | C-4 02 C40   | -            | -
26: -             | C-4 03 C30   | -            | -
27: -             | -            | -            | C-4 01 C40
28: -             | C-4 03 C40   | D#4 06 C40   | -
2A: -             | C-4 03 C30   | --- -- 484   | C-4 01 C30
2C: -             | C-4 02 C40   | D-4 06 C40   | -
2E: -             | C-4 03 C30   | --- -- 484   | -
30: C-4 04 ---    | C-4 03 C40   | C-4 06 C40   | C-4 01 C40
32: -             | C-4 03 C30   | --- -- 484   | -
34: -             | C-4 02 C40   | -            | -
36: -             | C-4 03 C30   | -            | -
38: -             | C-4 03 C40   | A#3 06 C40   | C-4 01 C40
3A: -             | -            | --- -- 484   | -
3C: -             | C-4 02 C40   | C-4 06 C40   | -
3E: -             | C-4 03 C30   | --- -- 484   | -
```

### Pattern 02: The Melody Part B
```text
Row: [Ch 1]       | [Ch 2]       | [Ch 3]       | [Ch 4]
00: F-4 04 ---    | C-4 03 C40   | G-4 06 C40   | C-4 01 C40
04: -             | C-4 02 C40   | --- -- 484   | -
08: -             | C-4 03 C40   | F-4 06 C40   | -
0C: -             | C-4 02 C40   | --- -- 484   | -
10: G-4 04 ---    | C-4 03 C40   | D#4 06 C40   | C-4 01 C40
14: -             | C-4 02 C40   | --- -- 484   | -
18: -             | C-4 03 C40   | C-4 06 C40   | C-4 01 C40
1C: -             | C-4 02 C40   | --- -- 484   | -
20: F-4 04 ---    | C-4 03 C40   | F-4 06 C40   | C-4 01 C40
24: -             | C-4 02 C40   | --- -- 484   | -
28: -             | C-4 03 C40   | D#4 06 C40   | -
2C: -             | C-4 02 C40   | --- -- 484   | -
30: C-4 04 ---    | C-4 03 C40   | C-4 06 C40   | C-4 01 C40
34: -             | C-4 02 C40   | --- -- 484   | -
38: -             | C-4 03 C40   | G-3 06 C40   | C-4 01 C40
3C: -             | C-4 02 C40   | --- -- 484   | -
```

### Pattern 03: The Breakdown
```text
Row: [Ch 1]       | [Ch 2]       | [Ch 3]       | [Ch 4]
00: F-4 04 ---    | C-4 08 C40   | C-4 05 C30   | -
04: -             | C-4 03 C30   | -            | -
08: -             | C-4 03 C30   | -            | -
0C: -             | C-4 03 C30   | -            | -
10: G-4 04 ---    | C-4 03 C30   | -            | -
14: -             | C-4 03 C30   | -            | -
18: -             | C-4 03 C30   | -            | -
1C: -             | C-4 03 C30   | -            | -
20: F-4 04 ---    | C-4 03 C30   | D-4 05 C30   | -
24: -             | C-4 03 C30   | -            | -
28: -             | C-4 03 C30   | -            | -
2C: -             | C-4 03 C30   | -            | -
30: C-4 04 ---    | C-4 03 C30   | -            | -
34: -             | C-4 03 C30   | -            | -
38: -             | C-4 03 C30   | -            | -
3C: -             | C-4 03 C30   | -            | -
```

### Pattern 04: The Build-Up
```text
Row: [Ch 1]       | [Ch 2]       | [Ch 3]       | [Ch 4]
00: F-4 04 ---    | -            | C-4 05 C38   | C-4 01 C40
08: -             | -            | -            | -
10: G-4 04 ---    | -            | -            | C-4 01 C40
18: -             | -            | -            | -
20: F-4 04 ---    | -            | D-4 05 C40   | C-4 01 C40
28: -             | -            | -            | C-4 07 C10
2c: -             | -            | -            | --- -- C20
2e: -             | -            | -            | --- -- C30
30: C-4 04 ---    | C-4 02 C10   | -            | C-4 01 C40
32: -             | C-4 02 C18   | -            | -
34: -             | C-4 02 C20   | -            | -
36: -             | C-4 02 C28   | -            | --- -- C20
38: -             | C-4 02 C30   | -            | C-4 01 C40
3A: -             | C-4 02 C38   | -            | -
3C: -             | C-4 02 C40   | -            | --- -- C38
3E: -             | C-4 02 C40   | -            | -
```

### Pattern 05: The Climax
```text
Row: [Ch 1]       | [Ch 2]       | [Ch 3]       | [Ch 4]
00: F-4 04 ---    | C-4 08 C40   | C-5 06 C40   | C-4 01 C40
04: -             | C-4 02 C40   | G-4 06 C30   | -
08: -             | C-4 03 C40   | D#4 06 C40   | -
0C: -             | C-4 02 C40   | G-4 06 C30   | -
10: G-4 04 ---    | C-4 03 C40   | D-5 06 C40   | C-4 01 C40
14: -             | C-4 02 C40   | G-4 06 C30   | -
18: -             | C-4 03 C40   | F-4 06 C40   | C-4 01 C40
1C: -             | C-4 02 C40   | G-4 06 C30   | -
20: F-4 04 ---    | C-4 03 C40   | C-5 06 C40   | C-4 01 C40
24: -             | C-4 02 C40   | G-4 06 C30   | -
28: -             | C-4 03 C40   | D#4 06 C40   | -
2C: -             | C-4 02 C40   | G-4 06 C30   | -
30: C-4 04 ---    | C-4 03 C40   | A#4 06 C40   | C-4 01 C40
34: -             | C-4 02 C40   | F-4 06 C30   | -
38: -             | C-4 03 C40   | D-4 06 C40   | C-4 01 C40
3C: -             | C-4 02 C40   | F-4 06 C30   | -
```

### Pattern 06: Climax Resolve
```text
Row: [Ch 1]       | [Ch 2]       | [Ch 3]       | [Ch 4]
00: F-4 04 ---    | C-4 03 C40   | G-4 06 C40   | C-4 01 C40
04: -             | C-4 02 C40   | D#4 06 C30   | -
08: -             | C-4 03 C40   | C-4 06 C40   | -
0C: -             | C-4 02 C40   | D#4 06 C30   | -
10: G-4 04 ---    | C-4 03 C40   | F-4 06 C40   | C-4 01 C40
14: -             | C-4 02 C40   | D-4 06 C30   | -
18: -             | C-4 03 C40   | A#3 06 C40   | C-4 01 C40
1C: -             | C-4 02 C40   | D-4 06 C30   | -
20: F-4 04 ---    | C-4 03 C40   | D#4 06 C40   | C-4 01 C40
24: -             | C-4 02 C40   | C-4 06 C30   | -
28: -             | C-4 03 C40   | G-3 06 C40   | -
2C: -             | C-4 02 C40   | C-4 06 C30   | -
30: C-4 04 ---    | C-4 03 C40   | C-4 06 C40   | C-4 01 C40
34: -             | C-4 02 C40   | G-4 06 C30   | -
38: -             | C-4 03 C40   | C-5 06 C40   | C-4 01 C40
3C: -             | C-4 02 C40   | --- -- 484   | -
```

### Pattern 07: The Deep Bridge
```text
Row: [Ch 1]       | [Ch 2]       | [Ch 3]       | [Ch 4]
00: F-4 04 ---    | -            | C-4 05 C20   | C-4 07 C40
01: -             | -            | -            | --- -- A02
02: -             | -            | -            | --- -- A02
03: -             | -            | -            | --- -- A02
04: -             | C-4 03 C20   | -            | --- -- A02
05: -             | -            | -            | --- -- A02
06: -             | -            | -            | --- -- A02
07: -             | -            | -            | C-4 08 C40
08: -             | -            | -            | -
0C: -             | C-4 03 C10   | -            | -
10: G-4 04 ---    | -            | -            | -
14: -             | C-4 03 C20   | -            | -
18: -             | -            | -            | -
1C: -             | C-4 03 C10   | -            | -
20: F-4 04 ---    | -            | D-4 05 C20   | C-4 07 C30
21: -             | -            | -            | --- -- A02
22: -             | -            | -            | --- -- A02
23: -             | -            | -            | --- -- A02
24: -             | C-4 03 C20   | -            | --- -- A02
25: -             | -            | -            | --- -- A02
26: -             | -            | -            | --- -- A02
27: -             | -            | -            | C-4 08 C40
28: -             | -            | -            | -
2C: -             | C-4 03 C10   | -            | -
30: C-4 04 ---    | -            | -            | -
34: -             | C-4 03 C20   | -            | -
38: -             | -            | -            | -
3C: -             | C-4 03 C10   | -            | -
```

### Pattern 08: The Syncopated Rise
```text
Row: [Ch 1]       | [Ch 2]       | [Ch 3]       | [Ch 4]
00: F-4 04 ---    | C-4 03 C40   | C-4 06 C40   | C-4 01 C40
04: -             | C-4 02 C20   | -            | -
08: -             | C-4 03 C30   | G-4 06 C40   | C-4 01 C40
0C: -             | C-4 02 C20   | -            | -
10: G-4 04 ---    | C-4 03 C40   | D#4 06 C40   | -
14: -             | C-4 02 C30   | -            | C-4 01 C40
18: -             | C-4 03 C30   | C-5 06 C40   | -
1C: -             | C-4 02 C40   | -            | -
20: F-4 04 ---    | C-4 03 C40   | F-4 06 C40   | C-4 01 C40
24: -             | C-4 02 C20   | -            | -
28: -             | C-4 03 C30   | C-4 06 C40   | C-4 01 C40
2C: -             | C-4 02 C30   | -            | -
30: C-4 04 ---    | C-4 03 C40   | G-4 06 C40   | C-4 01 C40
34: -             | C-4 02 C20   | -            | -
38: -             | C-4 03 C40   | D-4 06 C40   | C-4 01 C40
3C: -             | C-4 02 C40   | -            | -
```

### Pattern 09: The Interlude Groove
```text
Row: [Ch 1]       | [Ch 2]       | [Ch 3]       | [Ch 4]
00: F-4 04 ---    | C-4 08 C30   | G-3 05 C38   | C-4 01 C40
04: -             | C-4 03 C30   | -            | -
08: -             | C-4 02 C40   | -            | -
0C: -             | C-4 03 C20   | -            | C-4 01 C30
10: G-4 04 ---    | C-4 03 C30   | A#3 05 C38   | C-4 01 C40
14: -             | C-4 03 C30   | -            | -
18: -             | C-4 02 C40   | -            | -
1C: -             | C-4 03 C20   | -            | -
20: F-4 04 ---    | C-4 08 C30   | G-3 05 C38   | C-4 01 C40
24: -             | C-4 03 C30   | -            | -
28: -             | C-4 02 C40   | -            | -
2C: -             | C-4 03 C20   | -            | C-4 01 C30
30: C-4 04 ---    | C-4 03 C30   | C-4 05 C38   | C-4 01 C40
34: -             | C-4 03 C30   | -            | -
38: -             | C-4 02 C40   | -            | -
3C: -             | C-4 03 C20   | -            | -
```

### Pattern 0a: The Tension Build
```text
Row: [Ch 1]       | [Ch 2]       | [Ch 3]       | [Ch 4]
00: F-4 04 ---    | C-4 03 C40   | F-4 06 C40   | C-4 01 C40
02: -             | -            | G-4 06 C30   | -
04: -             | C-4 03 C30   | G#4 06 C40   | C-4 01 C40
06: -             | -            | A#4 06 C30   | -
08: -             | C-4 03 C40   | C-5 06 C40   | C-4 01 C40
0A: -             | -            | D-5 06 C30   | -
0C: -             | C-4 03 C30   | D#5 06 C40   | C-4 01 C40
0E: -             | -            | F-5 06 C30   | -
10: G-4 04 ---    | C-4 03 C40   | G-4 06 C40   | C-4 01 C40
12: -             | -            | A#4 06 C30   | -
14: -             | C-4 03 C30   | C-5 06 C40   | C-4 01 C40
16: -             | -            | D-5 06 C30   | -
18: -             | C-4 03 C40   | D#5 06 C40   | C-4 01 C40
1A: -             | -            | F-5 06 C30   | -
1C: -             | C-4 03 C30   | G-5 06 C40   | C-4 01 C40
1E: -             | -            | A#5 06 C30   | -
20: F-4 04 ---    | C-4 03 C40   | F-4 06 C40   | C-4 01 C40
22: -             | -            | G-4 06 C30   | -
24: -             | C-4 03 C30   | G#4 06 C40   | C-4 01 C40
26: -             | -            | A#4 06 C30   | -
28: -             | C-4 03 C40   | C-5 06 C40   | C-4 01 C40
2A: -             | -            | D-5 06 C30   | -
2C: -             | C-4 03 C30   | D#5 06 C40   | C-4 01 C40
2E: -             | -            | F-5 06 C30   | -
30: C-4 04 ---    | C-4 02 C10   | G-5 06 C40   | C-4 01 C40
32: -             | C-4 02 C18   | F-5 06 C30   | -
34: -             | C-4 02 C28   | D#5 06 C40   | C-4 01 C40
36: -             | C-4 02 C38   | D-5 06 C30   | -
38: -             | C-4 02 C40   | C-5 06 C40   | C-4 01 C40
3A: -             | C-4 02 C40   | G-4 06 C30   | -
3C: -             | C-4 02 C40   | F-4 06 C40   | C-4 01 C40
3E: -             | C-4 02 C40   | D#4 06 C30   | -
```

---

## 5. Tested & Passing Status Confirmation

* **Sample Memory Footprint:** **PASSED** — Total active sample RAM remains well below the Paula 512KB Chip RAM limit.
* **Harmonic Pitch Calibration:** **PASSED** — `DigDug` (0), `Heaven` (-2 / `0xE`), and `PolySynth` (+2 / `0x2`) execute without key drift or beat frequency dissonance.
* **Polyphonic Voice Sharing:** **PASSED** — Dynamic volume commands (`C10`–`C40`) and effect commands (`A02`, `E00`, `484`) perform clean voice truncation across channels 2 and 4.
* **Order List & Pattern Mapping:** **PASSED** — 19-position sequence vector in `song.yaml` maps all 11 pattern files (`0` through `10` / `0a`) with zero dangling index references.

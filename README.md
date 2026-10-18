# Stolperbeats Visualiser v2

A visualiser and emulator of the MSM Stolperbeats eurorack module. See and hear exactly where its Timings put each hit, program its pattern banks, and try alt timing tables on your own module with the Firmware lab. Unofficial, for educational purposes only. See the [disclaimer](#disclaimer).

v2 is focused on the module only. The earlier page, with Deluge styles and proposed extras, stays at [stolperbeats_v1](https://github.com/thisisbribery/stolperbeats_v1).

## Using it

It's a single HTML file with no build step and no dependencies.

- **Online:** GitHub Pages, from the `main` branch root.
- **Locally:** open `index.html` in Chrome, Firefox, Safari or Edge.

Pick a Timing, turn the Shuffle control and press Play. Audio starts on your first click, because browsers block sound until you interact with the page.

## What's on the page

- **Timing, Feel, Linear and the 0 to 6 Shuffle control**, laid out like the module.
- **Six tracks** in the module's order: Kick, Snare, Hihat 1, Hihat 2, Perc 1, Perc 2. Click or drag to write your own beat; it's saved in your browser.
- **Four bars, like the module.** Kick and Snare run 4 bars (64 steps). The hats and percs loop 1 bar (16 steps) under them.
- **SKETCH and MODULE modes.** Play your own beats, or your pattern banks the way the module picks them.
- **Pattern banks.** Import, edit and download the module's `PatternBankNNN.txt` files.
- **Firmware lab.** Put alt tables on the Timing buttons of your own official firmware and flash it over USB.
- **15 preset beats**, **Hear straight**, and **808, 909 and 606 kits** synthesised in the browser.
- **A close-up** of half a bar, with the tick each step lands on and its offset in ms.
- **A timing creator** for making your own tables by hand.
- **Download MIDI** of all 4 bars, swing and all.

## Timings

### From the module (firmware 163)

| Timing | Feel |
|---|---|
| Trip | Uneven tuplet grooves where steps trip over each other |
| Shake | Long-short swing on every pair of 16ths |
| Push | Steps lean late, making room for each downbeat |
| Clave | 3:3:2 anchors hold while the other steps swing |

Every Timing runs 0 to 6 like the module's Shuffle, with 0 meaning straight 16ths.

**Changes while playing.** Like the module, a Shuffle or Timing change keeps the current beat as it was and takes over from the next beat. Pattern, Feel and tempo changes land straight away.

### Alt tables

Each alt table is held in the module's own row format, so you can hear it here and then put it on any Timing button with the Firmware lab.

| Table | What it does | On a real module |
|---|---|---|
| HOPP | MPC / Linn 16th swing in whole ticks (55.6% to 71.4%) | Not yet |
| DEEP | Two-level swing: the 8ths swing, then the 16ths inside them | Test builds 164 and 166 |
| SQEZ | Made in the creator: starts like CLSTR, then the & and a squeeze up against the next downbeat | Test build 166 |
| CLSTR | The e, & and a cluster mid-beat on a tuplet grid, leaning late as the level rises | Test build 165 |
| FOLD | The e and a of every beat fold in toward the & | Test build 164 |

Rules every table keeps: whole ticks, 16 to 36 ticks per beat in steps of 4 (so the Subdiv clock out stays even), every step at least 1 tick, and the half bar's 8 lengths adding up to 2N.

## Feels

From the module.

| Feel | What it does |
|---|---|
| Tight | All six tracks shuffle together |
| Rolls | Hihat 2 retriggers until the next step |
| Flam | Kick and Snare land one tick late |
| Slop | Like Flam, plus the hats a tick late where they hit with Kick or Snare |

## Four bars

The manual's Pattern Edit lengths: Kick and Snare are 4 x 16 = 64 steps, Hihat 1, Hihat 2, Perc 1 and Perc 2 are 16 steps.

- **Bar tabs 1 to 4** pick which bar the grid shows and edits. Each tab has a mini map of that bar's Kick (top row) and Snare (bottom row).
- **Follow** keeps the grid on the bar that's playing. Pick a tab while playing to stay on that bar and edit it while the loop runs.
- In bars 2 to 4 the hats and percs are dimmed and labelled *1-bar loop*: they're bar 1 repeating, so editing them there edits the one bar they share.
- **Copy bar N to all** copies the shown bar's Kick and Snare into the other three.
- Play always starts from bar 1. Linear, Slop and Rolls work bar by bar, since they depend on that bar's Kick and Snare.
- The presets repeat one bar of Kick and Snare four times. Beats saved before this change load the same way.

## SKETCH and MODULE

The switch above the grid picks what the grid plays.

- **SKETCH:** the presets and your own beat, as before.
- **MODULE:** your pattern banks, picked the way the module does it. A **Bank** picker, then one picker per track: **Kick**, **Snare**, **Hihat 1**, **Hihat 2**, **Perc 1** and **Perc 2**, each 1 to 24. Each track picks its own number, so Kick on 3 with Hihat 1 on 17 is normal. Click the arrows, scroll over the number, or focus it and use the arrow keys.
- In MODULE, edits on the grid go straight into the bank, like Pattern Edit on the module.
- Changes while playing land the way the module does it: bank and pattern picks, grid edits, Feel, Linear and tempo land straight away. Timing and Shuffle changes wait for the next beat, because the firmware only takes a new row at a beat.
- Switching back to SKETCH brings back whatever you had there.
- The page remembers your mode, bank and pattern numbers.

All six tracks pick their pattern separately, as on the hardware. Default until checked: Bank changes move every track at once and keep their numbers.

## Pattern banks

Program the module's pattern banks here and load them through its SD card. The **Pattern banks** panel under the grid starts closed; click it to open.

- **Import from SD** opens one or more `PatternBankNNN.txt` files. `PatternBank000.txt` is Bank 1. The bank number comes from the file name.
- **Bank chips** pick the bank. **File** renumbers it, **Remove** drops it from the browser.
- **Six rows of 24 tiles**, one row per track: Kick and Snare (each tile maps all 4 bars), then Hihat 1, Hihat 2, Perc 1 and Perc 2. Click a tile to put that track on that pattern, same as the MODULE pickers.
- **Send sketch to bank** (SKETCH mode) writes the beat on the grid into the bank at the numbers the rows show. **Tracks** picks which tracks it writes, so you can send just a new Kick. **Undo** reverses it.
- **New bank** starts an empty one on the first free number.
- **Download bank** saves the selected bank's file. **Download all** zips every bank.
- Banks stay in this browser until you remove them. No banks ship with the page.

### File format

Read from the module's own files. Six groups in this order: `KICK`, `SNARE`, `HIHAT1`, `HIHAT2`, `PERC1`, `PERC2`. Each has 24 lines, `PTN0` to `PTN23`:

```
KICK > PTN0: 1000000000000000, 1000000000000000, 1000000000000000, 1000000000000001;
HIHAT1 > PTN0: 1000100010001000;
```

Kick and Snare hold four 16-step bars separated by `, `. The others hold one. `1` is a hit. Windows line endings (CRLF), one blank line between groups, and a line ending after the last line. A full bank is 7462 bytes. The file stores hits only, no accents or velocity. Exports match the module's files byte for byte.

### Getting banks onto the module

1. Press Stop, then power off the rack. The module writes its data to the card when it stops, so never swap files while it's on.
2. Take out the SD card and back up every file on it.
3. Copy the downloaded PatternBank files into the same folder as the card's own, replacing any with the same name.
4. Put the card back and power on.
5. A bank number the module hasn't used yet starts switched off. Hold either Bank button for 2 seconds, turn the Kick encoder to the bank and click to switch it on.

## Firmware lab

Build your own experimental Stolperbeats firmware, then flash it, all in the page. The **Firmware lab** panel near the bottom starts closed.

This repo and page never contain firmware. You download the official file from [Making Sound Machines](https://makingsoundmachines.com/firmware/), the page changes it in your browser, and hands it back. For personal, educational experiments only.

1. **Open the .bin** (or drop it on the panel). The page checks it's an STM32 image, then finds the four Timing tables and the ticks-per-beat table by their factory values, never by fixed addresses. If anything doesn't match exactly once, it stops and changes nothing. Start from an unmodified official file.
2. **Pick your mods.** Each Timing button (Trip, Shake, Push, Clave) gets a menu: Factory, another factory table, an alt table (HOPP, DEEP, SQEZ, CLSTR, FOLD), or your own Timings from the CREATOR. **Hear it** plays the pick in the visualiser. A pick that breaks the module's rules is marked in orange and can't be built.
3. **Build** downloads the new file, named for what changed (e.g. `..._hw_rev4-163-mod-PushDEEP-ClaveSQEZ.bin`), with a list of every byte range changed and its SHA-256.
4. **Flash** over USB in Chrome or Edge: hold BOOT, press and release RESET, let go of BOOT, then **Connect** and **Flash my build**. The page erases only the sectors it needs, writes, reads everything back to check it byte for byte, then restarts the module. **Flash official file** puts the original back. Elsewhere, use `dfu-util` as the manual describes.

The STM32 bootloader lives in the chip's ROM, so a bad flash can always be undone by flashing the official file again.

**Recipes.** Save recipe writes a small `.json` of your picks (and the rows of any of your own Timings), with no firmware in it. Anyone can open it with their own official file and build the same firmware. Share recipes, not `.bin` files.

**What's been checked.** Opened on the official 163 file (SHA-256 `c04df924…`), the lab finds every table, and building Push = DEEP with Clave = SQEZ gives a file byte for byte identical to test build 166, which ran on a real module. The USB flashing is tested against a simulated bootloader; flashing a real module from the page hasn't been tried yet.

### Adding a mod

Mods live in `fwPatches()` in `index.html`. A mod is a list of byte writes. The rules:

- Find what you change by its known content, and require exactly one match. Never hard-code an address.
- Keep the module's own rules (for Timings: whole ticks, 16 to 36 ticks per beat in steps of 4, the half bar adds up to 2N). Check them before building, and throw if they fail.
- Never add firmware bytes to the repo. Values you search for should be small and documented, like the timing tables.

## Linear

From the module, next to the grid. When tracks clash on a step only the highest priority one plays: Snare beats Kick, both beat the hats and percs, open hat beats closed, Perc 2 beats Perc 1. Hats and percs don't silence each other. Silenced hits show as dashed outlines.

## Download tables

The button by the Timings saves the selected **alt table** as a zip: a README, the Stolperbeats-format rows, the step positions at 96 ticks per beat, and one-bar MIDI groove clips for Ableton Live (right-click a clip and choose *Extract Groove(s)*). It's off for the four factory Timings. No firmware is included.

## Download MIDI

The **Download MIDI** button above the grid saves all 4 bars exactly as they play, swing and all, so the groove survives in Ableton or any DAW even on a straight grid: every hit where the grid shows it, with the Timing, Shuffle, Feel and Rolls, accents as velocity, at the current tempo. Muted tracks and hits Linear silences are left out. It's four bars of GM drums on channel 10 (Kick 36, Snare 38, Hihat 1 42, Hihat 2 46, Perc 1 39, Perc 2 63) at 960 ticks per beat, so hits are placed to within 1/960 of a beat. The file name says what it is, e.g. `stolperbeats-Boom-bap-SQEZ-5-Tight-90-bpm.mid`.

## Creator

The **VISUALISER | CREATOR** switch next to Dark turns the Timing row into a table maker. The grid, kits, beats, Feels and playback all stay the same.

- **Start from** any Timing the module could hold as a table (Trip, Shake, Push, Clave, an alt table, or one of your own), or from straight.
- **Drag steps** 2 to 4 and 6 to 8 in the half-bar view while it plays. Steps 1 and 5 are pinned to the beat. Or click a step and use the arrow keys.
- **The Shuffle slider picks the level.** Level 0 is always straight. A level you haven't touched yet starts as a copy of the one before, and **Copy previous level** re-copies it.
- **Grid** sets the level's ticks per beat (16 to 36 in steps of 4). **Snap** moves by single ticks or by 4-tick slots (N/4 slots per beat, like Trip).
- **Beats:** *Every beat* makes beat 2 copy beat 1 (like Shake, Push, DEEP and CLSTR). *Beat 1 ≠ 2* edits all 8 steps of the half bar (like Trip and Clave).
- The table under the half bar shows all 7 rows exactly as the firmware holds them: ticks per beat and 16 step lengths.

Every Timing made here keeps to the module's rules: whole ticks, 16 to 36 ticks per beat in steps of 4, every step at least 1 tick, and the half bar's 8 lengths adding up to 2N. The badge turns amber for things that are allowed but worth knowing: 1-tick steps (2 is the shortest tested on hardware), step 5 off the beat (factory Clave does this), and the Rolls buzz at level 3 on grids above 20.

- **Save to visualiser** adds it to the alt tables, with a teal light. Saved Timings stay in this browser only.
- **Export** downloads `NAME.timing.json`: the 7 rows in the same `stolperbeatsRows` format Download tables uses.
- **Import** loads a `.timing.json`, or a style's JSON from Download tables, back into the creator.

## How accurate is it

**Read from firmware 163:**
- Ticks per beat for each Shuffle setting, and the step-length table for each Timing.
- How steps are placed: each fires at the running total of the step lengths before it, and a tick is 1/N of a beat.
- Flam, Slop, Rolls and Linear, as described above.
- Shuffle and Timing changes waiting for the next beat.

**Confirmed on a real module:** test builds with DEEP, FOLD, CLSTR and SQEZ swapped into the Push and Clave tables played as the page shows, by ear. That also confirms the Push and Clave buttons play those two tables. Nothing has been measured with instruments.

**Matched, not traced or measured:**
- Feel colours, from the manual.
- Trip and Shake's buttons, from the manual's button order.
- How the Feels appear on MIDI out.
- The preset beats are examples, not the module's pattern banks, and the kits are approximations.

## Disclaimer

This is an unofficial, independent project made for education. It is not affiliated with, endorsed by, or supported by Making Sound Machines.

Stolperbeats is designed and made by [Making Sound Machines](https://makingsoundmachines.com/stolperbeats/), and all rights in the module, its firmware and its documentation remain theirs. The small set of timing values used here was read from publicly available firmware purely to illustrate how the shuffle behaves. No firmware is included in or distributed by this repository.

The alt tables are not part of Stolperbeats.

For official information, use the [Stolperbeats manual](https://makingsoundmachines.com/stolperbeats/) and Making Sound Machines' own support channels.

## Credits

- Stolperbeats and its Trip, Shake, Push and Clave timings are by Making Sound Machines.
- The 808, 909 and 606 names refer to the classic drum machines whose character the kits loosely imitate. The trademarks belong to their owners.

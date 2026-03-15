# Form Sandbox Port Report

Generated on March 14, 2026.

## Sandbox Output

- Sandbox repo: `C:\Users\BrettWiggins\Documents\Playground\sandbox\zmk-config-form-adv360-sandbox`
- Main keymap: `config/stp.keymap`
- Build workflow updated from current Kinesis upstream: `.github/workflows/build.yml`

## Core Layout Decisions

- `Esc` and `` ` `` are swapped:
  - top-left key is now `` ` ``
  - `Esc` is now on the number row next to `1`
- The default top row is now much closer to your actual 360 behavior instead of a generic productivity strip.
- The keyboard still cycles through three persistent top-row modes:
  1. `360`
  2. `Fn`
  3. `Media`

## Fn Key Behavior

The physical `Fn` key still controls the row modes.

- tap: return to `360`
- hold: advance to the next mode

Cycle order:

- `360` -> `Fn`
- `Fn` -> `Media`
- `Media` -> `360`

## 360 Default Row

The default `360` top row is now wired like this:

- top-left key: `` ` ``
- `F1`: 360-style hold/tap launch key
  - tap = `Ctrl+Alt+1`
  - hold = `Ctrl+Alt+2`
- `F2`: 360 `RPN` tap dance
- `F3`: 360 copy/select/paste/cut tap dance
- `F4`: empty
- `F5`: plain `Backspace`
- `F6`: plain `Delete`
- `F11`: `-`
- `F12`: `=`
- extra top-right key: `Backspace`

## Bottom Row Changes

Left-hand bottom row is now:

- leftmost: tap `Alt`, double tap `Windows`
- next key: toggle `CAD` layer
- next key: `Ctrl`

Right-hand bottom row is still conservative:

- `Ctrl`
- row-mode key
- `Alt`
- arrows stay where they were

## Space And Shift Behavior

- Left space:
  - tap = `Space`
  - hold = `Shift`
  - double tap = `Caps Word`
  - triple tap = `Caps Lock`
- Right space:
  - tap = `Space`
  - hold = `Shift`
  - double tap = `Home`
  - double tap + hold = `End`
- Both physical shift keys are now momentary numpad-layer keys.

## Numpad And CAD Layers

### Numpad

- `Caps` toggles the numpad layer.
- Both shift keys also momentarily access that same numpad layer.
- Left-hand numpad grid remains:
  - `W E R` -> `7 8 9`
  - `S D F` -> `4 5 6`
  - `X C V` -> `1 2 3`
  - bottom-left third key -> `0`

### CAD

The CAD layer is toggled from the second bottom-left key and carries:

- `W` -> `MID`
- `E` -> `END`
- `S` -> `FRO`
- `D` -> `M2P`
- `X` -> `.X`
- `C` -> `.Y`

## Behaviors Ported From The 360

- `RPN` tap dance
- 360 copy/select/paste/cut tap dance
- AutoCAD command macros:
  - `FRO`
  - `M2P`
  - `MID`
  - `END`
  - `.X`
  - `.Y`

## Assumptions I Made

- I kept the row-mode key on the physical `Fn` position even though you also like `Menu` on the right bottom cluster. Your earlier mode-cycling requirement was more specific, so I treated that as the higher-priority behavior.
- I used plain `Delete` for `F6` and removed the word-delete behavior from that slot because you called out that it was not working well for you.
- I left the right-hand bottom cluster mostly stable so the board does not become too foreign all at once.

## Upstream Kinesis Check

I compared your local form repo against the cached upstream remote `KinesisCorporation/zmk-config-form`.

- Your local/fork head: `902874b` (`Updated stp.keymap`)
- Upstream main head: `0d90a38` (`Downgrade docker image`)
- Upstream branch also present: `upstream/mouse` at `cee264f`

What changed upstream after your fork:

- `.github/workflows/build.yml` switched the build container from `zmkfirmware/zmk-build-arm:stable` to `zmkfirmware/zmk-build-arm:3.5`
- `config/stp.keymap` was cleaned up a bit
- no meaningful stock layout or feature changes landed in `main`

Bottom line: I did not find major stock functionality improvements on `main` since your copy. The only practical upstream improvement worth carrying forward into the sandbox was the pinned build image, and I applied that.

## Recommended First Real-World Test

1. Confirm the `Esc` / grave swap feels right.
2. Test `F1`, `F2`, and `F3` first, because they carry the most custom behavior.
3. Test left and right spaces separately:
   - left for caps word / caps lock
   - right for home / end
4. Hold either shift key and make sure the numpad layer appears the way you expect.
5. Toggle the CAD layer and check `MID`, `END`, `FRO`, `M2P`, `.X`, and `.Y`.

# tree-rf

Control a pre-lit Balsam Hill / Polygroup Christmas tree from Apple Home by
emulating its 433 MHz RF remote with an ESP32 and ESPHome.

Nothing on the tree is cut or modified. The ESP32 just sends the same radio
frames the handheld remote does.

## Status

- [ ] Transmitter wired
- [ ] `Test Off` confirmed on the tree (proves the protocol matches)
- [ ] All effects mapped (see `docs/protocol.md`)
- [ ] Named buttons added for each effect
- [ ] Exposed to Apple Home

The protocol in this repo comes from two write-ups on a sibling Polygroup
remote (CW003). The remote for this tree is a PST03-14 (FCC ID
2A62O-PDT015TS). It has not been verified yet, and the config has not been
compiled yet.

## Quick start

1. Wire the transmitter. See `docs/wiring.md`.
2. `cp secrets.yaml.example secrets.yaml` and fill in Wi-Fi.
3. Flash: `esphome run xmas-tree.yaml`
4. Open the device web page or Home Assistant and press **Test Off**.
   - Tree turns off: same protocol. Go to step 5.
   - Nothing: capture the real remote. See the fallback in `docs/protocol.md`.
5. Sweep. Set **Sweep Command** to 0, press **Send Sweep Command**, note what
   the tree does in `docs/protocol.md`, then step through the values.
6. Replace the test buttons with one named button per effect.

## Apple Home

Two routes:

- **Home Assistant**: add the ESPHome device, then expose the buttons through
  the HomeKit Bridge integration. Effects show up as switches.
- **No hub**: port the frame builder to HomeSpan (Arduino). Not in this repo
  yet.

Commands are one-way. The ESP32 does not know the tree's real state if someone
uses the handheld remote or foot pedal.

## Files

| File | What |
|---|---|
| `xmas-tree.yaml` | ESPHome config: frame builder, test buttons, sweep |
| `secrets.yaml.example` | Wi-Fi secrets template |
| `docs/protocol.md` | Protocol notes and the command map to fill in |
| `docs/wiring.md` | Parts, wiring, pin notes |

## Later

Replacing the stock controller with an ESP32 and H-bridge would give full
control of the two-polarity LED strings (custom effects, real state). That is
an off-season job with the tree down, and it voids the warranty.

## Credits

Protocol work by zerowidth.com and Dave Corder. Links in `docs/protocol.md`.

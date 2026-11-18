# RF protocol notes

Status: **unverified on the PST03-14 remote.** Everything below was decoded by
others on the sibling Polygroup CW003 remote. The first job is confirming it
applies here.

## Remote

| Field | Value |
|---|---|
| Maker | Polygroup |
| Model / HVIN | PST03-14 |
| FCC ID | 2A62O-PDT015TS |
| IC | 28592-PDT015TS |
| Battery | CR2032 |
| Tree | Tree Classics by Balsam Hill 9 ft Classic Fraser Fir, model TG90P4368D10, Lowe's item 6023528 |

Buttons on the label: Combo, Clear Steady, Color Steady, Clear Twinkle,
Color Twinkle, Clear Fade, Color Fade, Clear/Color Alt, Clear/Color Fast Blink,
Clear/Color Slow Blink, Clear/Color Fade, Brightness, Timer, On/Off.

## Reference protocol (CW003 remote, FCC ID 2A62O-CW003 / 2APJZ-CW003)

- 433.92 MHz, OOK/ASK
- Sync: 11450 us high, 5275 us low
- Bit: 1100 us high, then a gap. 3100 us gap = 1, 1100 us gap = 0
- Frame: 32 bits, MSB first: `FF 0F CMD ~CMD`
- Tail: 1100 us high, 11450 us low
- Frame sent 6 times back to back

| Button | CMD | Frame |
|---|---|---|
| Dimmer | 0x00 | ff0f00ff |
| Brighter | 0x01 | ff0f01fe |
| Off | 0x02 | ff0f02fd |
| Color | 0x03 | ff0f03fc |
| Clear | 0x04 | ff0f04fb |
| Color + Clear | 0x05 | ff0f05fa |

## Command map for this tree

Fill in while sweeping. Leave blank if nothing happens.

| CMD | Effect on tree | Matches remote button |
|---|---|---|
| 0x00 | | |
| 0x01 | | |
| 0x02 | | |
| 0x03 | | |
| 0x04 | | |
| 0x05 | | |
| 0x06 | | |
| 0x07 | | |
| 0x08 | | |
| 0x09 | | |
| 0x0A | | |
| 0x0B | | |
| 0x0C | | |
| 0x0D | | |
| 0x0E | | |
| 0x0F | | |

## If the reference protocol does not work

Capture the real remote with an RTL-SDR:

```
rtl_433 -f 433.92M -A
rtl_433 -f 433.92M -X "n=tree,m=OOK_PPM,short=1100,long=3100,reset=11450,gap=5270"
```

Record sync, bit timings, frame length, and one frame per button here, then
update the lambda in `xmas-tree.yaml`.

## Sources

- https://zerowidth.com/2025/reverse-engineering-my-christmas-tree/
- https://www.davecorder.org/blog/automating-a-balsam-hill-artificial-tree/

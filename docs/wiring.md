# Hardware and wiring

## Parts

- ESP32-S3-DevKitC-1-N16R8
- STX882 433 MHz ASK transmitter with spring antenna (kit also includes an
  SRX882 receiver, not needed for transmit)
- 3 female-to-female jumper wires
- USB-C cable and 5 V USB supply

## Wiring

| STX882 | ESP32-S3 |
|---|---|
| DATA | GPIO4 |
| VCC | 5V |
| GND | GND |
| ANT | spring antenna (solder) |

5 V on VCC gives the most transmit power. DATA is fine at 3.3 V logic.

## Pins to avoid on the N16R8

- GPIO35, 36, 37: used by octal PSRAM
- GPIO0, 3, 45, 46: strapping pins
- GPIO19, 20: USB

## Optional: receive path

To capture the remote with the SRX882: DATA to GPIO5, VCC to 3V3, GND to GND,
and tie the CS pin high to enable the module. Powering it from 3V3 keeps the
DATA output safe for the ESP32.

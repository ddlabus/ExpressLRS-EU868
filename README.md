# ExpressLRS 4.0 for E32-900M30S (EU868 1W)

Custom ELRS firmware for E32-900M30S module (SX1276, 1W output).

## Hardware
- **RX:** ESP-01F (ESP8285) + E32-900M30S
- **TX:** ESP32-WROOM-32E + E32-900M30S

## Frequency
- Band: EU868 (863-870MHz)

## Download
See [Releases](https://github.com/ddlabus/ExpressLRS-EU868/releases) for compiled firmware.

## Files
| File | Description |
|------|-------------|
| `ELRS_4.0_RX_ESP8285_EU868.bin` | Receiver firmware |
| `ELRS_4.0_TX_ESP32_EU868.bin` | Transmitter firmware |
| `E32-900M30S_RX.json` | RX hardware layout |
| `E32-900M30S_TX.json` | TX hardware layout |

## Flashing
Use [esptool](https://github.com/espressif/esptool) or ELRS Configurator.

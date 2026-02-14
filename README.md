# ExpressLRS for E32-900M30S (EU868 1W)

Custom ELRS firmware for E32-900M30S module (SX1276, 1W output).

![E32-900M30S Module](https://www.cdebyte.com/u_file/2010/photo/7ba4b2da2f.png)

## Hardware

### Receiver (RX)
- **MCU:** ESP-01F (ESP8285)
- **Radio:** E32-900M30S (SX1276, 30dBm/1W)

![ESP-01F](https://www.cdebyte.com/u_file/2212/photo/4b67b3f116.png)

### Transmitter (TX)
- **MCU:** ESP32-WROOM-32E
- **Radio:** E32-900M30S (SX1276, 30dBm/1W)

## Frequency
- Band: EU868 (863-870MHz)

---

## Wiring Diagrams

### RX: ESP-01F + E32-900M30S

```
ESP-01F (ESP8285)          E32-900M30S
┌─────────────────┐        ┌─────────────────┐
│ GPIO3 (RX) ─────┼────────┼─ TX (to FC)     │
│ GPIO1 (TX) ─────┼────────┼─ RX (from FC)   │
│ GPIO4  ─────────┼────────┼─ DIO0           │
│ GPIO5  ─────────┼────────┼─ DIO1           │
│ GPIO12 ─────────┼────────┼─ MISO           │
│ GPIO13 ─────────┼────────┼─ MOSI           │
│ GPIO14 ─────────┼────────┼─ SCK            │
│ GPIO15 ─────────┼────────┼─ NSS            │
│ GPIO0  ─────────┼────────┼─ RXEN           │
│ GPIO2  ─────────┼────────┼─ TXEN           │
│ GPIO16 ─────────┼────────┼─ LED (optional) │
│ 3V3    ─────────┼────────┼─ VCC (3.3V)     │
│ GND    ─────────┼────────┼─ GND            │
└─────────────────┘        └─────────────────┘
```

| ESP-01F Pin | E32-900M30S Pin | Function |
|-------------|-----------------|----------|
| GPIO4 | DIO0 | Radio interrupt |
| GPIO5 | DIO1 | Radio interrupt |
| GPIO12 | MISO | SPI data in |
| GPIO13 | MOSI | SPI data out |
| GPIO14 | SCK | SPI clock |
| GPIO15 | NSS | SPI chip select |
| GPIO0 | RXEN | PA RX enable |
| GPIO2 | TXEN | PA TX enable |

### TX: ESP32-WROOM-32E + E32-900M30S

```
ESP32-WROOM-32E            E32-900M30S
┌─────────────────┐        ┌─────────────────┐
│ GPIO26 ─────────┼────────┼─ DIO0           │
│ GPIO25 ─────────┼────────┼─ DIO1           │
│ GPIO19 ─────────┼────────┼─ MISO           │
│ GPIO23 ─────────┼────────┼─ MOSI           │
│ GPIO18 ─────────┼────────┼─ SCK            │
│ GPIO5  ─────────┼────────┼─ NSS            │
│ GPIO14 ─────────┼────────┼─ RST            │
│ GPIO13 ─────────┼────────┼─ RXEN           │
│ GPIO12 ─────────┼────────┼─ TXEN           │
│ GPIO22 ─────────┼────────┼─ LED            │
│ 3V3    ─────────┼────────┼─ VCC (3.3V)     │
│ GND    ─────────┼────────┼─ GND            │
└─────────────────┘        └─────────────────┘
```

---

## Flashing Firmware on Virgin ESP

### Requirements
- USB-TTL adapter (CH340, CP2102, FT232)
- `pip install esptool`

### RX (ESP-01F)
```
USB-TTL → ESP-01F: TX→GPIO3, RX→GPIO1, 3V3→VCC+EN, GND→GND+GPIO0+GPIO15
```
```bash
esptool.py --port /dev/ttyUSB0 --baud 460800 write_flash 0x0 ELRS_*_RX_ESP8285_EU868.bin
```

### TX (ESP32)
```
USB-TTL → ESP32: TX→GPIO3, RX→GPIO1, 3V3→3V3, GND→GND+GPIO0
```
```bash
esptool.py --port /dev/ttyUSB0 --baud 460800 --chip esp32 write_flash 0x0 ELRS_*_TX_ESP32_EU868.bin
```

### After Flashing
1. Disconnect GPIO0 from GND, power cycle
2. Connect to WiFi: `ExpressLRS RX/TX`
3. Configure at `10.0.0.1`

---

## Download
See [Releases](https://github.com/ddlabus/ExpressLRS-EU868/releases)

## Links
- [E32-900M30S Datasheet](https://www.cdebyte.com/products/E32-900M30S)
- [ExpressLRS Documentation](https://www.expresslrs.org/)

# Elevator Security Control System

A hardware design project for a secure elevator access system using multi-level authentication — **RFID, fingerprint, and capacitive keypad** — controlled by an **STM32G070CBT6 microcontroller**. The deliverable is a complete schematic and double-layer PCB design created in EasyEDA.

---

## 🔒 Overview

The system restricts elevator access to authenticated users only. Authentication follows a layered flow: RFID card scan → optional fingerprint or keypad verification → floor selection via touch keypad. Visual feedback is provided through a 7-segment display and 16 LEDs controlled via a shift register to minimize GPIO usage. A DC-DC converter handles the 24V to 5V step-down for the entire system.

---

## ✨ Key Features

- Multi-level authentication: RFID + fingerprint + capacitive keypad
- 16-channel touch keypad (TTP229) for floor selection
- 7-segment display for current/selected floor indication
- 74HC595 shift register to drive 16 LEDs with only 3 MCU pins
- W25Q128 serial flash for storing user credentials and access logs
- MC34063A DC-DC converter stepping 24V → 5V
- Double-layer PCB with modular section layout for clean signal routing

---

## 🔧 Components

| Component | Part Number | Purpose |
|---|---|---|
| Microcontroller | STM32G070CBT6 | Core processing and peripheral control |
| RFID Reader | RC522 | 13.56 MHz card scanning (ISO 14443A) |
| Fingerprint Sensor | ZW101 | Optical fingerprint capture and matching |
| Touch Keypad | TTP229 | 16-key capacitive input for floor selection |
| Shift Register | 74HC595 | Expand GPIO — drive 16 LEDs with 3 pins |
| Serial Flash | W25Q128 | 16MB non-volatile storage for user data |
| 7-Segment Display | — | Floor number display |
| DC-DC Converter | MC34063A | Step down 24V → regulated 5V |

### STM32G070CBT6 — Key Specs
- ARM Cortex-M0+, up to 64 MHz
- 128 KB Flash, 36 KB SRAM
- 2× I²C, 2× SPI, 4× USART
- 12-bit ADC, PWM timers
- 2.0V to 3.6V supply voltage

### RC522 RFID — Key Specs
- Operating frequency: 13.56 MHz
- Tag memory: 1 KB
- Interface: SPI
- Compatible with ISO 14443A tags (read & write)

### ZW101 Fingerprint Module — Key Specs
- Interface: UART
- Built-in optical sensor and matching processor
- Stores fingerprint templates internally

### W25Q128 Flash — Key Specs
- Capacity: 128 Mbit (16 MB)
- Interface: SPI (up to 104 MHz)
- 100,000 erase cycles per sector, >20 years data retention

---

## 🔐 Authentication Flow

```
User Approaches Elevator
        │
        ▼
  RFID Card Scan (RC522)
        │
        ├─ Not Recognized → Access Denied
        │
        └─ Recognized
                │
                ▼
   Fingerprint / Keypad Verification (ZW101 / TTP229)
                │
                ├─ Failed → Access Denied
                │
                └─ Verified
                        │
                        ▼
            Floor Selection via Touch Keypad
                        │
                        ▼
             Relay Triggered → Elevator Moves
```

---

## 🗂️ Repository Structure

```
elevator-security-control-system/
│
├── hardware/
│   ├── schematic.pdf              # Full schematic (EasyEDA export)
│   ├── pcb_design.pdf             # PCB layout (EasyEDA export)
│   └── gerber/                    # Gerber files ready for manufacturing
│       └── *.gbr
│
├── docs/
│   ├── pcb_front_back.png         # 2D front and back PCB render
│   └── bom.csv                    # Bill of Materials
│
├── .gitignore
└── README.md
```

---

## 🖥️ PCB Design Notes

Designed in **EasyEDA** as a double-layer board following this process:

1. **Schematic Creation** — All components and sub-circuits mapped out in four sections: Shift Register Circuit, Touch Button Circuit, Microcontroller Circuit, Voltage Converter Circuit, and Serial Flash Memory
2. **Footprint Assignment** — SMD packages selected to minimize board area
3. **Routing** — Short direct traces, decoupling capacitors placed close to IC power pins to reduce voltage ripple
4. **Component Grouping** — Each functional block assigned its own PCB region to simplify debugging and testing
5. **DRC & ERC Check** — Design verified for electrical and layout errors
6. **Gerber Export** — Files finalized and ready for manufacturing

---

## 🛠️ Built With

- [EasyEDA](https://easyeda.com/) — Schematic and PCB design
- [STM32G070CBT6 Datasheet](https://www.st.com/en/microcontrollers-microprocessors/stm32g070cb.html)
- [MFRC522 Datasheet](https://www.nxp.com/docs/en/data-sheet/MFRC522.pdf)
- [W25Q128 Datasheet](https://www.winbond.com/resource-files/w25q128jv%20spi%20revc%2011162016.pdf)

---

## 🔮 Future Scope

- Firmware development for STM32 to implement the full authentication logic
- Cloud connectivity for remote access control and audit logging
- Real-time elevator status reporting via wireless interface

---

## 👤 Author

**Arya Sureshbhai Patel**  

# RFID-Based Door Lock System with TFT Display

This project is an **RFID-based door lock system** using an **Arduino Uno R3**, **MFRC522 RFID module**, **SG90 servo motor**, and **ST7735 TFT display**. When a registered RFID card is detected, the system grants access, moves the servo to unlock the door, and displays an "Access Granted" message on the TFT. If an unrecognized card is scanned, access is denied.

## Components & Pin Connections

### **1. Arduino Uno R3 Pinouts:**
| **Component** | **Pin** | **Arduino Pin** |
|-------------|---------|---------------|
| **TFT Display (ST7735)** | CS | 7 |
| | DC | 6 |
| | RST | 5 |
| **RFID Module (MFRC522)** | CS | 10 |
| | RST | 9 |
| **Servo Motor (SG90)** | Signal | 3 |

### **2. SPI Pins (Arduino Uno Default SPI Bus)**
| **Signal** | **Arduino Pin** |
|-----------|----------------|
| MOSI | 11 |
| MISO | 12 |
| SCK | 13 |

## Libraries Used

The following libraries are required for this project. Install them via the Arduino Library Manager:
- **SPI.h** → Handles SPI communication
- **Adafruit_GFX.h** → Graphics library for TFT display
- **Adafruit_ST7735.h** → TFT display driver
- **MFRC522.h** → RFID module driver
- **Servo.h** → Controls the SG90 servo motor

## How It Works
1. The system starts with the TFT display showing **"Place the Card"** with a smiley face.
2. When an RFID card is scanned:
   - If the card's **UID matches** a stored UID, the door unlocks, and "Access Granted" appears on the TFT.
   - If the card **does not match**, "Access Denied" is displayed.
3. The servo motor moves **90° counterclockwise** to unlock the door and **returns to its original position** after 5 seconds.
4. The system resets and waits for another card scan.

## Code Highlights
- **Preventing Floating Pins:** All TFT, RFID, and Servo data pins are initialized to `LOW` to prevent unintended behavior.
- **SPI Management:** The RFID module and TFT display share SPI pins. The `CS` (Chip Select) pin is toggled to switch between devices.
- **Performance Optimization:** The TFT refresh rate is improved using `tft.setSPISpeed(4000000);` (optional for stability).
- **Expandability:** More RFID cards can be added by updating the `allowedUIDs` array.

## Setup & Uploading Code
1. **Connect all components** as per the pinout table above.
2. **Install required libraries** from Arduino Library Manager.
3. **Upload the code** to Arduino Uno using the Arduino IDE.
4. **Test the system** by scanning an RFID card.

## Troubleshooting
- **No display on TFT?**
  - Check wiring connections, especially CS, DC, and RST pins.
  - Ensure `tft.setRotation(1);` is set correctly for your display.
- **RFID not detecting cards?**
  - Verify SPI connections (MOSI, MISO, SCK, CS).
  - Make sure the correct RFID module library is installed.
- **Servo not moving?**
  - Ensure the servo pin is connected properly.
  - Try `doorServo.attach(SERVO_PIN);` inside `loop()` temporarily to debug.

## Future Improvements
- Add **EEPROM storage** for dynamic card management.
- Integrate a **buzzer** for audible feedback.
- Use **WiFi (ESP8266/ESP32)** for remote access logging.

---
### **Shinya Kogami**
Project designed for **Arduino Uno R3** 🚀



# 📘 Voice-Controlled Robotic Arm using ESP32 and State Pattern

## 📌 Project Overview

This side project demonstrates a **voice-controlled robotic arm system** built with an **ESP32** microcontroller. By utilizing **state pattern programming**, the system translates different voice commands into corresponding robotic arm actions such as turning, lifting, and paw control.

It integrates **GPIO input reading**, **UART serial communication**, and **structured object-oriented design** to enable real-time control of a physical robotic arm.

---

## 🔧 Hardware Components

| Component           | Description / Model                |
|--------------------|------------------------------------|
| Microcontroller     | ESP32 DevKit (e.g., ESP32-WROOM)   |
| Voice Module        | [e.g., LD3320 / DFRobot Speech Module] *(please fill)* |
| Robotic Arm         | [e.g., DIY 4-DOF arm kit with servo motors] *(please fill)* |
| Serial Interface    | UART (TX: 17, RX: 16)              |
| Power Source        | USB / External 5V Supply           |

> ✅ *Note: The robotic arm accepts a specific 25-byte command structure via UART.*

---

## 🧠 System Architecture

```
[Voice Command Input]
        ↓
[ESP32 GPIO Detection]
        ↓
[State Pattern: Init / Left / Right / Up / Down / Open / Close]
        ↓
[Command Assembly (25-byte)]
        ↓
[Serial2 UART Transmission]
        ↓
[Robotic Arm Action Execution]
```

---

## 💡 Features

- 🎙️ Voice-controlled input via GPIO (8 digital commands)
- 🤖 Multiple states: Init, Left, Right, Up, Down, Open Paw, Close Paw
- 📦 Object-oriented design using abstract `State` class and its extensions
- 🔁 Real-time command generation and UART-based delivery
- 🧩 Easily extensible architecture for future arm functions

---

## 🧑‍💻 Project Structure

```
project_root/
├── main.cpp           // Main execution loop and voice command polling
├── State.h            // Abstract State class + Init / Left / Right implementations
├── Controller.h       // Control interface wrapping state behavior
```

---

## 🚀 How to Run

1. **Setup Arduino IDE:**
   - Install ESP32 board via Board Manager
   - Select correct board (e.g., ESP32 Dev Module)
   - Select proper COM port

2. **Wiring:**
   - Connect 8 GPIO pins to the voice module output (pins 15~8 used)
   - Connect TX (ESP32 GPIO17) → Robotic arm RX
   - Connect RX (ESP32 GPIO16) ← Robotic arm TX *(optional)*

3. **Upload Code:**
   - Open `main.cpp` and upload to ESP32

4. **Open Serial Monitor:**
   - Set baud rate: `9600`
   - Observe state transitions and command feedback

---

## 📷 Example Output (Serial)

```
X0=1、X1=0、X2=0、X3=0、X4=0、X5=0、X6=0、
State: Init
```

> When a GPIO input is high (e.g., X0), the corresponding state is activated.

---

## 🧩 State Pattern Explained

Each state inherits from the abstract `State` class and implements its own `doAction()` method:

```cpp
class Init : public State {
    char ary[25] = {0x55, 0x55, ...};
    void doAction(int del_num) override {
        // Compose and transmit command via Serial2
    }
};
```

The `Controller` class acts as an interface to invoke actions on the current state:

```cpp
ctr->doAction(state, 3000);   // e.g., Init / Left / Right
ctr->Up(state, 3000);         // Additional movement
```

---

## 💡 Future Improvements

- ✅ Add button-based fallback in case voice module fails
- ✅ Visualize current state on OLED / LCD screen
- ✅ Integrate with Wi-Fi or Bluetooth for remote control
- ✅ Support more servo degrees and interpolation

---

## 📚 Skills Demonstrated

- C++ OOP with State Design Pattern
- Embedded system I/O (GPIO, Serial2)
- UART protocol and byte-level command encoding
- Real-time voice-controlled decision logic
- System modularity and expandability

---

## 📎 License

MIT License — for educational and demonstration purposes.

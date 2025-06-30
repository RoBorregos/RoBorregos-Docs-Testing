## 📡 Electronics System Overview

The electronics system is based on a custom-designed PCB that integrates all sensors, actuators, and controllers required for autonomous navigation in the RoboCupJunior Rescue Maze 2025 environment.

---

### 🔌 **Electronic Design and Manufacturing**

| Component         | Description |
|------------------|-------------|
| **Controller**    | ESP32 microcontroller + Jetson Nano |
| **Sensors**       | - 6x VL53L0X (3 front, 1 rear, 2 sides) for wall detection<br>- BNO055 IMU for orientation and ramp detection<br>- TCS34725 color sensor for tile detection<br>- Wheel encoders for velocity measurement<br>- 2x LMX219 cameras for victim detection |
| **Power System**  | 11.1V LiPo battery regulated to:<br>- 5V (ESP32)<br>- 3.3V (logic)<br>- 6V (motors) |
| **Actuators**     | - SG90 micro servo (kit deployment)<br>- Pololu gear motors with TB6612FNG motor drivers |
| **Others**        | - SSD1306 OLED display for debugging<br>- WS2812 RGB LEDs for victim signaling<br>- Push button for manual reset/start |
| **Communication** | TCA9548A I2C multiplexer to manage multiple I2C devices |

---

### ⚙️ **System Functionality**

- **Distance Measurement**: VL53L0X sensors detect nearby walls and help the robot center itself on the tiles and detect ramps.
- **Victim Detection**: Jetson Nano processes images from LMX219 cameras and uses WS2812 LEDs for standardized blinking, as required by [RCJ rules 2025](https://junior.robocup.org/robocupjunior-general-rules/).
- **Tile Identification**: The TCS34725 color sensor recognizes checkpoints (silver), blue tiles (puddles), and black tiles (holes).
- **Motor Feedback**: Pololu motors with encoders provide real-time velocity data to the ESP32.
- **Orientation**: BNO055 ensures accurate 90° turns and detects slopes.
- **I2C Expansion**: The TCA9548A allows communication with multiple I2C devices without address conflict.
- **User Interface**: SSD1306 OLED screen displays debug info, and a push button is used for start/reset operations.

---
### Schematic and PCB design
![Conections diagram](docs/assets/Conexion.PNG)
![Schematic](docs/assets/Schematic_maze_2025.PNG)
![Top View of PCB](docs/assets/PCB_maze_2025.PNG)

---

### 🛠️ Notes

- All sensors and actuators were tested to comply with the environmental tolerance requirements specified in the [RCJ Rescue Maze Rules 2025 PDF](RCJRescueMaze2025-final-1.pdf).
- The ESP32 handles low-level control and sensor polling, while the Jetson Nano is dedicated to computer vision processing.

---



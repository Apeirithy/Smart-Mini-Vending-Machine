# Smart Mini Vending Machine for Electrical Components

A microcontroller-based embedded system designed to automatically distribute small electronic components. Built from scratch including custom PCB design, C-based bare-metal firmware (AVR-GCC), and 3D-modeled mechanical enclosures.

## Project Demonstration
* **Live Demo & Explanation:** https://youtu.be/EqsmP9JuczM

## System Architecture & Hardware
The system acts as a fully functional automated dispenser operated by coin insertion.
* **Microcontroller:** Arduino Nano (ATmega328P) acting as the main control unit.
* **Motor Control:** Dual DRV8833 Motor Drivers controlling 4 independent DC motors for product dispensing.
* **Sensors:** 
  * IR Optocoupler (Speed Sensor) for accurate coin insertion detection.
  * IR Obstacle Avoidance Sensors serving as drop detectors to verify successful product dispensation.
* **I/O Management:** Utilized PCF8574 I2C expansion board to manage push-button inputs, saving precious microcontroller pins.
* **Custom PCB:** The entire circuit was routed and engraved on a custom single-layer PCB using EasyEDA, replacing unreliable jumper wires.

> **View Hardware Schematic:** [Click here to view the EasyEDA Schematic](./Hardware_Schematics/Schematic_Vending_Machine.png)

## Mechanical & Enclosure Design
The physical chassis and dispensing mechanism were custom-designed to fit the specific needs of electrical components:
* **Enclosure:** Modeled in Tinkercad and fabricated using 5mm acrylic via laser cutting for a precise and professional finish.
* **Dispensing Mechanism:** Custom 3D-printed spiral pushers (coils) directly coupled to the DC motors.

> **View 3D Layout:** [Click here to view the Tinkercad Layout](./3D_Mechanical_Design/3D_Design_Part.stl)

## Firmware Logic (Finite State Machine)
The firmware is written in pure C (AVR-GCC) and relies on a robust Finite State Machine (FSM) to prevent conflicting operations.
1. **STATE_IDLE:** System awaits a hardware interrupt (PCINT) triggered by the optical coin sensor.
2. **STATE_SELECT:** Activates the I2C button matrix for user selection.
3. **STATE_RUNNING:** Actuates the DRV8833 motor driver until the drop sensor is triggered.
4. **STATE_FINISH:** Halts the motor, displays a "Thank You" message on the I2C 16x2 LCD, and resets the loop.

*A Watchdog Timer (WDT) is implemented to automatically recover the system in case of unexpected execution hangs.*

> **View Logic Flowchart:** [Click here to view the FSM Flowchart](./Firmware_Logic/Flowchart_Vending_Machine.png)

## Academic Report
For full technical specifications, hardware pin-mapping, and testing evaluations, please read the [Full Project Report (PDF)](./Reports/Vending_Machine_Report.docx).

> **Visual Documentation:** Photos of the final built device, internal wiring, and documentation from the campus exhibition can be found on **pages 25–27** of the report.

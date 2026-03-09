# C-project
# Vehicle Control System 🚗

## Overview

This project simulates a **Vehicle Control System** using the C programming language.
The system allows the user to control the vehicle engine and simulate sensor readings such as traffic lights, room temperature, and engine temperature.

Based on the sensor inputs, the system automatically adjusts:

* Vehicle speed
* Air Conditioning (AC) state
* Engine Temperature Controller state

The project demonstrates the use of:

* Conditional statements
* Loops
* User input handling
* Preprocessor directives
* Basic embedded systems logic

---

## Features

* Turn the vehicle engine **ON / OFF**
* Simulate **traffic light sensor**
* Simulate **room temperature sensor**
* Simulate **engine temperature sensor**
* Automatic control of:

  * Vehicle speed
  * Air Conditioning (AC)
  * Engine Temperature Controller
* Continuous sensor monitoring while the engine is ON
* Display the **current vehicle state** after every action

---

## System Logic

### Traffic Light Sensor

| Traffic Light | Vehicle Speed |
| ------------- | ------------- |
| G (Green)     | 100 km/h      |
| O (Orange)    | 30 km/h       |
| R (Red)       | 0 km/h        |

---

### Room Temperature Sensor

* If temperature < 10 → AC **ON** and set temperature to **20**
* If temperature > 30 → AC **ON** and set temperature to **20**
* Otherwise → AC **OFF**

---

### Engine Temperature Sensor

* If temperature < 100 → Engine Temperature Controller **ON** and set temperature to **125**
* If temperature > 150 → Engine Temperature Controller **ON** and set temperature to **125**
* Otherwise → Engine Temperature Controller **OFF**

---

### Special Case

If the vehicle speed becomes **30 km/h**:

* Turn **AC ON** if it was OFF and set
  `Room Temperature = Current Temperature * (5/4) + 1`

* Turn **Engine Temperature Controller ON** if it was OFF and set
  `Engine Temperature = Current Temperature * (5/4) + 1`

---

## Vehicle State Output

After applying sensor logic, the system displays:

* Engine State (ON / OFF)
* AC State (ON / OFF)
* Vehicle Speed
* Room Temperature
* Engine Temperature Controller State
* Engine Temperature

---

## Bonus Feature

The project includes a **preprocessor directive**:

```c
#define WITH_ENGINE_TEMP_CONTROLLER 1
```

If set to **1** → Engine Temperature Controller code will compile and run.
If set to **0** → All related code will be excluded during compilation.

This simulates **conditional compilation used in embedded systems**.

---

## Technologies Used

* C Programming Language
* GCC Compiler
* Console-based interface

---

## How to Run

1. Compile the program:

```bash
gcc vehicle_control.c -o vehicle
```

2. Run the program:

```bash
./vehicle
```

3. Follow the menu instructions in the console.

---

## Project Purpose

This project was developed as part of learning **Embedded C fundamentals**, focusing on implementing a **vehicle control logic system using sensors simulation**.

---

## Author

Huda Esam
Junior Software QA Tester | Learning Embedded Systems

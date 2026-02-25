# CAS Interface Board 2026

Control Actuation System (CAS) Interface Board for the UTS Rocketry avionics stack.

This board provides closed-loop control for the airbrake and roll control systems, along with sensor interfaces and onboard data logging. The design is based on the STM32F405RGT6 microcontroller and integrates inertial sensing, actuator control, and non-volatile storage.

The CAS board is intended to operate as part of the UTS Rocketry flight avionics architecture.

---

## Overview

The CAS Interface Board is responsible for:

- Airbrake deployment control
- Roll stabilization control
- Sensor acquisition
- Data logging
- Actuator interfacing

Closed-loop control is performed onboard using IMU and barometric sensor measurements.

---

## Hardware

### Microcontroller

STM32F405RGT6

- ARM Cortex-M4F
- 168 MHz
- Hardware floating point
- 1 MB Flash
- 192 KB RAM

---

### Sensors

#### IMU

LSM6DS3TR-C

Interface:

- SPI (4-wire)

Signals:

- SCK
- MOSI
- MISO
- CS
- DRDY Interrupt

Power:

- 3.3 V

---

#### Barometer

Interface:

- I2C

Signals:

- SCL
- SDA

Power:

- 3.3 V

---

### Storage

#### MicroSD Card

Interface:

- SPI

Signals:

- SCK
- MOSI
- MISO
- CS

Purpose:

- Flight data logging

---

#### External Flash

Interface:

- SPI

Purpose:

- Backup logging
- Blackbox storage

---

### Actuator Interfaces

#### Servo Outputs

- Airbrake Servo
- Roll Control Servo

Control Method:

- Timer PWM outputs

Power:

- Dedicated 5 V servo rail

Signal Voltage:

- 3.3 V logic

---

### Analog Inputs

#### Airbrake Position Feedback

External potentiometer input.

Signals:

- 3.3 V
- ADC Input
- GND

---

### Digital Inputs

#### Limit Switches

Digital inputs for actuator limits.

Typical configuration:

- External pull-down resistors
- GPIO input

---

#### IMU Interrupt

IMU data-ready interrupt.

Connected to STM32 EXTI input.

---

### Debug Interface

Serial Wire Debug (SWD)

Signals:

- SWDIO
- SWCLK
- NRST
- 3.3 V
- GND

Used for:

- Programming
- Debugging

---

## Communication Interfaces

### SPI Buses

SPI1

Used for:

- IMU

SPI2

Used for:

- MicroSD card
- External flash

---

### I2C Bus

I2C1

Used for:

- Barometer

---

## Power Architecture

### 3.3 V Rail

Supplies:

- MCU
- IMU
- Barometer
- Flash
- SD card logic

---

### 5 V Rail

Supplies:

- Servo motors

---

### Grounding

- Continuous ground plane
- Shared logic and servo ground

---

## Control System

### Airbrake Control

The CAS system predicts apogee using altitude and velocity estimates derived from sensor measurements.

Airbrake deployment is adjusted to reach the target apogee.

Inputs:

- Barometer altitude
- Estimated vertical velocity

Outputs:

- Airbrake servo PWM

---

### Roll Control

Roll stabilization is performed using gyroscope measurements from the IMU.

Inputs:

- Roll rate from IMU

Outputs:

- Roll control servo PWM

---

## Firmware

Development tools:

- STM32CubeMX
- STM32CubeIDE
- ST-Link

Features:

- SPI IMU driver
- I2C barometer driver
- PWM servo control
- SD card logging
- Flash logging
- Interrupt-driven sensor acquisition

---

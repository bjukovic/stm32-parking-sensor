# STM32 Parking Sensor System

An embedded parking sensor system developed using an **STM32 Nucleo microcontroller**, an **HC-SR04 ultrasonic sensor**, an **SSD1306 OLED display**, an LED, and a buzzer.

The system measures the distance between the sensor and a nearby obstacle and provides real-time feedback through visual, audio, and display outputs.

## Overview

The project was developed for the **Embedded Systems (EE325)** course at the International University of Sarajevo.

The main goal was to implement a simple parking assistance system that demonstrates fundamental embedded systems concepts such as:

* Sensor interfacing
* GPIO control
* I2C communication
* Precise timing and pulse measurement
* Real-time distance calculation
* Embedded C programming
* Hardware/software integration

The system was also tested on a small remote-controlled truck to simulate a practical parking/reversing scenario.

## Features

* Ultrasonic distance measurement using an HC-SR04 sensor
* Real-time distance display on an SSD1306 OLED
* Distance-based LED warning
* Distance-based buzzer alerts
* Different alert intervals depending on obstacle distance
* STM32 GPIO and I2C peripheral configuration
* Real-time embedded firmware implemented in C

## Hardware

The main components used in the project are:

* STM32 Nucleo development board
* HC-SR04 ultrasonic sensor
* SSD1306 OLED display
* Red LED
* BPT-14X piezo buzzer
* 100 Ω resistor
* Breadboard
* Jumper wires
* USB power source

## System Architecture

The system can be divided into three main blocks:

```text
             ┌─────────────────────┐
             │   HC-SR04 Sensor    │
             │  Distance Detection │
             └──────────┬──────────┘
                        │
                        ▼
             ┌─────────────────────┐
             │   STM32 Nucleo      │
             │                     │
             │ Distance Calculation│
             │ GPIO / Timing       │
             │ Control Logic       │
             └──────┬───────┬──────┘
                    │       │
             ┌──────┘       └──────────┐
             ▼                         ▼
      ┌─────────────┐           ┌─────────────┐
      │ LED + Buzzer│           │ SSD1306 OLED│
      │   Alerts    │           │   Display   │
      └─────────────┘           └─────────────┘
```

## Distance-Based Alerts

The system changes its warning behavior depending on the measured distance:

| Distance   | Alert behavior     |
| ---------- | ------------------ |
| `< 10 cm`  | Rapid alert        |
| `10–20 cm` | Moderate alert     |
| `20–40 cm` | Slow alert         |
| `> 40 cm`  | Standby / no alert |

The OLED continuously displays the measured distance in centimeters.

## Software

The firmware was developed using **STM32CubeIDE** and written in **Embedded C**.

The implementation includes:

* STM32 HAL initialization
* GPIO configuration
* I2C configuration
* SSD1306 OLED control
* Ultrasonic trigger and echo measurement
* Distance calculation
* Distance-based alert control
* DWT cycle counter for precise timing

The distance is calculated from the measured ultrasonic echo time using the time-of-flight principle.

## Pin Configuration

| STM32 Pin | Function                   |
| --------- | -------------------------- |
| PA0       | Ultrasonic sensor trigger  |
| PA1       | Ultrasonic sensor echo     |
| PC2       | LED / alert output         |
| PC3       | Buzzer / alert output      |
| I2C1      | SSD1306 OLED communication |

## Project Structure

```text
stm32-parking-sensor/
│
├── Core/
│   ├── Inc/
│   └── Src/
│
├── Drivers/
│   └── SSD1306/
│
├── docs/
│   └── images/
│
├── README.md
├── Parking Sensor System - Project Report.pdf
├── *.ioc
├── .project
└── .cproject
```

## Testing

The completed system was mounted on a small remote-controlled truck and tested against different obstacles, including walls and boxes.

During testing, the ultrasonic sensor provided distance measurements while the OLED, LED, and buzzer responded according to the measured distance.

The moving setup was used to simulate a practical reversing/parking scenario.

## Challenges

Several hardware and software issues were encountered during development, including:

* Loose or defective sensor and I2C connections
* OLED communication and I2C address configuration
* SSD1306 library integration with the STM32 HAL
* Missing I2C pull-up resistors
* Residual firmware stored on the microcontroller
* Maintaining stable connections while testing the system on a moving platform

These issues were addressed through continuity testing, library configuration, hardware debugging, and complete chip erasure when required.

## Future Improvements

Possible extensions include:

* Multiple ultrasonic sensors for front and side detection
* Wireless communication using Bluetooth or Wi-Fi
* Mobile application integration
* Camera-based obstacle detection
* Machine-learning-based object classification
* Improved enclosure and power supply
* Longer-duration outdoor testing

## Course

**Embedded Systems — EE325**
International University of Sarajevo
Spring 2025

## Authors

**Berina Juković**
**Hena Šehović**

For detailed implementation, hardware configuration, testing, and results, see the project report included in this repository.

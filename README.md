# Mini Project: Smart RTC and Schedule Controller

A microcontroller-based embedded C project built for the NXP LPC2148/LPC21xx family. This project turns a simple development board into a digital clock with an interactive menu, date and time settings, day-of-week tracking, and a configurable ON/OFF schedule that controls an LED.

The system reads inputs from a 4x4 keypad, displays information on a 16x2 LCD, keeps track of real time using the on-chip RTC, and allows users to configure time/date/day and an appliance-style schedule.

## Overview

This project is designed as a mini embedded application for learning and demonstrating:

- Embedded C programming
- Microcontroller peripheral initialization
- Real-Time Clock (RTC) usage
- LCD interfacing
- Keypad scanning
- Interrupt-driven menu requests
- Time-based control logic

In simple terms, it behaves like a small digital clock and scheduler controller that can be used as the foundation for automation or appliance timing logic.

## Features

- Digital clock display with hour, minute, and second
- Date and month display
- Day-of-week display
- RTC configuration menu
- Time adjustment by keypad
- Date adjustment by keypad
- Day selection menu
- ON/OFF schedule configuration
- LED control based on current time
- Midnight crossover schedule support
- Interrupt-based menu access using external interrupt

## Hardware Used

This project is intended for an LPC2148/LPC21xx development board with the following peripherals:

- LPC2148 or compatible LPC21xx microcontroller
- 16x2 LCD display
- 4x4 matrix keypad
- RTC-capable microcontroller clock configuration
- LED output for scheduled control
- External interrupt input for menu trigger

## System Behavior

The firmware initializes:

1. The LCD module
2. The RTC peripheral
3. The keypad matrix
4. The LED output
5. The external interrupt handler

Then it enters a continuous loop that:

- refreshes the LCD with the current time
- shows date/day information in alternating display modes
- reads current RTC values
- compares them with the configured schedule
- turns the LED ON or OFF depending on whether the current time is within the active window

## Menu Structure

The user can access a main menu via an interrupt-triggered request. The project supports the following menu options:

- RTC settings
  - Set time
  - Set date
  - Set day
- Schedule settings
  - Set ON time
  - Set OFF time
  - Save schedule
- Exit menu

The menu is implemented using keypad entries and LCD strings, allowing users to enter values and validate input ranges.

## Project Structure

```text
Mini-project/
├── README.md                 Project documentation
├── KPM.c                     Keypad scanning and numeric input logic
├── KPM.h                     Keypad function declarations
├── KPM_defines.h             Keypad pin definitions and constants
├── LCD.c                     LCD driver implementation
├── LCD.h                     LCD function declarations
├── LCD_defines.h             LCD pin definitions and command constants
├── Rtclock.c                 RTC configuration and access logic
├── Rtclock.h                 RTC API declarations
├── schedule.c                LED scheduling logic and time conversion
├── schedule.h                Schedule and LED declarations
├── delay.c                   Delay functions
├── delay.h                   Delay function declarations
├── output.c                  Main application logic and menu flow
└── types.h                   Shared type definitions (if included by the project)
```

## Key Components

### 1. Keypad Module (`KPM.c`)

Responsible for:

- scanning rows and columns
- identifying pressed keys
- decoding keypad values
- reading numeric input for time/date configuration

This module provides functions like `KeyScan()`, `ReadNum()`, and row/column scanning logic.

### 2. LCD Driver (`LCD.c`)

Responsible for:

- initializing the LCD controller
- sending commands and data
- writing strings and numbers to the display
- displaying menu options and status messages

### 3. RTC Module (`Rtclock.c`)

Responsible for:

- RTC initialization
- setting/getting time
- setting/getting date
- setting/getting day of week

### 4. Schedule Logic (`schedule.c`)

Responsible for:

- converting time values to seconds
- storing ON/OFF time
- checking if the current time is within the active schedule
- controlling an LED output based on that schedule

### 5. Main Application (`output.c`)

This is the central control file that ties all pieces together. It manages:

- initialization
- RTC setup defaults
- menu interaction
- schedule creation
- LED update loop
- continuous display refresh

## How the Schedule Works

The project stores two time values:

- `on_time`
- `off_time`

Then it converts those times to a second-based value and compares them with the current RTC time.

The scheduler supports:

- normal day schedules where ON starts before OFF
- overnight schedules where ON is after OFF (midnight crossover)

If the current time falls within the configured active window, the LED is switched ON; otherwise, it remains OFF.

## Typical Example

For example, if the defined schedule is:

- ON: 09:01
- OFF: 09:02

Then the LED will remain active only during that time interval, and the project will automatically evaluate current time against the interval in each loop.

## Build and Flash Instructions

This project is written in C for a microcontroller target and is meant to be built using an embedded toolchain for LPC2148/LPC21xx devices.

### Prerequisites

- ARM-compatible compiler or IDE
- LPC2148/LPC21xx board support
- Flashing utility or debugger
- Hardware board with LCD, keypad, and LED connected to corresponding pins

### Typical workflow

```bash
# Compile the firmware in your embedded IDE or build system
# Example: Keil µVision / ARM GCC / vendor-specific toolchain

# Flash the generated binary/hex to the LPC2148 board
```

### Notes

- The project uses processor-specific register names such as `lpc21xx.h` and `lpc214x.h`.
- Pin definitions are handled in the peripheral header files and `*_defines.h` files.
- The code is designed for embedded target hardware, not for a desktop PC environment.

## Usage

After flashing the firmware to the board:

1. The LCD starts showing the current time and date
2. The device remains in a running display loop
3. Pressing the configured external interrupt or menu trigger enters the main menu
4. Use the keypad to set time, date, day, or schedule
5. Save changes and continue running the application

## Important Implementation Notes

- The project uses `__irq` interrupt routines for the menu trigger
- Values are validated before being accepted (for example, valid ranges for hour/minute/second/date/month/year)
- The system supports both display modes: date display and schedule display
- Input values are checked to ensure valid ranges are used

## Future Enhancements

This project could be extended with:

- EEPROM storage for persistent schedules
- more advanced alarm features
- buzzer or relay-based control
- SPI/I2C sensor modules
- serial communication for monitoring/debugging
- a more robust menu state machine

## License

This repository does not currently include a license file. If you plan to distribute or reuse it publicly, it is recommended to add an appropriate open-source license.

## Summary

This project is a practical embedded systems mini-project that demonstrates how to build an RTC-driven digital clock and scheduler using C on an LPC2148 board. It combines multiple embedded concepts—LCD, keypad, RTC, interrupts, menu logic, and scheduling—into one working hardware application.

If you are learning embedded C or microcontroller design, this repository is a good hands-on example of how hardware I/O and software logic are combined in a real-time system.

---

Created for: Mini Project / Embedded Systems Learning

Author: varshareddy011

Repository: https://github.com/varshareddy011/Mini-project

























































































































































































































































































































































































































































































































































































































































































































































































































































































































































































n
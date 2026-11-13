<div align="center">

# RTC Scheduler

### LPC2148-based real-time clock and scheduled LED controller

A bare-metal Embedded C project that combines an RTC, a 16×2 LCD, a 4×4 keypad, and scheduled LED control.

[Features](#features) · [Hardware](#hardware) · [How-it-works](#how-it-works) · [Build-and-run](#build-and-run) · [Project-structure](#project-structure)

</div>

---

## Overview

RTC Scheduler is a microcontroller project for the LPC2148/LPC21xx family. It displays the current time, date, and day on an LCD; lets a user configure clock and schedule values through a keypad menu; and switches an LED according to the configured daily ON/OFF interval.

The project is intended as a learning and demonstration example for embedded C, peripheral interfacing, and real-time control. The LED is a demonstration output; controlling mains-powered equipment would require appropriately rated, isolated hardware and a safe design.

## Features

- Displays hours, minutes, seconds, date, month, year, and day of week.
- Provides keypad menus to set the RTC time, date, and day.
- Allows users to configure and save schedule ON and OFF times.
- Validates entered time and calendar values in the application menus.
- Controls an LED according to the schedule; the ON instant is included and the OFF instant is excluded.
- Supports schedules that cross midnight.
- Uses an external interrupt to request entry to the menu.

## Hardware

The firmware is written for LPC2148/LPC21xx-style hardware and expects the peripherals below. Check the source pin definitions and your board schematic before wiring; this repository does not include a complete wiring diagram or board configuration guide.

| Component | Purpose |
| --- | --- |
| LPC2148 or compatible LPC21xx board | Runs the firmware and provides the RTC and GPIO |
| 16×2 character LCD | Displays the clock, date, status, and menus |
| 4×4 matrix keypad | Menu navigation and numeric input |
| LED | Shows whether the schedule is active |
| External interrupt input | Requests the menu |

> **Safety:** The project’s output is an LED. Do not connect an appliance or mains load directly to a microcontroller pin. Use a properly rated and isolated driver circuit designed for the load.

## How it works

1. `main()` in `output.c` initializes the LCD, RTC, keypad, LED, and external interrupt.
2. The main loop refreshes the display and reads the RTC.
3. `Schedule_IsActive()` compares current time with the saved ON/OFF interval. `schedule.c` handles both ordinary intervals and intervals crossing midnight.
4. `LED_Control()` updates the LED output.
5. The external interrupt sets a menu request flag; the main loop responds by entering the keypad-driven menus.

### Menu controls

- **Main menu:** `1` opens RTC settings, `2` opens schedule settings, `3` exits the menu.
- **RTC menu:** `1` time, `2` date, `3` day, `4` back.
- **Time and date submenus:** use the displayed number choices to select a field and return.
- **Schedule menu:** `1` configures ON time, `2` configures OFF time, `3` saves and returns.

The firmware uses a 4×4 keypad layout defined in `KPM.c`. The menu is requested by the configured external interrupt (EINT0); check the board wiring and `EINT0_Init()` in `output.c` to identify the correct trigger input for your setup.

## Project structure

```text
.
├── output.c          Main application, display loop, menus, and EINT0 handling
├── schedule.c        Schedule interval checks and LED GPIO control
├── schedule.h        Schedule and LED interface
├── Rtclock.c         RTC initialization and register access
├── Rtclock.h         RTC interface
├── KPM.c             4×4 keypad scanning and numeric input
├── KPM.h             Keypad interface
├── KPM_defines.h     Keypad pin and layout definitions
├── LCD.c             LCD initialization and display helpers
├── LCD.h             LCD interface
├── LCD_defines.h     LCD pin and command definitions
├── delay.c           Delay implementation
├── delay.h           Delay interface
└── README.md          Project documentation
```

### Main modules

- **`output.c`** coordinates initialization, LCD updates, user menus, RTC configuration, scheduling, and LED updates.
- **`KPM.c`** scans the keypad and provides `KeyScan()` and `ReadNum()` for menu input.
- **`LCD.c`** sends LCD commands and data and provides string and numeric display helpers.
- **`Rtclock.c`** reads and writes RTC time, date, and day-of-week registers.
- **`schedule.c`** converts times to seconds, checks the active interval, and controls the LED.
- **`delay.c`** supplies timing helpers used by the peripheral code.

## Build and run

This repository contains C source and headers, but does not currently include a Makefile, IDE project, linker script, startup code, or a documented automated test setup. It is firmware for a physical target, not a standalone desktop application.

To build and run it:

1. Open or create a project for the exact LPC microcontroller on your board in a compatible ARM embedded toolchain.
2. Add the project’s required `.c` files and headers, along with the device-specific CMSIS/vendor headers, startup code, and linker configuration required by that toolchain.
3. Confirm that the target device, clock configuration, peripheral pin mapping, LCD wiring, keypad wiring, and interrupt input match the code and board.
4. Build the firmware, flash it to the board, and test the LCD, keypad, RTC, interrupt input, and LED individually.
5. Set the RTC and schedule from the menu, then verify the LED at times before, within, and after the configured interval.

The source uses LPC device headers (including `lpc21xx.h` and `lpc214x.h`) and compiler-specific interrupt syntax such as `__irq`. The exact compiler setup may therefore need adaptation for your selected chip and toolchain. No single build command can be provided from the files currently in the repository.

## Configuration and implementation notes

- The code has initial date/day and schedule values in `output.c`; review these defaults before using the firmware.
- Schedule and hardware settings are held in memory and initialized by the application; persistent schedule storage is not implemented.
- Pin assignments and LCD/keypad wiring are hardware-dependent. Confirm them in the `*_defines.h` headers and against your board documentation.
- `Rtclock.c` contains LPC2148-specific RTC clock-source configuration. Confirm that it matches your exact MCU and oscillator setup.
- This project has not been documented with a hardware test report or a reproducible build configuration. Treat the build steps above as setup guidance and verify behavior on your target board.

## Validation checklist

- [ ] LCD initializes and displays the time/date.
- [ ] Keypad presses are detected and menu values are entered correctly.
- [ ] RTC time, date, and day can be updated.
- [ ] Invalid values are rejected by the menus.
- [ ] LED remains inactive before the ON time, becomes active during the interval, and turns off at the OFF time.
- [ ] An interval crossing midnight behaves as expected.
- [ ] The interrupt input requests the menu on the target hardware.

## Learning and project use

This repository can support an embedded systems lab, academic mini-project, portfolio demonstration, or internship/final-year project. It demonstrates microcontroller GPIO, LCD and keypad interfacing, RTC access, interrupt handling, and time-based decision logic. For academic submissions, supplement the source with your own board details, circuit diagram, toolchain/build settings, photographs, and measured test results rather than presenting unverified results as completed tests.

## Possible extensions

- Add an IDE project or reproducible build system with documented toolchain and MCU configuration.
- Store schedule settings in non-volatile memory.
- Add a relay/driver stage for a suitably rated low-voltage load, with appropriate isolation and protection.
- Add serial diagnostics, alarms, or additional schedules.
- Add automated tests for schedule calculations and boundary conditions.

## License

No license file is currently included. Until a license is added, reuse and redistribution permissions are not explicitly granted. Repository owners can add an open-source license if they want to permit reuse.

## Author

**Varsha Reddy** · [GitHub profile](https://github.com/varshareddy011)

---

<p align="center"><sub>Embedded C · LPC2148 · RTC · LCD · Keypad · Scheduling</sub></p>

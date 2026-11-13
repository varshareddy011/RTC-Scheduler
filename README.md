# RTC-Based LED Schedule Controller Using LPC2148

A microcontroller-based embedded systems project designed around the LPC2148/LPC21xx family. The system combines keypad input, LCD display, real-time clock functionality, and time-based control logic to create a compact digital clock and scheduling controller that switches an LED based on a user-defined ON/OFF timetable.

This repository is suitable for academic submission, professional portfolio presentation, embedded systems learning, and internship/final-year project documentation.

## 1. Project Title

RTC-Based LED Schedule Controller Using LPC2148

## 2. Abstract

This project demonstrates the design and implementation of a real-time embedded system using the LPC2148 microcontroller. The system displays current time, date, and day information on a 16x2 LCD, accepts user commands from a 4x4 keypad, and allows configuration of RTC settings and an ON/OFF schedule. Based on the configured schedule, an LED is turned ON or OFF automatically.

The application is a practical example of how embedded hardware and software interact in real time. It integrates multiple peripheral modules such as keypad scanning, display output, timer/clock management, and interrupt-driven control logic. The project is useful as a base for automation systems, appliance control, and  time-scheduling applications.

## 3. Problem Statement

Embedded systems are widely used in automation, time-based control, and user-interactive devices. A common requirement in - systems is the ability to keep track of time, allow user adjustments, and trigger an action based on a schedule. Traditional systems often require complex hardware and software combinations.

This project addresses this need by implementing a compact microcontroller-based controller that can:

- read real time from the RTC
- display information on an LCD
- take user input from a keypad
- allow time/date configuration
- control a device (LED) according to a defined schedule

## 4. Objectives

The main objectives of this project are:

- To design a realtime clock-based embedded application using LPC2148
- To interface a keypad with a microcontroller for user input
- To display time and date on an LCD
- To configure RTC values through a menu-driven interface
- To implement an ON/OFF scheduling mechanism
- To control an LED using time-based logic
- To create a simple and reliable embedded solution suitable for demonstrations and learning

## 5. Project Scope

The project includes:

- RTC initialization and time/date management
- LCD initialization and display logic
- 4x4 keypad scanning and number input
- menu-driven configuration system
- LED scheduling logic with cross-midnight support
- external interrupt for menu triggering

The project does not include advanced networking, database integration, or cloud-based monitoring. It is focused on embedded control and real-time hardware interaction.

## 6. Project Significance

This project is significant because it introduces students and developers to essential embedded systems concepts, including:

- microcontroller peripheral interfacing
- real-time clock operations
- user interface development
- embedded firmware architecture
- interrupt-driven event handling
- scheduling logic in embedded applications

It is also a strong example of building a system that is both practical and easy to understand.

## 7. Features

- Real-time clock display for hours, minutes, and seconds
- Date, month, and year display
- Day-of-week tracking
- 4x4 keypad-based user interaction
- LCD menu system for RTC setup
- Time validation logic
- Date validation logic
- Day selection menu
- ON/OFF schedule configuration
- LED control based on current time
- Midnight-overlap schedule support
- Menu request using external interrupt
- Continuous real-time monitoring loop

## 8. Hardware Requirements

The project targets the LPC2148 or a compatible LPC21xx microcontroller board and requires the following hardware:

- LPC2148 / LPC21xx development board
- 16x2 LCD display
- 4x4 matrix keypad
- LED indicator
- Breadboard / PCB wiring
- Power supply
- Optional external interrupt trigger input

## 9. Software Requirements

The project is implemented in embedded C and requires an ARM-compatible toolchain such as:

- Keil µVision
- ARM GCC
- LPC-specific firmware development environment
- Flashing utility or debugger

## 10. System Architecture

The application is built as a layered embedded system:

- Input Layer: keypad, external interrupt
- Processing Layer: LPC2148 microcontroller
- Storage/Time Layer: RTC registers and time variables
- Output Layer: LCD display and LED control

The system continuously monitors time and decides whether the LED should be ON or OFF based on the configured schedule.

## 11. Block Diagram

```text
+------------------+
| 4x4 Keypad       |
+---------+--------+
          |
          v
+------------------+
| LPC2148 MCU      |
| - RTC            |
| - GPIO           |
| - Interrupts     |
+---------+--------+
          |
     +----+----+
     |         |
     v         v
+-----------+ +-----------+
| LCD       | | LED       |
| 16x2      | | Output    |
+-----------+ +-----------+
```

## 12. Working Principle

On startup, the microcontroller initializes the LCD, RTC, keypad, LED, and interrupt system. It then begins displaying the current time and date. The user can enter the menu system to configure:

- current time
- date
- day
- ON schedule
- OFF schedule

The schedule is stored as time values, converted to seconds, and compared with the current RTC time. When the current time matches the scheduled interval, the LED is activated. The system continues updating in a cyclic loop.

## 13. Functional Description

### RTC Section
The RTC module initializes the real-time clock and provides functions to:

- set time
- get time
- set date
- get date
- set day of week

### LCD Section
The LCD module handles:

- command and data writes
- initialization routines
- string and numeric display
- 2-line output formatting

### Keypad Section
The keypad logic performs:

- row scanning
- column detection
- key decoding
- numeric value reading

### Schedule Section
The schedule module performs:

- HH:MM conversion to seconds
- ON/OFF time storage
- schedule comparison logic
- LED output control

### Main Controller
The main file is responsible for the complete behavior of the device. It bridges all modules together and manages the main application loop.

## 14. Menu Flow

The firmware uses a menu-driven structure for user interaction.

Main Menu:

- RTC
- Schedule
- Exit

RTC Menu:

- Time
- Date
- Day
- Back

Schedule Menu:

- ON Time
- OFF Time
- Save Schedule
- Back

This menu is navigated using keypad entries and displayed on the LCD.

## 15. Project Structure

```text
Mini-project/
├── README.md
├── KPM.c
├── KPM.h
├── KPM_defines.h
├── LCD.c
├── LCD.h
├── LCD_defines.h
├── Rtclock.c
├── Rtclock.h
├── schedule.c
├── schedule.h
├── delay.c
├── delay.h
├── output.c
├── types.h
└── other board-specific support files
```

## 16. File-wise Overview

### KPM.c / KPM.h
Responsible for keypad scanning and decoding user input.

### LCD.c / LCD.h
Responsible for LCD initialization and display output.

### Rtclock.c / Rtclock.h
Responsible for RTC read/write operations.

### schedule.c / schedule.h
Responsible for ON/OFF schedule logic and LED control.

### output.c
Main controller logic for the complete project behavior.

### delay.c / delay.h
Provides delay functions needed for timing and LCD operations.

## 17. How the Schedule Logic Works

The project converts hour and minute values into seconds using the formula:

```c
seconds = (hour * 3600) + (minute * 60) + second;
```

Then it compares the current time with the configured ON/OFF interval. If the current time falls inside the active period, the LED is triggered. The logic also handles schedules that cross midnight.

## 18. Example Workflow

A typical operational sequence is:

1. Power ON the board
2. LCD displays current time
3. User presses the menu trigger
4. User enters RTC menu
5. User sets time or date
6. User enters schedule menu
7. User sets ON and OFF times
8. The LED follows the schedule automatically

## 19. Output and Results

The system demonstrates:

- time management using RTC
- real-time display on LCD
- keypad-based configuration
- automated control action based on time

This proves the viability of embedded scheduling in a compact system.

## 20. Use Cases

This project can be adapted for:

- automatic street light control
- office appliance scheduling
- digital clock with control interface
- classroom demonstration of embedded systems
- home automation prototypes
- timer-based switching devices

## 21. Advantages

- Simple and low-cost embedded design
- Easy to understand and demonstrate
- Real-time scheduling capability
- Good learning project for electronics and C programming
- Suitable for microcontroller lab work

## 22. Limitations

- No persistent storage for schedule data after power reset
- No external communication or web dashboard
- Hardware-specific pin configuration is necessary
- Limited to onboard device control (LED demonstration)

## 23. Future Enhancements

Possible extensions include:

- EEPROM storage for saved time and schedule settings
- Relay output instead of LED for practical appliance control
- Buzzer alarm functionality
- Temperature and humidity monitoring
- GSM / Wi-Fi communication
- Web or mobile monitoring interface
- Real-time logging and event tracking

## 24. Academic Relevance

This project is relevant for:

- Embedded Systems
- Microprocessor and Microcontroller Lab
- Real-Time Systems
- Internet of Things (IoT) basics
- Digital Design and Automation
- Embedded C Programming

It is a strong example of hardware-software integration and real-time control.

## 25. Portfolio / Interview Relevance

This project demonstrates:

- microcontroller interfacing skills
- practical embedded software development
- peripheral integration knowledge
- ability to build a user-driven real-time system
- understanding of design and testing in embedded engineering

It is a strong addition to a portfolio for embedded systems, firmware, or electronics-related roles.

## 26. Open-Source Presentation Summary

This repository is a clean, hardware-focused C project that showcases a complete embedded application. It can be presented as:

- a learning project
- a laboratory demonstration
- a real-world automation prototype
- a microcontroller-based scheduling system

The code is organized into modules for easy understanding and expansion.

## 27. Internship / Final-Year Project Documentation

The project can be documented as a final-year mini project or internship assignment under the following headings:

- Introduction
- Background and Motivation
- Hardware and Software Requirements
- Methodology
- System Design
- Implementation
- Results and Discussion
- Conclusion
- Future Scope

This repository can easily serve as the implementation artifact for such a report.

## 28. Testing and Validation

The project can be validated by checking:

- LCD initializes correctly
- keypad input is detected correctly
- RTC values update properly
- menu input accepts valid values only
- invalid time/date values are rejected
- LED changes state when time enters and exits the schedule interval

## 29. Conclusion

The - RTC-Based LED Schedule Controller is a practical embedded systems project that demonstrates real-time clock functionality, menu-driven user interaction, and time-based logic control. It combines multiple core concepts in microcontroller programming and embedded design in a compact and understandable implementation.

This project is suitable for learning, demonstration, and documentation across academic, portfolio, and internship contexts.

## 30. License

This repository currently does not include a formal software license file. If the project is intended for public distribution or reuse, it is recommended to add an appropriate license such as MIT or Apache 2.0.

## 31. Author

Varsha Reddy

GitHub: https://github.com/varshareddy011
Repository: https://github.com/varshareddy011/Mini-project

## 32. References

- LPC2148 / LPC21xx microcontroller documentation
- Embedded C programming principles
- LCD interfacing concepts
- RTC and GPIO register programming
- Real-time embedded scheduling design

---

This README is written to be clear enough for academic submission, portfolio display, open-source presentation, and internship/final-year project documentation.

# STM32 Learning

This repository documents my structured journey learning STM32 embedded systems development with the STM32 NUCLEO-F446RE.

The goal is to build practical embedded C and firmware skills through theory, hardware experiments, STM32Cube projects, engineering documentation, and progressively more advanced applications.

## Objectives

- Learn embedded C programming.
- Understand STM32 microcontroller architecture and peripherals.
- Configure projects and peripherals with STM32CubeMX.
- Build, program, test, and debug firmware with STM32CubeIDE and ST-LINK.
- Develop safe, reliable hardware interfaces.
- Use professional Git and GitHub workflows.
- Build an embedded systems engineering portfolio.

## Hardware

- STM32 NUCLEO-F446RE development board
- Breadboards and jumper wires
- LEDs and resistors
- Pushbuttons
- Potentiometers
- USB-to-serial adapter
- Soldering equipment
- Basic electronic components

Additional sensors and communication modules may be added as the repository develops.

## Software

- STM32CubeMX
- STM32CubeIDE
- Visual Studio Code
- Git and GitHub
- macOS Terminal

## Repository Structure

```text
stm32-learning/
├── README.md
├── ROADMAP.md
├── CHANGELOG.md
├── CONTRIBUTING.md
├── 01_gpio/
│   ├── README.md
│   ├── theory.md
│   ├── notes.md
│   ├── cheat-sheet.md
│   ├── exercises/
│   ├── projects/
│   ├── cube_projects/
│   │   ├── 01_gpio_led_blink/
│   │   ├── 02_gpio_led_button/
│   │   └── 03_gpio_led_toggle/
│   └── images/
├── 02_uart/
├── 03_timers/
├── 04_interrupts/
├── 05_adc/
├── 06_pwm/
├── 07_spi/
├── 08_i2c/
├── 09_dma/
├── 10_rtos/
├── notes/
├── diagrams/
└── resources/
```

## Progress

### Module 01 — GPIO: Completed Fundamentals

- Configured the NUCLEO-F446RE with STM32CubeMX.
- Generated, built, and programmed projects with STM32CubeIDE.
- Verified successful programming through ST-LINK.
- Completed LED blink using PA5 / LD2.
- Completed direct button control using PC13 / B1 and polling.
- Completed button-toggle behaviour using state-change detection and simple debounce.
- Documented GPIO modes, pull resistors, HAL functions, polling, edges, and bounce.

Completed projects:

1. `01_gpio_led_blink`
2. `02_gpio_led_button`
3. `03_gpio_led_toggle`

### Next Module

Module 02 — UART communication.

## Current Status

| Module | Status |
|---|---|
| 01 GPIO | Fundamentals and three onboard projects completed |
| 02 UART | Next |
| 03 Timers | Planned |
| 04 Interrupts | Planned |
| 05 ADC | Planned |
| 06 PWM | Planned |
| 07 SPI | Planned |
| 08 I2C | Planned |
| 09 DMA | Planned |
| 10 RTOS | Planned |

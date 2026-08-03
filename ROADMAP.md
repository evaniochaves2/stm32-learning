# STM32 Learning Roadmap

This roadmap tracks my progression through STM32 embedded systems development using the STM32 NUCLEO-F446RE.

## Phase 1 — Fundamentals

### 01 — GPIO

- [x] Digital logic, inputs, and outputs
- [x] Push-pull and open-drain output modes
- [x] Floating, pull-up, and pull-down inputs
- [x] STM32CubeMX pin configuration and code generation
- [x] STM32CubeIDE build and programming workflow
- [x] ST-LINK download and verification
- [x] LED blink project
- [x] Button polling project
- [x] Button-toggle project with state tracking
- [x] Introductory software debounce
- [ ] External LED and button breadboard exercise

### 02 — UART

- [ ] UART frames, TX/RX, and baud rate review
- [ ] Configure USART2
- [ ] Transmit text to a serial terminal
- [ ] Receive and process commands
- [ ] Build a UART-controlled GPIO application

### 03 — Timers

- [ ] Timer clock and prescaler concepts
- [ ] Periodic events without blocking delays
- [ ] Hardware timer exercise
- [ ] Digital stopwatch project

### 04 — Interrupts

- [ ] External interrupt concepts
- [ ] Configure B1 / PC13 for EXTI
- [ ] Implement the HAL GPIO EXTI callback
- [ ] Interrupt-safe button debounce
- [ ] Compare polling and interrupt-driven input

## Phase 2 — Core Peripherals

### 05 — ADC

- [ ] Analog signal fundamentals
- [ ] Read a potentiometer
- [ ] Convert ADC counts to voltage

### 06 — PWM

- [ ] Duty cycle and frequency
- [ ] LED dimming
- [ ] Servo control

### 07 — SPI

- [ ] SPI bus fundamentals
- [ ] Master communication exercise
- [ ] Peripheral or display interface

### 08 — I2C

- [ ] I2C addressing and open-drain bus behaviour
- [ ] Device scanning
- [ ] Sensor or display interface

## Phase 3 — Advanced Topics

### 09 — DMA

- [ ] DMA concepts
- [ ] Peripheral data transfer
- [ ] Compare CPU-driven and DMA-driven transfers

### 10 — RTOS

- [ ] FreeRTOS tasks and scheduler
- [ ] Queues, semaphores, and synchronization
- [ ] Multi-task embedded application

## Completed Projects

- [x] `01_gpio_led_blink` — automatic LED blink
- [x] `02_gpio_led_button` — button-controlled LED
- [x] `03_gpio_led_toggle` — stateful LED toggle with simple debounce

## Planned Engineering Projects

- UART terminal communication
- UART-controlled LED
- Non-blocking LED patterns
- Digital stopwatch
- Potentiometer voltage monitor
- PWM LED dimmer
- Servo motor control
- Sensor and display interfaces
- Data logger
- Multi-peripheral embedded application

## Long-Term Goals

- Develop strong embedded C programming skills.
- Understand STM32 peripherals and hardware abstraction.
- Learn professional firmware development and documentation practices.
- Build a portfolio of tested embedded systems projects.
- Prepare for embedded software, automation, and firmware engineering roles.

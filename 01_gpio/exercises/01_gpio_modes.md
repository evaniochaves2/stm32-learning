# Exercise 01: GPIO Modes

## Objective

Identify the correct STM32 GPIO mode and pull configuration for common devices.

## Hardware Context

- Board: NUCLEO-F446RE
- Logic level: 3.3 V
- Onboard LED LD2: PA5
- Onboard button B1: PC13
- USART2 TX: PA2

## Questions and Answers

### 1. What does GPIO mean?

GPIO means **General-Purpose Input/Output**. A GPIO pin can be configured by software to read a digital signal or drive a digital output.

### 2. Select the correct mode for each device

| Device | Pin | Correct mode | Pull setting | Reason |
|---|---|---|---|---|
| LD2 LED | PA5 | Output Push-Pull | No Pull | The MCU actively drives the LED on and off. |
| B1 button | PC13 | Input or External Interrupt | Board-defined / No Pull | The MCU reads the button state. The Nucleo board provides the required button circuitry. |
| USART2 TX | PA2 | Alternate Function Push-Pull | No Pull | The USART peripheral controls the pin. |

### 3. Push-pull versus open-drain

- **Push-pull:** actively drives the output both HIGH and LOW. This is normally used for an LED.
- **Open-drain:** actively drives LOW but needs a pull-up resistor to become HIGH. It is common on shared communication lines such as I2C.

### 4. Why is a floating input a problem?

A floating input has no defined HIGH or LOW level. Electrical noise can make its reading change unpredictably. A pull-up or pull-down resistor gives the pin a stable default state.

### 5. Pull resistors

- **Pull-up:** holds the input HIGH when nothing else drives it.
- **Pull-down:** holds the input LOW when nothing else drives it.

## Review Check

1. Which GPIO mode should normally control an LED? **Output Push-Pull**
2. Which mode allows USART to control a pin? **Alternate Function**
3. What voltage represents the STM32F446RE logic supply? **3.3 V**
4. Why should an unused input not float? **Noise may cause unpredictable readings.**

## Completion

- [x] Identified input, output, and alternate-function modes
- [x] Compared push-pull and open-drain outputs
- [x] Explained pull-up, pull-down, and floating inputs

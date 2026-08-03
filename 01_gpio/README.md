# Module 01 — GPIO (General-Purpose Input/Output)

## Overview

GPIO is the foundation of embedded systems programming. It allows firmware to read digital inputs and control digital outputs. This module combines GPIO theory, STM32CubeMX configuration, STM32 HAL programming, and practical work with the STM32 NUCLEO-F446RE.

## Learning Outcomes

In this module, I learned to:

- Explain digital inputs, outputs, and 3.3 V logic levels.
- Identify the onboard LD2 LED on PA5 and B1 user button on PC13.
- Distinguish push-pull, open-drain, floating, pull-up, and pull-down configurations.
- Configure pins and generate starter code with STM32CubeMX.
- Build, program, and test firmware with STM32CubeIDE and ST-LINK.
- Use STM32 HAL functions to write, read, and toggle GPIO pins.
- Poll a button and detect a change between its previous and current states.
- Apply a simple delay-based button debounce.

## Completed STM32Cube Projects

| Project | Behaviour | Main concepts |
|---|---|---|
| `01_gpio_led_blink` | LD2 changes state every 500 ms | Digital output, toggle, delay |
| `02_gpio_led_button` | B1 directly controls LD2 | Digital input, polling, conditional logic |
| `03_gpio_led_toggle` | Each button action changes and retains the LED state | Edge detection, state tracking, debounce |

## Board Pins Used

| Board component | STM32 pin | Configuration used |
|---|---|---|
| LD2 green LED | PA5 | GPIO output, push-pull, no pull, low speed |
| B1 user button | PC13 | Button input/EXTI pin, no internal pull in the generated board configuration |
| USART2 TX | PA2 | Alternate function (generated but not used in these GPIO exercises) |

## Important HAL Functions

```c
HAL_GPIO_WritePin(GPIOx, GPIO_Pin, PinState);
HAL_GPIO_ReadPin(GPIOx, GPIO_Pin);
HAL_GPIO_TogglePin(GPIOx, GPIO_Pin);
HAL_Delay(milliseconds);
```

## Module Files

| File or folder | Purpose |
|---|---|
| `theory.md` | Full GPIO lesson content |
| `notes.md` | Study notes and practical observations |
| `cheat-sheet.md` | Quick revision reference |
| `exercises/` | Short practice exercises |
| `projects/` | Project documentation and source examples |
| `cube_projects/` | Complete STM32CubeMX/STM32CubeIDE projects |
| `images/` | Hardware photos, diagrams, and screenshots |

## Progress

- [x] GPIO fundamentals and digital logic
- [x] GPIO input and output modes
- [x] Push-pull and open-drain outputs
- [x] Floating, pull-up, and pull-down inputs
- [x] STM32CubeMX board and pin configuration
- [x] STM32CubeIDE code generation and project workflow
- [x] Build with 0 errors and 0 warnings
- [x] Program and verify the NUCLEO-F446RE with ST-LINK
- [x] Project 1 — LED blink
- [x] Project 2 — Button-controlled LED using polling
- [x] Project 3 — Button-toggle LED with state tracking and simple debounce
- [ ] External LED and pushbutton circuit on a breadboard
- [ ] GPIO interrupts (covered in Module 04)

## Next Step

Continue to Module 02 — UART. GPIO interrupt handling will be revisited in Module 04 after the fundamentals modules.

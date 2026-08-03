# GPIO Project: LED Blink

## Project Summary

This introductory STM32 project blinks the onboard LD2 LED on a NUCLEO-F446RE every 500 ms. It demonstrates the complete workflow from CubeMX pin configuration through CubeIDE build, ST-LINK programming, and physical testing.

## Project Details

| Item | Value |
|---|---|
| CubeIDE project | `01_gpio_led_blink` |
| Board | NUCLEO-F446RE |
| MCU | STM32F446RE |
| Output | LD2 green LED |
| Pin | PA5 |
| Timing | 500 ms per state |
| Framework | STM32 HAL |

## Configuration

PA5 was configured as a low-speed push-pull GPIO output with no internal pull resistor. The initial output level was LOW.

## Core Implementation

```c
while (1)
{
  HAL_GPIO_TogglePin(LD2_GPIO_Port, LD2_Pin);
  HAL_Delay(500);
}
```

## Program Flow

1. HAL and the system clock are initialized.
2. GPIO configuration is applied.
3. LD2 changes to its opposite state.
4. The program waits 500 ms.
5. The infinite loop repeats.

## Verification

- Build result: 0 errors, 0 warnings
- Programming: download verified successfully through ST-LINK
- Hardware test: LD2 visibly alternated between on and off

## Skills Demonstrated

- STM32CubeMX board and GPIO configuration
- STM32CubeIDE code generation and building
- Safe editing inside CubeMX `USER CODE` sections
- HAL GPIO output control
- Blocking millisecond delays
- ST-LINK programming and physical verification

## Improvement Ideas

- Replace the blocking delay with timer-based or `HAL_GetTick()` timing.
- Make the blink interval configurable.
- Drive an external LED with a current-limiting resistor.

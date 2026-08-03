# GPIO Project: Button-Toggled LED

## Project Summary

This project toggles the onboard LD2 LED once for each new press of the onboard B1 button. It introduces button-state memory, software edge detection, and basic debouncing.

## Project Details

| Item | Value |
|---|---|
| CubeIDE project | `03_gpio_led_toggle` |
| Board | NUCLEO-F446RE |
| MCU | STM32F446RE |
| Input | B1 blue button on PC13 |
| Output | LD2 green LED on PA5 |
| Detection | RESET-to-SET state transition |
| Debounce | Simple 50 ms blocking delay |
| Framework | STM32 HAL |

## State Variable

```c
GPIO_PinState previousButtonState = GPIO_PIN_RESET;
```

## Core Implementation

```c
while (1)
{
  GPIO_PinState currentButtonState =
      HAL_GPIO_ReadPin(B1_GPIO_Port, B1_Pin);

  if ((currentButtonState == GPIO_PIN_SET) &&
      (previousButtonState == GPIO_PIN_RESET))
  {
    HAL_GPIO_TogglePin(LD2_GPIO_Port, LD2_Pin);
    HAL_Delay(50);
  }

  previousButtonState = currentButtonState;
}
```

## How State-Change Detection Works

The current button reading is compared with the saved previous reading. The LED changes only when the input moves from RESET to SET. A button that remains held therefore produces only one toggle.

## Debouncing

Mechanical contacts may briefly switch several times during one press. The 50 ms delay is a simple way to reduce false toggles. It is suitable for this exercise but blocks other main-loop work during the delay.

## Verification

- Project built and programmed successfully
- First press turned LD2 on and it stayed on after release
- Second press turned LD2 off and it stayed off after release
- Repeated presses alternated the LED state correctly

## Skills Demonstrated

- Tracking program state with a variable
- Reading and comparing GPIO states
- Software edge detection
- Toggling a GPIO output
- Basic mechanical-button debouncing
- Testing persistent output behaviour

## Improvement Ideas

- Replace `HAL_Delay()` with non-blocking time checks using `HAL_GetTick()`.
- Implement B1 using an external interrupt and callback.
- Build a reusable debounce function or state machine.
- Add short and long press behaviours.

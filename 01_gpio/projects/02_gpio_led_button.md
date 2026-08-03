# GPIO Project: Button-Controlled LED

## Project Summary

This project uses the onboard B1 button as a digital input to control the onboard LD2 LED. LD2 is on only while B1 is pressed, demonstrating input polling and explicit output-state control.

## Project Details

| Item | Value |
|---|---|
| CubeIDE project | `02_gpio_led_button` |
| Board | NUCLEO-F446RE |
| MCU | STM32F446RE |
| Input | B1 blue button on PC13 |
| Output | LD2 green LED on PA5 |
| Method | GPIO polling |
| Framework | STM32 HAL |

## Core Implementation

```c
while (1)
{
  if (HAL_GPIO_ReadPin(B1_GPIO_Port, B1_Pin) == GPIO_PIN_SET)
  {
    HAL_GPIO_WritePin(LD2_GPIO_Port, LD2_Pin, GPIO_PIN_SET);
  }
  else
  {
    HAL_GPIO_WritePin(LD2_GPIO_Port, LD2_Pin, GPIO_PIN_RESET);
  }
}
```

## Program Flow

1. Read the digital state of B1.
2. If the button is pressed, write SET to LD2.
3. Otherwise, write RESET to LD2.
4. Repeat continuously in the main loop.

## Verification

- Build result: 0 errors, 0 warnings
- Firmware downloaded successfully
- Pressing B1 turned LD2 on
- Releasing B1 turned LD2 off

## Skills Demonstrated

- Digital input reading
- Digital output writing
- Conditional logic in embedded C
- GPIO polling
- Connecting software behaviour to physical input and output devices

## Design Note

Polling is simple and appropriate for this learning exercise, but it repeatedly uses processor time to check the input. A future project can use an external interrupt when the program must respond to an input while performing other work.

## Improvement Ideas

- Add button debouncing.
- Use a GPIO interrupt callback.
- Control an external LED or relay-interface circuit with suitable protection.

# Exercise 03: Button Input

## Objective

Read the onboard B1 button and control LD2 using GPIO polling.

## Required Behaviour

- Button pressed: LD2 on
- Button released: LD2 off

## Hardware and Pins

| Component | Pin | Purpose |
|---|---|---|
| B1 blue button | PC13 | Digital input |
| LD2 green LED | PA5 | Digital output |

No external wiring is required.

## Coding Task

Add this logic inside the infinite loop:

```c
if (HAL_GPIO_ReadPin(B1_GPIO_Port, B1_Pin) == GPIO_PIN_SET)
{
  HAL_GPIO_WritePin(LD2_GPIO_Port, LD2_Pin, GPIO_PIN_SET);
}
else
{
  HAL_GPIO_WritePin(LD2_GPIO_Port, LD2_Pin, GPIO_PIN_RESET);
}
```

## How It Works

- `HAL_GPIO_ReadPin()` samples the button input.
- The `if` statement selects an action based on the reading.
- `HAL_GPIO_WritePin()` explicitly turns LD2 on or off.
- The loop polls the button repeatedly while the board is running.

## Expected Result

LD2 remains on only while B1 is pressed and turns off after B1 is released.

## Test Record

- [x] Project built with 0 errors and 0 warnings
- [x] Firmware programmed successfully
- [x] Button press turned LD2 on
- [x] Button release turned LD2 off

## Review Questions

1. What is polling?  
   Repeatedly checking an input inside the main loop.

2. Why use `HAL_GPIO_WritePin()` here instead of `HAL_GPIO_TogglePin()`?  
   The output must match a specific button state rather than simply change state.

3. How is this different from the blink exercise?  
   The LED is controlled by an external input instead of elapsed time.

## Note

The generated board configuration may label B1 as an external-interrupt input. The pin can still be read, but a later interrupts module should implement the callback-based interrupt method properly.

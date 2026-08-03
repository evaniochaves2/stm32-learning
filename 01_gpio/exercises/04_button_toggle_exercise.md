# Exercise 04: Button Toggle and Debouncing

## Objective

Make each new B1 button press toggle LD2 and keep the selected LED state after the button is released.

## Required Behaviour

- First press: LD2 turns on and stays on
- Second press: LD2 turns off and stays off
- Later presses: LD2 alternates between on and off

## State Variable

Add this inside `USER CODE BEGIN PV`:

```c
GPIO_PinState previousButtonState = GPIO_PIN_RESET;
```

## Loop Logic

Add this inside `USER CODE BEGIN 3`:

```c
GPIO_PinState currentButtonState =
    HAL_GPIO_ReadPin(B1_GPIO_Port, B1_Pin);

if ((currentButtonState == GPIO_PIN_SET) &&
    (previousButtonState == GPIO_PIN_RESET))
{
  HAL_GPIO_TogglePin(LD2_GPIO_Port, LD2_Pin);
  HAL_Delay(50);
}

previousButtonState = currentButtonState;
```

## How It Works

The program compares the current and previous button states. It toggles LD2 only when the signal changes from RESET to SET. This is rising-edge detection in software and prevents a held button from continuously toggling the LED.

The 50 ms delay is a simple debounce measure. A mechanical button can produce several rapid electrical transitions during one physical press. The delay gives the contacts time to settle.

## Expected Result

Each distinct press changes LD2 once. Releasing the button does not change the LED.

## Test Record

- [x] State variable added in a protected user-code section
- [x] Project built successfully
- [x] Firmware programmed successfully
- [x] Each button press toggled LD2 once during testing
- [x] LD2 retained its state after button release

## Review Questions

1. Why store `previousButtonState`?  
   To detect a transition instead of responding continuously to a held level.

2. What problem does debounce address?  
   Mechanical contact bounce can look like several presses.

3. What is a limitation of `HAL_Delay(50)`?  
   It blocks the processor. A future non-blocking design can use `HAL_GetTick()`, a timer, or an interrupt-driven state machine.

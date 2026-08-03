# GPIO Cheat Sheet — STM32 NUCLEO-F446RE

## Core Idea

GPIO means **General-Purpose Input/Output**.

- Input: reads a digital signal.
- Output: drives a digital signal.
- STM32F446RE GPIO logic uses approximately 3.3 V for HIGH and 0 V for LOW.

## Onboard Hardware

| Component | Pin | Purpose |
|---|---|---|
| LD2 green LED | PA5 | GPIO output |
| B1 user button | PC13 | GPIO input / EXTI-capable pin |
| USART2 TX | PA2 | Alternate function |

## Output Modes

| Mode | HIGH behaviour | LOW behaviour | Common use |
|---|---|---|---|
| Push-pull | Actively drives HIGH | Actively drives LOW | LEDs and general outputs |
| Open-drain | Released; needs a pull-up | Actively drives LOW | I2C and shared lines |

## Input Bias

| Configuration | Default state | Key point |
|---|---|---|
| Floating | Undefined | May react to electrical noise |
| Pull-up | HIGH | External action commonly pulls it LOW |
| Pull-down | LOW | External action commonly drives it HIGH |

Always confirm whether a button is **active-high** or **active-low** from the board circuit or by testing. The electrical state and the meaning “pressed” are not automatically the same.

## Common HAL Calls

```c
HAL_GPIO_WritePin(LD2_GPIO_Port, LD2_Pin, GPIO_PIN_SET);
HAL_GPIO_WritePin(LD2_GPIO_Port, LD2_Pin, GPIO_PIN_RESET);

GPIO_PinState state = HAL_GPIO_ReadPin(B1_GPIO_Port, B1_Pin);

HAL_GPIO_TogglePin(LD2_GPIO_Port, LD2_Pin);
HAL_Delay(500);
```

## Three Completed Patterns

### Blink

```c
HAL_GPIO_TogglePin(LD2_GPIO_Port, LD2_Pin);
HAL_Delay(500);
```

### Direct button control

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

### Toggle using state-change detection

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

## CubeMX Configuration Used

| Item | Setting |
|---|---|
| PA5 / LD2 | Output push-pull |
| PA5 pull | No pull |
| PA5 speed | Low |
| PC13 / B1 | `GPIO_MODE_IT_FALLING` in generated board configuration |
| PC13 pull | No internal pull |

The toggle exercise polls PC13 even though CubeMX generated it as an EXTI-capable falling-edge input. Actual interrupt callbacks are saved for the interrupts module.

## Quick Checks

- Keep custom code inside `USER CODE BEGIN` / `USER CODE END` sections.
- Save before building.
- Successful build: `0 errors, 0 warnings`.
- Successful programming: `Download verified successfully`.
- Avoid floating inputs.
- Use a current-limiting resistor with an external LED.
- Never apply 5 V to a pin unless its datasheet specifically identifies that pin/configuration as 5 V tolerant.

# Exercise 02: LED Blink

## Objective

Configure the onboard LD2 LED as a GPIO output and toggle it every 500 ms.

## Hardware

- NUCLEO-F446RE
- LD2 green LED on PA5
- USB connection through ST-LINK

No external wiring is required.

## CubeMX Configuration

| Setting | Value |
|---|---|
| Pin | PA5 / LD2 |
| Mode | GPIO Output |
| Output type | Push-Pull |
| Pull | No Pull |
| Speed | Low |
| Initial level | Low |

## Coding Task

Add the following code inside the protected `USER CODE BEGIN 3` section of the infinite loop:

```c
HAL_GPIO_TogglePin(LD2_GPIO_Port, LD2_Pin);
HAL_Delay(500);
```

## How It Works

1. `HAL_GPIO_TogglePin()` changes LD2 to the opposite state.
2. `HAL_Delay(500)` pauses execution for 500 ms.
3. The infinite loop repeats the sequence continuously.

One complete on-off cycle takes approximately 1 second: 500 ms on and 500 ms off.

## Expected Result

- LD2 changes state every 500 ms.
- The LED continues blinking until the board is reset, disconnected, or reprogrammed.
- Red power and ST-LINK indicators may remain on normally.

## Test Record

- [x] Code generated successfully
- [x] Build completed with 0 errors and 0 warnings
- [x] Program downloaded and verified through ST-LINK
- [x] LD2 blink confirmed on the physical board

## Review Questions

1. Why is an infinite loop used?  
   Embedded firmware must continue running while the board is powered.

2. What changes if the delay becomes `1000`?  
   The LED holds each state for one second, producing a two-second complete cycle.

3. Why is PA5 configured as an output?  
   The microcontroller must drive the LED signal.

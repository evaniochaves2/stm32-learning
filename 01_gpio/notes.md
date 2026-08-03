# GPIO Study Notes

## What I Practiced

I completed the full STM32 development workflow with the NUCLEO-F446RE:

1. Selected the NUCLEO-F446RE in STM32CubeMX.
2. Reviewed PA5 (LD2), PC13 (B1), and generated peripheral settings.
3. Generated STM32CubeIDE projects.
4. Added application code inside the protected `USER CODE` sections.
5. Built each project with 0 errors and 0 warnings.
6. Programmed the board through the onboard ST-LINK interface.
7. Confirmed `Download verified successfully` and tested the hardware.

## GPIO Output Modes

### Push-Pull

Push-pull actively drives both HIGH and LOW. It is the usual choice for LEDs and general digital outputs. LD2 on PA5 was configured as push-pull, no pull, and low speed.

### Open-Drain

Open-drain actively drives LOW but releases the line for HIGH. A pull-up resistor produces the HIGH state. This is useful when multiple devices share a signal, as in I2C.

## GPIO Input Bias

### Floating

A floating input has no defined voltage and may change unpredictably because of electrical noise.

### Pull-Up

A pull-up establishes HIGH as the default state. A switch may then connect the signal to ground and produce LOW.

### Pull-Down

A pull-down establishes LOW as the default state. An external source or switch may then produce HIGH.

The meaning of “pressed” depends on how the button is wired. Firmware must compare the pin reading with the correct active level.

## Completed Projects

### 1. `01_gpio_led_blink`

- Toggled LD2 with `HAL_GPIO_TogglePin()`.
- Used `HAL_Delay(500)`.
- Result: 500 ms on and 500 ms off, giving a one-second complete cycle.

### 2. `02_gpio_led_button`

- Read B1 using `HAL_GPIO_ReadPin()`.
- Used `if` / `else` logic to write LD2 HIGH or LOW.
- Learned polling: the program repeatedly checks the input inside `while (1)`.

### 3. `03_gpio_led_toggle`

- Stored the previous and current button readings.
- Detected a RESET-to-SET state change.
- Toggled LD2 only when that transition occurred.
- Added `HAL_Delay(50)` as simple software debounce.
- Result: LD2 retained its state instead of changing continuously while the button was held.

## State and Edge Detection

A **state** is the pin's present level: SET or RESET. An **edge** is a transition between levels:

- Rising edge: RESET to SET.
- Falling edge: SET to RESET.

Comparing the current reading with the previous reading allows firmware to react once to a transition instead of repeatedly reacting to a held button.

## Button Bounce

A mechanical pushbutton may create several rapid electrical transitions when pressed or released. This is called bounce. The 50 ms delay used here is a simple beginner-friendly debounce method, but it blocks the processor during the delay. Later projects can use timers or non-blocking time checks.

## Generated Configuration Observations

- B1 was generated as `GPIO_MODE_IT_FALLING` with `GPIO_NOPULL`.
- The exercises read B1 by polling; no interrupt callback was implemented yet.
- LD2 was generated as `GPIO_MODE_OUTPUT_PP`, `GPIO_NOPULL`, and `GPIO_SPEED_FREQ_LOW`.
- USART2 was also initialized by the board project template, although UART was not used in the GPIO application logic.

## Practical Lessons

- CubeMX configures hardware and generates initialization code.
- CubeIDE edits, builds, programs, and debugs the firmware.
- ST-LINK is the onboard programmer/debugger interface.
- `Exit` after successful verification means the programming utility finished normally.
- Custom code belongs inside `USER CODE` sections so later code generation does not overwrite it.
- A successful build proves the code compiled; testing the board proves the behaviour works.

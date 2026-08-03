# GPIO Theory

## Introduction

GPIO (General-Purpose Input/Output) connects STM32 firmware to physical hardware. GPIO pins can read devices such as switches and digital sensors or control devices such as LEDs and enable signals.

## Digital Logic

Digital GPIO represents information with two states:

| Logical state | Typical STM32F446RE level |
|---|---|
| HIGH / SET / 1 | Approximately 3.3 V |
| LOW / RESET / 0 | Approximately 0 V |

A logic HIGH does not always mean a device is active. Hardware can be active-high or active-low, so firmware must account for the circuit's polarity.

## GPIO Operating Modes

| Mode | Purpose |
|---|---|
| Input | Read a digital voltage level |
| Output | Drive a digital voltage level |
| Alternate function | Connect the pin to a peripheral such as UART, SPI, I2C, or a timer |
| Analog | Connect the pin to analog circuitry and disable the digital input path |
| External interrupt/event | Detect selected signal transitions |

## Output Driver Types

### Push-Pull

Push-pull actively drives the pin HIGH and LOW. It is efficient for ordinary digital outputs such as LEDs and logic control signals.

### Open-Drain

Open-drain actively drives LOW but does not actively drive HIGH. When released, a pull-up resistor brings the line HIGH. This permits shared-line applications such as I2C.

## Input Biasing

### Floating Input

A floating input has no defined default voltage. It can react to electrical noise and produce unreliable readings.

### Pull-Up and Pull-Down Resistors

A pull resistor gives an otherwise undriven input a known default level:

| Bias | Default | Typical external action |
|---|---|---|
| Pull-up | HIGH | Connect the input to ground to produce LOW |
| Pull-down | LOW | Connect the input to 3.3 V to produce HIGH |

STM32 devices provide configurable internal pull resistors, but a board may also contain external components. The schematic and board configuration determine which is appropriate.

## Output Speed

STM32 GPIO output speed controls the pin's signal slew rate rather than application timing. Low speed is suitable for slowly changing signals such as an LED and can reduce noise and electromagnetic interference. A delay or timer controls how often firmware changes the output.

## Polling and Interrupts

### Polling

Polling repeatedly reads an input in the main loop. It is simple and was used for the button-control and toggle exercises.

### Interrupts

An external interrupt can notify the processor when a configured edge occurs. This avoids continuously checking the input, but it requires an interrupt configuration and callback or handler. Interrupt-driven GPIO will be covered separately in Module 04.

## Edges and State Tracking

| Term | Transition |
|---|---|
| Rising edge | RESET/LOW to SET/HIGH |
| Falling edge | SET/HIGH to RESET/LOW |

State tracking compares the present input with its previous value. It allows code to perform one action per transition instead of repeating the action while a button is held.

## Mechanical Button Debouncing

Mechanical contacts can briefly switch several times during a single press or release. This is called bounce. Common solutions include:

- A short blocking delay after detecting an edge.
- A non-blocking time threshold.
- Requiring several consistent readings.
- Hardware filtering.

The GPIO toggle exercise used a 50 ms blocking delay as an introductory software debounce.

## STM32 NUCLEO-F446RE Pins Used

| Board feature | MCU pin | Role in this module |
|---|---|---|
| LD2 green LED | PA5 | Push-pull digital output |
| B1 user button | PC13 | Digital input / EXTI-capable input |
| USART2 TX | PA2 | Alternate function generated with the board project |

## STM32 HAL GPIO Interface

The Hardware Abstraction Layer provides portable functions for common operations:

```c
HAL_GPIO_WritePin(GPIOx, GPIO_Pin, PinState);
HAL_GPIO_ReadPin(GPIOx, GPIO_Pin);
HAL_GPIO_TogglePin(GPIOx, GPIO_Pin);
```

`GPIO_PIN_SET` and `GPIO_PIN_RESET` represent the two digital states. `HAL_Delay()` creates a blocking millisecond delay; it is convenient for introductory exercises but is not ideal for applications that must perform other work concurrently.

## CubeMX-Generated Initialization

For the completed exercises, the generated `MX_GPIO_Init()` function:

1. Enabled the required GPIO port clocks.
2. Set LD2 to an initial RESET state.
3. Configured B1 as a falling-edge EXTI-capable input with no internal pull.
4. Configured LD2 as a low-speed push-pull output with no pull.

Even though B1 was generated in an interrupt-capable mode, the completed input exercises read it through polling. No interrupt callback was used.

## Safety and Reliability Notes

- Use a current-limiting resistor with an external LED.
- Keep input voltage within the limits specified in the MCU datasheet.
- Do not assume every STM32 pin is 5 V tolerant.
- Avoid shorting an output directly to power or ground.
- Establish a known level for inputs rather than leaving them floating.
- Check pin conflicts before assigning alternate functions.

## Key Takeaways

- GPIO configuration connects software intent to electrical behaviour.
- Inputs read; outputs drive; alternate functions connect peripherals.
- Push-pull and open-drain describe output electrical behaviour.
- Pull resistors prevent undefined input states.
- Polling reads repeatedly; edge detection responds to changes.
- Debouncing prevents one mechanical action from being interpreted as several.

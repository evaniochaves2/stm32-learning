# Changelog

All notable changes to this STM32 learning repository are documented here.

## [Unreleased]

### Planned

- Begin UART fundamentals and communication exercises
- Explore GPIO interrupts and improved non-blocking debouncing

## [2026-08-02] - GPIO Fundamentals Completed

### Added

- `01_gpio_led_blink` — toggles the onboard LD2 LED every 500 ms
- `02_gpio_led_button` — controls LD2 using the onboard B1 button
- `03_gpio_led_toggle` — toggles LD2 on each button press
- GPIO theory, notes, cheat sheet, exercises, and project documentation

### Learned

- GPIO input, output, and alternate-function modes
- Push-pull and open-drain outputs
- Pull-up, pull-down, and floating inputs
- GPIO polling and button-state reading
- Rising and falling edges
- State-change detection
- Basic 50 ms button debouncing
- STM32 HAL GPIO functions
- CubeMX pin configuration and code generation
- CubeIDE building and ST-LINK programming

### Verified

- All three GPIO projects built with zero errors and zero warnings
- Programs downloaded and verified successfully on the NUCLEO-F446RE
- Physical LED and button behaviour tested successfully
# rgb-led-controller

# High-Current RGB LED Controller (24V)

A compact (30.99 mm* 32.07 mm = <1000mm^2, high efficiency PWM controller designed to drive 24V RGB LED strips using logic-level mosfets.

## Specifications
- Input -> 24V - (IRLML6344 functions up to 30v)
- Control Logic -> 3.3v or 5v (micocontroller compatible) - (IRLML6344 functions up to 12v)
- Max Current -> 4A (per channel) - (limited by IRLML6344 Ip)
- Switching Frequency -> Tested up to 20kHz PWM

## Design Justification
- Trace widths:
    - Main power rails utilize 2mm traces. Based on IPC-2221 standards, this means that the traces can handle the max current of 4A.
    - Signal traces utilised 0.3mm traces, as they will not be carrying significant current (only control mosfet gates)

- Component selection:
    - IRLML6344
        - low gate threshold voltage - Vgs(th) - (0.5-1.1v), allowing it be driven with a 3.3v micocontroller signal without needing a gate driver.
        - Rated for Vds = 30v, providing a safe margin for 24v LEDs
        - Low on-resitance - Rds(on) = 29-37mΩ - minimises power dissipation, keeping the SOT-23 package cool when driving several amps of current
    - 100R Gate Resistor
        - Protects MCU GPIO by limiting peak current to (3.3V/100Ω=33mA)
    - 100K Pull-Down Resistor
        - Prevent floating GPIOs from causing the LEDs to flicker
        - 100K was chosen as a "weak" pull-down -> strong enough to bleed off charge but high enough to not wase significant power during operation
    - 100uF bulk electrolytic capacitor
        - Rated for 25V to ensure it can handle 24V load
        - Prevent voltage dips when switching
    - 100nF decoupling ceramic capacitor
        - Filter out high frequency noise from PWM switching -> ensures LED doesn't flicker

- Thermal managment: Added a large ground pour on the bottom layer, which will act as a heatsink for the SOT-23 mosfets.
    - SOT-23 Package can dissipate ≈ 1.25W
        - At 2A load, P = 2^2 * 0.037 = 0.148W -> design operates at a 8x safety factor regarding thermals
        - At 4A load, P = 4^2 * 0.037 = 0.592W -> design operates at a 2x safety factor regarding thermals

## Iteration and Improvements
<img width="1137" height="411" alt="PCB V1" src="https://github.com/user-attachments/assets/3f1e7a64-476e-4f86-9fef-bd87daad5408" />


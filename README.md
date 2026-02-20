# rgb-led-controller

# High-Current RGB LED Controller (24V)

A compact (<1000mm^2), high efficiency PWM controller designed to drive 24V RGB LED strips using logic-level mosfets.

## Specifications
- Input -> 24V - (IRLML6344 functions up to 30v)
- Control Logic -> 3.3v or 5v (micocontroller compatible) - (IRLML6344 functions up to 12v)
- Max Current -> 4A (per channel) - (limited by IRLML6344 Ip)
- Switching Frequency -> Tested up to 20kHz PWM

## Design Justification
- Trace widths: Main power rails utilize 2mm traces. Based on IPC-2221 standards, this means that the traces can handle the max current of 4A.
    - Signal traces utilised 0.3mm traces, as they will not be carrying significant current (only control mosfet gates)

- Component selection: I chose the IRLML6344 was chosen for its low gate threshold voltage (0.5-1.1v), allowing it be driven with a 3.3v micocontroller signal without needing a gate driver.

- Thermal managment: Added a large ground pour on the bottom layer, which will act as a heatsink for the SOT-23 mosfets. 

# UART_Project
Transmitter and Receiver
# UART Transmitter & Receiver in Verilog

**Part of my 100-day VLSI journey (Day X).**

## Features
- Standard UART protocol (8 data bits, 1 stop bit, no parity - 8N1).
- Configurable baud rate (currently set to 115200).
- Modular design: separate TX, RX, and Baud Generator.
- Self-checking testbench with automated verification.

## Tools Used
- Language: Verilog HDL
- Simulator: Icarus Verilog (iverilog)
- Waveform Viewer: GTKWave

## How to Simulate (Copy-paste these commands)
1. Clone the repo.
2. Navigate to the project folder.
3. Run these commands in your terminal:
   ```bash
   iverilog -o uart_sim rtl/*.v sim/testbench.v
   vvp uart_sim
   gtkwave dump.vcd

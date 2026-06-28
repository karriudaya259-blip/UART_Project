# UART — Universal Asynchronous Receiver Transmitter in Verilog

A complete UART implementation in Verilog — both transmitter (TX) and receiver (RX) — with configurable baud rate, testbenches, and GTKWave waveform verification.

**Tools:** Icarus Verilog · GTKWave  
**Language:** Verilog HDL  
**Protocol:** UART — 8N1 (8 data bits, no parity, 1 stop bit)

---

## 📡 What is UART?

UART is a serial communication protocol that transmits data bit by bit over a single wire. It is widely used in embedded systems, microcontrollers, and FPGAs to communicate between devices without a shared clock — making it asynchronous.

**Frame format (8N1):**
```
[START bit] [D0 D1 D2 D3 D4 D5 D6 D7] [STOP bit]
```

---

## 🏗️ Modules

### `uart_tx.v` — Transmitter
- Serializes 8-bit parallel data into a single TX line
- Sends: Start bit → 8 data bits (LSB first) → Stop bit
- Baud rate controlled by clock divider
- `tx_done` flag asserted when transmission completes

| Port | Direction | Description |
|---|---|---|
| `clk` | Input | System clock |
| `rst` | Input | Active-high reset |
| `tx_start` | Input | Start transmission |
| `tx_data[7:0]` | Input | 8-bit data to transmit |
| `tx` | Output | Serial TX line |
| `tx_done` | Output | High when transmission complete |

### `uart_rx.v` — Receiver
- Detects start bit on RX line
- Samples each data bit at the center of the baud period
- Deserializes bits into 8-bit parallel output
- `rx_done` flag asserted when full byte received

| Port | Direction | Description |
|---|---|---|
| `clk` | Input | System clock |
| `rst` | Input | Active-high reset |
| `rx` | Input | Serial RX line |
| `rx_data[7:0]` | Output | Received 8-bit data |
| `rx_done` | Output | High when byte received |

### `uart_tx_tb.v` / `uart_rx_tb.v` — Testbenches
- Drives TX with test data bytes
- Monitors and verifies output waveforms
- Dumps VCD for GTKWave analysis

---

## 📊 Waveform

Simulation verified in GTKWave:
- TX line shows correct start bit, 8 data bits (LSB first), stop bit
- RX correctly samples and reconstructs the transmitted byte
- `tx_done` and `rx_done` flags toggle as expected

---

## 🛠️ How to Simulate

```bash
# Simulate TX
iverilog -o uart_tx.vvp uart_tx.v uart_tx_tb.v
vvp uart_tx.vvp
gtkwave uart_tx.vcd

# Simulate RX
iverilog -o uart_rx.vvp uart_rx.v uart_rx_tb.v
vvp uart_rx.vvp
gtkwave uart_rx.vcd
```

---


## 🔗 Links

- 📂 [Full Verilog Portfolio](https://jyoshnakarri.github.io/Verilog_Codes/)
- 📂 [100 Days VLSI Journey](https://github.com/jyoshnakarri/100-days-vlsi)
- 💼 [LinkedIn](https://www.linkedin.com/in/jyoshna-k-5b1626401/)

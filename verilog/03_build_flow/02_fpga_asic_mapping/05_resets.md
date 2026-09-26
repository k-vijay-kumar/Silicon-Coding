# Resets

A reset in a clocked process describes how state responds to reset assertion.

- **FPGA:** Synthesis may use available flip-flop set/reset resources or implement reset logic around state elements.
- **ASIC:** Synthesis may select reset-capable flip-flop cells from the library.

Reset polarity, synchrony, fanout, and target-cell support affect the implementation. Check synthesis reports and device documentation.
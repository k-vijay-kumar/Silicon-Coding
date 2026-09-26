# Combinational Logic

For `assign out = (a & b) | c;`, synthesis implements the Boolean function using the target's logic resources.

- **FPGA:** The function may map to a lookup table (LUT). On the Tang Nano 9K, the Gowin flow targets the device's LUT resources; inspect the synthesis report for the actual mapping.
- **ASIC:** The function maps to cells from the selected standard-cell library, such as AND and OR gates.

Mapping depends on optimization, constraints, and the target device or library.
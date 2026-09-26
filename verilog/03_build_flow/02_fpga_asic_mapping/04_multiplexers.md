# Multiplexers

A conditional expression such as `assign out = select ? b : a;` describes selection logic.

- **FPGA:** The function may map into LUTs or dedicated mux resources.
- **ASIC:** It may map to a mux cell or equivalent standard-cell logic.

The exact implementation is chosen by synthesis and physical-design tools.
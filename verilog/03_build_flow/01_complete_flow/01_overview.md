# Complete Build Flow Overview

A Verilog project can target physical hardware or run as a simulation. Both may use synthesizable RTL, but their source sets, tools, and outputs differ.

## Common Design Inputs

- Synthesizable RTL modules and the selected design top.
- Parameters, macros, and included files needed to configure the design.
- Target constraints, such as clocks, pins, I/O standards, or timing requirements.
- For simulation: a testbench, models, and test data.

Lint, review, simulation, synthesis, and implementation checks find different classes of problems; none replaces all the others.

## Flow Pages

- [FPGA hardware flow](02_fpga_hardware_flow.md)
- [ASIC hardware flow](03_asic_hardware_flow.md)
- [Simulation build and run flow](04_simulation_build_and_run_flow.md)
- [Outputs and validation](05_outputs_and_validation.md)

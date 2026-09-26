# FPGA Hardware Flow

```text
Synthesizable RTL + FPGA device + constraints
    -> elaborate and synthesize
    -> map logic to FPGA resources
    -> place and route
    -> timing and design checks
    -> generate bitstream
    -> program FPGA and test on board
```

1. **Select the target:** Choose the FPGA part and provide timing, pin, and I/O constraints.
2. **Elaborate:** Resolve the top module, parameters, generate blocks, and hierarchy.
3. **Synthesize:** Convert synthesizable RTL into a generic logic representation and optimize it.
4. **Map:** Fit logic and state into LUTs, flip-flops, memories, DSP blocks, and I/O resources where available.
5. **Place and route:** Assign mapped resources to physical locations and connect them using programmable routing.
6. **Analyze:** Check timing, constraints, and implementation reports; revise RTL or constraints if requirements are not met.
7. **Generate the bitstream:** Create the device configuration image.
8. **Test on hardware:** Program the FPGA and validate behavior with real I/O and operating conditions.

Tool stages and names vary by FPGA vendor.
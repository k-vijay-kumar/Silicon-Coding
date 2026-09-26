# Sequential Storage

A clocked process such as `always @(posedge clk) q <= d;` describes edge-triggered state.

- **FPGA:** State typically maps to flip-flops in logic blocks, connected through programmable routing.
- **ASIC:** State typically maps to flip-flop cells from the standard-cell library.

The selected resources and timing depend on the target and synthesis constraints.
# Combinational Blocks

`always @(*)` reevaluates the block when a read signal changes. Blocking assignments (`=`) are commonly used for combinational logic.

```verilog
always @(*) begin
    result = 1'b0;
    if (enable)
        result = a & b;
end
```

Assign outputs on every path to avoid inferring a latch. `always_comb` is available in SystemVerilog.
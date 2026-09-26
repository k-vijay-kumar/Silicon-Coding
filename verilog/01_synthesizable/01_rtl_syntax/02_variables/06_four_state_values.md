# Four-State Values

Verilog signals can hold `0`, `1`, `x` (unknown), or `z` (high impedance). Unknown values often reveal uninitialized state, conflicting drivers, or incomplete simulation models.

```verilog
reg [3:0] value;
initial $display("value=%b", value); // x before the variable is assigned
```

`z` is mainly meaningful at tri-state boundaries; it is not a general internal FPGA logic value. Do not assume simulation `x` or `z` corresponds to a particular physical voltage.
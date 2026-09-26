# Conditional Operator

The `?:` operator selects one of two expressions based on a condition and commonly describes a mux.

```verilog
wire selected;
assign selected = choose_b ? b : a;
```

The true expression follows `?`; the false expression follows `:`.
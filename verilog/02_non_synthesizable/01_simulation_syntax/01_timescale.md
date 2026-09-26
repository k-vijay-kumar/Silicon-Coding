# Timescale

The `` `timescale `` directive sets the time unit and precision for a Verilog module or compilation unit, subject to tool and language rules.

```verilog
`timescale 1ns / 1ps
```

A delay of `#5` is five time units. Precision controls how delay values are rounded. SystemVerilog also provides `` `timeunit `` and `` `timeprecision `` declarations.
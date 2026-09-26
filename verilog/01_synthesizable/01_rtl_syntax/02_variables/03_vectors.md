# Vectors

A packed vector groups bits into one signal. A common convention is to number from the most significant bit down to bit zero.

```verilog
wire [7:0] data;
reg  [3:0] nibble;
```

`[7:0]` contains eight bits. Use parameters for widths that need to vary.
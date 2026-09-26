# Fixed Part-Selects

A fixed part-select extracts a compile-time-known range from a vector.

```verilog
wire [7:0] data;
wire [3:0] high_nibble;
assign high_nibble = data[7:4];
```

The selected width is `msb - lsb + 1` for a descending range.
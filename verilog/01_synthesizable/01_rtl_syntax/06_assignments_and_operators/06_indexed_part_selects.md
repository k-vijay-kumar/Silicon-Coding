# Indexed Part-Selects

Indexed part-selects use a variable base and a fixed width. They are useful for selecting a moving window from a vector.

```verilog
wire [15:0] data;
wire [3:0] nibble;
assign nibble = data[start_index +: 4];
```

`+:` selects upward from the base; `-:` selects downward. The width must be constant.
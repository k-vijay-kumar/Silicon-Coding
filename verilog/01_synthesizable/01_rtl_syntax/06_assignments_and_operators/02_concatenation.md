# Concatenation

Curly braces join signals or bit slices into a wider vector.

```verilog
wire [9:0] packet;
assign packet = {header, payload};
```

The leftmost item becomes the most significant part. The destination width must match the combined width.
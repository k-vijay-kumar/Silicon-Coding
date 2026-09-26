# Signed Casts

`$signed(expression)` treats an expression as signed for operations where signed interpretation is needed.

```verilog
wire signed [7:0] signed_value;
wire [7:0] raw_value;
assign signed_value = $signed(raw_value);
```

Casting does not change the bit pattern. Mixed-width and mixed-signedness expressions still need deliberate sizing.
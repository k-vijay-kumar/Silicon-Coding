# Signed Values

Declare a vector `signed` when arithmetic should interpret it as two's-complement.

```verilog
reg signed [7:0] temperature;
wire signed [15:0] offset;
```

Signedness affects expression sizing and extension. Check mixed signed and unsigned expressions explicitly.
# Arithmetic Sizing

Verilog expression width and signedness depend on the operands and expression context. Do not assume an addition always produces a carry bit or that a destination automatically preserves every product bit.

```verilog
wire [7:0] a, b;
wire [8:0] sum;
assign sum = {1'b0, a} + {1'b0, b};
```

Extend operands explicitly when the design needs extra result bits. Check the language version and tool rules for more complex expressions.
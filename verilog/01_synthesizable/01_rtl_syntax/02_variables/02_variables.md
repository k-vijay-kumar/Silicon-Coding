# Variables

In Verilog, `reg` is a procedural variable type. It does not by itself mean a flip-flop: the assignments and process determine the hardware inferred.

```verilog
reg result;

always @(*) begin
    result = left & right;
end
```

A complete assignment in every combinational path avoids inferring a latch.
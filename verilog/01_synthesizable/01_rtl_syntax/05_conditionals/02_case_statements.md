# Case Statements

`case` selects a branch by matching the expression against its alternatives.

```verilog
always @(*) begin
    case (mode)
        2'b00: result = a;
        2'b01: result = b;
        default: result = 1'b0;
    endcase
end
```

Provide complete assignments, including a `default`, in combinational logic to avoid unintended latches.
# If and Else

Use `if` and `else` to select behavior based on a condition.

```verilog
always @(*) begin
    if (enable)
        result = data_in;
    else
        result = 8'b0;
end
```

Assign a value on every path in combinational logic to avoid inferring a latch. Use `else if` for additional mutually exclusive conditions.
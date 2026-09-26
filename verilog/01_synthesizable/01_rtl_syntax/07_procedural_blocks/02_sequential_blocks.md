# Sequential Blocks

A clock edge in the sensitivity list describes edge-triggered behavior. Nonblocking assignments (`<=`) are standard for clocked state updates.

```verilog
always @(posedge clk or negedge rst_n) begin
    if (!rst_n)
        count <= 8'b0;
    else
        count <= count + 1'b1;
end
```

The asynchronous reset shown is active-low. Omit reset edges when the design does not require an asynchronous reset.
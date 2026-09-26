# Clock Enables and Resets

Use a clock enable to update state only when work is needed. This generally keeps the design on its intended clock rather than creating a gated clock in RTL.

```verilog
always @(posedge clk) begin
    if (!rst_n)
        count <= 8'b0;
    else if (enable)
        count <= count + 1'b1;
end
```

This example describes a synchronous active-low reset because `rst_n` is tested only at the rising clock edge. An asynchronous reset instead appears in the sensitivity list, for example `@(posedge clk or negedge rst_n)`. Choose reset style to match the target flow; asynchronous reset deassertion often needs synchronization to the destination clock. Avoid using data signals as clocks.
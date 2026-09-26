# Race Example

A `$display` in the Active region can see the old value before a nonblocking update; `$strobe` sees the settled value at the end of the time step.

```verilog
always @(posedge clk) begin
    q <= d;
    $display("active q=%b", q);
    $strobe("settled q=%b", q);
end
```

If `q` starts as `x` and `d` is `1`, the display can print `x` while the strobe prints `1`. Avoid depending on process order within the Active region.
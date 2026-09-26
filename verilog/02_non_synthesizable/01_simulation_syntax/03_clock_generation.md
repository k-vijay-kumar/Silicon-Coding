# Clock Generation

A testbench can generate a periodic clock with an `initial` process and `forever` loop.

```verilog
initial begin
    clk = 1'b0;
    forever #5 clk = ~clk;
end
```

With a `1ns` time unit, this creates a 10 ns period (100 MHz). A zero-delay forever loop prevents simulation time from advancing.
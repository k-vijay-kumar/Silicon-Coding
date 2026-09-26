# NBA Region

For a nonblocking assignment, the right-hand side is evaluated when the statement executes; the left-hand side update is scheduled for the NBA region.

```verilog
always @(posedge clk)
    q <= d;
```

This lets clocked processes observe old state while updates are applied together. Changes can trigger more evaluation in the same simulation time slot.
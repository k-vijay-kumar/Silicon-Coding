# Initial Blocks

An `initial` process starts once at simulation time zero and runs its statements in order.

```verilog
initial begin
    reset_n = 1'b0;
    #10 reset_n = 1'b1;
end
```

This is commonly used for testbench setup and stimulus. It is not a general synthesizable RTL process.
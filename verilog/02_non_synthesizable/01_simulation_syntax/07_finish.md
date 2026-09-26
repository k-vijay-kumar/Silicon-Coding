# Finish

`$finish` ends the simulation and returns control to the simulator or command line.

```verilog
initial begin
    #100;
    $finish;
end
```

Use it to stop a testbench after its checks or stimulus complete.
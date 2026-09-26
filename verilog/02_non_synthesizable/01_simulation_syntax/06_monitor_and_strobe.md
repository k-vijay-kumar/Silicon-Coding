# Monitor and Strobe

`$monitor` prints when a listed argument changes; `$strobe` prints once at the end of the current time step.

```verilog
$monitor("time=%t data=%h", $time, data);
$strobe("settled data=%h", data);
```

`$strobe` is useful when output should reflect updates scheduled in the current time step, including nonblocking assignments.
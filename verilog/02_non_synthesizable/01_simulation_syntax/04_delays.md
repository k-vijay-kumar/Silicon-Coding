# Delays

The `#` delay suspends the current procedural process for the specified simulation time.

```verilog
#10 signal = 1'b1;
#5;
```

The values use the current time unit and are rounded to the configured precision. Delay controls are generally for simulation, not portable synthesizable timing.
# Synthesizable Functions

A function returns a value and can factor out combinational calculations.

```verilog
function [7:0] times_three;
    input [7:0] value;
    begin
        times_three = (value << 1) + value;
    end
endfunction
```

In classic Verilog, functions complete without simulation time controls and cannot contain timing delays. Keep the function purely combinational and check language-version rules for function features.
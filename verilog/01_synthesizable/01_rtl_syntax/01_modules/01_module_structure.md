# Module Structure

A module defines a hardware block and its interface.

```verilog
module counter (
    input wire clk,
    output reg [7:0] count
);
    // RTL goes here
endmodule
```

Each module starts with `module` and ends with `endmodule`. Parameters and ports can be added to the header.
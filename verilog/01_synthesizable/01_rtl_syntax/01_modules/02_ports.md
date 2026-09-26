# Ports

ANSI-style ports declare direction, type, and width in the module header.

```verilog
module byte_unit (
    input  wire       clk,
    input  wire [7:0] data_in,
    output reg  [7:0] data_out,
    inout  wire       io_pin
);
endmodule
```

Use `input`, `output`, or `inout` for direction. Choose net or variable types to match how each port is driven.
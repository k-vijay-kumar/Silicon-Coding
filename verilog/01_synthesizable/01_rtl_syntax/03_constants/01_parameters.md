# Parameters

Parameters configure a module at elaboration time. `localparam` is a derived constant that cannot be overridden by an instantiating module.

```verilog
module fifo #(parameter ADDR_WIDTH = 4) ();
    localparam DEPTH = 1 << ADDR_WIDTH;
endmodule
```

Use parameters for configurable dimensions; use local parameters for internal constants.
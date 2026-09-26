# Behavioral Coding Style

Behavioral Style (Procedural Block Syntax Flow)

Objective: Describe hardware behavior with procedural statements. Combinational processes describe logic; clocked processes describe state.

```verilog
// 2-to-1 Multiplexer: Behavioral Procedural Implementation
module behavioral_mux (
    input  wire a,      // Input data channel 0
    input  wire b,      // Input data channel 1
    input  wire sel,    // Binary control select line
    output reg  out     // Verilog procedural variable; SystemVerilog may use logic
);

    // Procedural Sensitivity Flow
    // The simulator schedules this process when a, b, or sel changes.
    always @(*) begin
        
        // Assign a value on every path to describe combinational logic.
        if (sel) begin
            out = b;    // Use BLOCKING assignment '=' for combinational logic
        end else begin
            out = a;    // Use BLOCKING assignment '=' for combinational logic
        end
        
    end

endmodule
```

In Verilog, a signal assigned procedurally is declared as `reg`. This describes a variable type, not necessarily a physical register. In SystemVerilog, `logic` is commonly used for this purpose.
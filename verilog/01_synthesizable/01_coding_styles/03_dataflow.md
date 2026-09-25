# Dataflow Coding Style

Dataflow Style (Continuous Assignment Syntax Flow)

Objective: Model hardware by defining the Boolean or algebraic equations of the system. This describes how data flows and transforms dynamically through nets.


// 2-to-1 Multiplexer: Dataflow Boolean Implementation
module dataflow_mux (
    input  wire a,      // Input data channel 0
    input  wire b,      // Input data channel 1
    input  wire sel,    // Binary control select line
    output wire out     // Combinational output net
);

    // Continuous Assignment Flow using Explicit Boolean Expressions
    // This evaluates instantly whenever any signal on the right side changes value.
    assign out = (~sel & a) | (sel & b); 

endmodule
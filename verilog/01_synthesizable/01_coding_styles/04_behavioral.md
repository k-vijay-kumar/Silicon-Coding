# Behavioral Coding Style

Behavioral Style (Procedural Block Syntax Flow)

Objective: Model hardware algorithmically over time using sequential or software-like logical evaluation branches.

// 2-to-1 Multiplexer: Behavioral Procedural Implementation
module behavioral_mux (
    input  wire a,      // Input data channel 0
    input  wire b,      // Input data channel 1
    input  wire sel,    // Binary control select line
    output reg  out     // MUST be declared as a 'reg' type because it is assigned in an always block
);

    // Procedural Sensitivity Flow
    // always @(*) triggers instantly on any change of input variables (a, b, sel)
    always @(*) begin
        
        // Software-like conditional decision structure
        if (sel) begin
            out = b;    // Use BLOCKING assignment '=' for combinational logic
        end else begin
            out = a;    // Use BLOCKING assignment '=' for combinational logic
        end
        
    end

endmodule
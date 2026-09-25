# Structural Coding Style

Structural Style (Gate-Level Syntax Flow)

Objective: Map hardware explicitly using raw primitive logic gates. This style directly mirrors a physical circuit schematic.

// 2-to-1 Multiplexer: Structural Primitive Implementation
module structural_mux (
    input  wire a,      // Input data channel 0
    input  wire b,      // Input data channel 1
    input  wire sel,    // Binary control select line
    output wire out     // Combinational output net
);
    // 1. Internal Structural Interconnects (Physical Wires)
    wire sel_n;         // Inverted select signal connection
    wire a_gated;       // Output of the channel A routing gate
    wire b_gated;       // Output of the channel B routing gate

    // 2. Gate Primitive Instantiations
    // Built-in Syntax: gate_type instance_name (output, input1, input2, ...);
    not u_inv  (sel_n, sel);              // Inverts select line
    and u_and1 (a_gated, a, sel_n);       // Evaluates Channel A route
    and u_and2 (b_gated, b, sel);         // Evaluates Channel B route
    or  u_or   (out, a_gated, b_gated);   // Combines channels to output
    
endmodule
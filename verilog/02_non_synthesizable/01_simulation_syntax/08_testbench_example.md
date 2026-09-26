# Self-Checking Testbench

A self-checking testbench instantiates the design under test (DUT), applies inputs, and compares outputs against expected values.

```verilog
`timescale 1ns / 1ps

module mux2 (
    input  wire a,
    input  wire b,
    input  wire sel,
    output wire y
);
    assign y = sel ? b : a;
endmodule

module tb;
    reg a, b, sel;
    reg expected;
    wire y;
    integer vector, errors;

    mux2 dut (.a(a), .b(b), .sel(sel), .y(y));

    initial begin
        errors = 0;
        for (vector = 0; vector < 8; vector = vector + 1) begin
            {sel, a, b} = vector;
            expected = sel ? b : a;
            #1;
            if (y !== expected) begin
                $display("FAIL: sel=%b a=%b b=%b y=%b expected=%b",
                         sel, a, b, y, expected);
                errors = errors + 1;
            end
        end

        if (errors == 0)
            $display("PASS: all mux input combinations checked");
        else
            $display("FAIL: %0d mismatches", errors);

        $finish;
    end
endmodule
```

Case inequality (`!==`) makes unknown or high-impedance DUT outputs fail the check instead of silently passing. Testbenches are simulation code and are not synthesized into the hardware DUT.
# Synthesizable RTL Edge Cases

## 1. Tri-State Buses (High Impedance Layout)

### A. Bidirectional Buffering
#### Formal Syntax Template
```verilog
assign io_pin = (drive_enable) ? data_out : 1'bz;
```
#### Component Breakdown
* **`1'bz`**: Directs the compiler to float the line by turning off the output driving transistors.
* *Synthesis Rule:* High impedance (`z`) can only exist on **external I/O boundary pins** of the FPGA. You **cannot** use internal tri-state buses inside the FPGA fabric. The compiler will reject internal `z` connections or convert them into broken multiplexer logic.

## 2. Full-Case vs. Parallel-Case Control

### A. Parallel Case Attribute (The Priority Encoder Killer)
#### Formal Syntax Template
```verilog
(* parallel_case *) 
case (expression)
    // Branch blocks
endcase
```
#### Component Breakdown
* **`(* parallel_case *)`**: A compiler directive telling the synthesizer that **only one branch condition can ever be true at any given moment**.
* **Circuit Impact:** Normally, if your branch conditions overlap, Verilog builds a slow, cascading chain of multiplexers called a **Priority Encoder**. Applying this attribute forces the compiler to disable that priority checking loop and build a **fast, flat parallel multiplexer** instead.

### B. Full Case Attribute (The Latch Prevention Override)
#### Formal Syntax Template
```verilog
(* full_case *) 
case (expression)
    // Branch blocks without a default statement
endcase
```
#### Component Breakdown
* **`(* full_case *)`**: A compiler directive telling the synthesizer that **every single possible value combination of the expression has been completely accounted for**, even if you skipped the `default` branch.
* **Circuit Impact:** Normally, if you leave out a possible binary combination in a combinational block, the compiler thinks you want to remember the old value and creates a highly destructive storage bug called an **accidental Latch**. This attribute forces the compiler to ignore the missing options and skip creating a latch.
* *Best Practice Warning:* **Avoid `(* full_case *)` in real projects.** If your software simulator treats the missing states as unknown (`x`) but your synthesis compiler forces them to be constants because of this attribute, you create a **Simulation-Synthesis Mismatch**. Always use an explicit `default:` branch instead!

## 3. Function Declarations (Pure Combinational Blocks)

### A. Synthesizable Functions
#### Formal Syntax Template
```verilog
function [MSB:LSB] function_name;
    input [MSB:LSB] input_argument;
    begin
        procedural_statements;
        function_name = execution_result;
    end
endfunction
```
#### Component Breakdown
* **`function`**: Creates a reusable chunk of code that returns a single value. Functions synthesize **strictly into combinational logic gates**.
* *Strict Syntax Rules:* Inside an RTL function, you **cannot** use clocks (`posedge`), you **cannot** use non-blocking assignments (`<=`), and you **cannot** invoke other modules. You must only use blocking `=` math assignments.

## Isolated Code Example (Tri-States, Attributes, and Functions)

```verilog
module final_edge_cases (
    inout  wire       sda_pin,       // Bidirectional I2C Data Pin
    input  wire       drive_en,
    input  wire       data_bit,
    input  wire [1:0] selector,
    output reg  [7:0] computed_out
);

    // 1. Bidirectional / Tri-State Pin Driver Architecture
    assign sda_pin = (drive_en) ? data_bit : 1'bz;

    // 2. Synthesizable Function Example (Combinational Multiplier by 3)
    function [7:0] multiply_by_three;
        input [7:0] val;
        begin
            multiply_by_three = (val << 1) + val; // (val*2) + val = val*3
        end
    endfunction

    // 3. Parallel Control Evaluation Structure
    always @(*) begin
        computed_out = 8'h00; // Default Latch Avoidance Baseline
        
        (* parallel_case *) // Modern attribute format enforcing parallel evaluation
        case (selector)
            2'b01: computed_out = multiply_by_three(8'd10); // Returns 30
            2'b10: computed_out = multiply_by_three(8'd20); // Returns 60
            default: computed_out = 8'h00;
        endcase
    end

endmodule
```

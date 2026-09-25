# Advanced Synthesizable RTL Mechanics

## 1. Inter-Module Structural Connections

### A. Named Port Instantiation
#### Formal Syntax Template
```verilog
module_name #(
    .PARAMETER_NAME (compile_time_constant)
) instance_name (
    .port_name_inside_submodule (local_wire_or_reg),
    .port_name_inside_submodule (local_wire_or_reg)
);
```
#### Component Breakdown
* **`.port_name(...)`**: Connection by name. Explicitly binds the internal pin of the sub-module to a local signal wire in the top module. 
* *Design Rule:* **Never use positional connection** (`instance (a, b, c)`). If you alter the port order inside the sub-module later, positional binding will silently miswire your hardware inputs and outputs without throwing a compiler error.

## 2. Mathematical Operands & Arithmetic Synthesis

### A. The Bit-Width Expansion Rule
#### Architectural Evaluation Rules
* **Addition/Subtraction (`+`, `-`)**: The intermediate bit-width of an addition operation matches the width of the largest operand plus **1 extra carry bit**.
* **Multiplication (`*`)**: Synthesizes directly into physical hardware multipliers or LUT cascades. The resulting bit-width is always equal to **the sum of both operand widths** (e.g., an 8-bit multiplied by a 4-bit requires a 12-bit output register to prevent truncation).

## 3. Bit-Slicing & Dynamic Indexing

### A. Fixed vs. Variable Part-Select Vector Slicing
#### Formal Syntax Template
```verilog
vector_name [constant_msb : constant_lsb]; // Standard Fixed Slice
vector_name [base_index   +: width_constant]; // Positive Indexed Part-Select
vector_name [base_index   -: width_constant]; // Negative Indexed Part-Select
```
#### Component Breakdown
* **`+:`**: Starts at a dynamic `base_index` variable and selects a fixed number of bits upward.
* **`-:`**: Starts at a dynamic `base_index` variable and selects a fixed number of bits downward.
* *Synthesis Rule:* In pure Verilog, you **cannot** use a variable for both indices (like `vector[a:b]`) because the compiler cannot determine the physical width of the bus at compile time. The width factor (`width_constant`) **must be a hardcoded number or parameter**.

#### Isolated Code Example (Connections, Math, and Slicing)
```verilog
module top_level_unit (
    input  wire [7:0] byte_in,
    input  wire [2:0] shift_index,
    output wire [15:0] math_out
);
    wire [3:0] upper_nibble;
    wire [3:0] dynamic_nibble;

    // 1. Fixed Part-Select Slicing
    assign upper_nibble = byte_in[7:4]; 

    // 2. Dynamic Variable Part-Select (+: matches width 4)
    assign dynamic_nibble = byte_in[shift_index +: 4]; 

    // 3. Structural Module Instantiation by Name
    // Multiplies dynamic_nibble (4 bits) by upper_nibble (4 bits) -> Requires 8 bits
    wire [7:0] mult_result;
    sub_multiplier u_multiplier (
        .operand_a (dynamic_nibble),
        .operand_b (upper_nibble),
        .product   (mult_result)
    );

    // 4. Bit-Width Arithmetic Expansion (8 bits + 8 bits = 9 bits capacity)
    assign math_out = {8'h00, mult_result} + 16'd25;

endmodule
```

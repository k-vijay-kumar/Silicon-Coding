# Synthesizable RTL Syntax Blueprint

## 1. Module Structure & Configuration

### A. Parameter Declarations
#### Formal Syntax Template
```verilog
parameter IDENTIFIER = DEFAULT_VALUE;
localparam IDENTIFIER = DERIVED_VALUE;
```
#### Component Breakdown
* **`parameter`**: A keyword declaring a constant that can be overridden during module instantiation or via a `defparam` statement.
* **`localparam`**: A keyword declaring a purely local constant. It cannot be altered by higher-level modules during instantiation.
* **`IDENTIFIER`**: The user-defined naming variable (conventionally in UPPERCASE).
* **`DEFAULT_VALUE` / `DERIVED_VALUE`**: The default numeric constant or compile-time mathematical expression assigned to the parameter.

### B. ANSI-C Style Port Format
#### Formal Syntax Template
```verilog
module module_name #(
    // Parameter List
)(
    DIRECTION TYPE [MSB:LSB] PORT_NAME,
    DIRECTION TYPE           PORT_NAME
);
```
#### Component Breakdown
* **`DIRECTION`**: Must be specified as `input`, `output`, or `inout`.
* **`TYPE`**: Specifies the data type driver. Synthesizable types are `wire` or `reg`. If omitted, the default type defaults to `wire`.
* **`[MSB:LSB]`**: The bus bit-width index configuration (Most Significant Bit to Least Significant Bit).
* **`PORT_NAME`**: The unique identifier for the connection terminal pin.

#### Isolated Code Example (Module & Ports)
```verilog
module full_synthesizable_unit #(
    parameter DATA_WIDTH = 8,             
    parameter ADDR_WIDTH = 4,             
    localparam MEM_DEPTH = 1 << ADDR_WIDTH 
)(
    input  wire                  clk,      
    input  wire                  rst_n,    
    input  wire                  en,       
    input  wire [DATA_WIDTH-1:0] data_in,  
    output reg                   valid,    
    output reg  [DATA_WIDTH-1:0] data_out  
);
    // Real physical circuit logic is instantiated here
endmodule
```

## 2. Signal & Data Type Declarations

### A. Scalar Net and Register Declarations
#### Formal Syntax Template
```verilog
wire identifier_name;
reg  identifier_name;
```
#### Component Breakdown
* **`wire`**: A hardware net type representing a structural data connection. It does not store values and must be driven continuously.
  * *Default Simulation Value:* **`z`** (High Impedance / Tri-stated / Floating). If a wire has no active driving source, it floats electronically.
  * *Physical Hardware Mapping:* Maps to a physical metal connection track or routing trace. In real FPGA silicon, an undriven wire acts as a floating antenna, capturing electrical noise and snapping arbitrarily to `0` or `1`.
* **`reg`**: A procedural variable type that retains its value from one procedural assignment to the next.
  * *Default Simulation Value:* **`x`** (Unknown / Uninitialized state). The simulator flags this variable as undefined at timestamp zero until an assignment occurs.
  * *Physical Hardware Mapping:* Maps to a physical storage element (like a D Flip-Flop) *only* if driven inside a sequential procedural block. Upon FPGA power-up, physical hardware cannot remain "unknown"; it will randomly snap to a stable `0` or `1` state based on microscopic silicon variations, making an explicit hardware reset network (`rst_n`) essential.

### B. Vector Declarations (Buses)
#### Formal Syntax Template
```verilog
wire [MSB:LSB] identifier_name;
reg  [MSB:LSB] identifier_name;
```
#### Component Breakdown
* **`[MSB:LSB]`**: Bounding indices. In synthesizable RTL, this uses a countdown convention where `MSB = Width - 1` and `LSB = 0` (e.g., `[7:0]` for an 8-bit bus).

### C. Signed Declarations
#### Formal Syntax Template
```verilog
wire signed [MSB:LSB] identifier_name;
reg  signed [MSB:LSB] identifier_name;
```
#### Component Breakdown
* **`signed`**: An optional modifier keyword that alters the internal math engine logic. The compiler interprets values as two's complement arithmetic rather than unsigned binary.

### D. 2D Memory Array Declarations
#### Formal Syntax Template
```verilog
reg [BIT_MSB:BIT_LSB] array_name [ARRAY_START:ARRAY_END];
```
#### Component Breakdown
* **`[BIT_MSB:BIT_LSB]`**: Defines the bit-width of each individual memory word slot.
* **`[ARRAY_START:ARRAY_END]`**: Defines the total addressable address depth allocation of the memory block.

#### Isolated Code Example (Data Types)
```verilog
wire        net_scalar;       
reg         reg_scalar;       
wire [7:0]  net_vector;       
reg  [31:0] reg_vector;       
wire signed [15:0] signed_net; 
reg  signed [15:0] signed_reg; 
reg [7:0] internal_ram [0:15]; // Holds 16 individual 8-bit elements
```

## 3. Continuous Assignments & Operators

### A. Continuous Assignment Syntax
#### Formal Syntax Template
```verilog
assign wire_identifier = expression;
```
#### Component Breakdown
* **`assign`**: Keyword instructing the compiler to establish a permanent driving connection onto a net.
* **`wire_identifier`**: The net target being driven. It cannot be a `reg` data type.
* **`expression`**: Any synthesizable boolean, logical, or mathematical evaluation.

### B. Conditional Operator (Ternary Mux)
#### Formal Syntax Template
```verilog
assign target = (condition_expression) ? true_expression : false_expression;
```
#### Component Breakdown
* **`?`**: Evaluates the condition on the left.
* **`:`**: Delimits the alternate return paths. Synthesizes directly into a physical multiplexer circuit layout.

### C. Vector Concatenation Operator
#### Formal Syntax Template
```verilog
assign target = {signal_a, signal_b, signal_c};
```
#### Component Breakdown
* **`{ , }`**: Braces list multiple distinct arrays or bits to merge them together into a single wider parallel bus output.

### D. Vector Replication Operator
#### Formal Syntax Template
```verilog
assign target = {REPLICATION_MULTIPLIER{signal_name}};
```
#### Component Breakdown
* **`{M{N}}`**: Outer braces capture the action. `M` specifies the multiplication constant factor, and the nested element `N` is duplicated consecutively `M` times.

#### Isolated Code Example (Assignments)
```verilog
assign net_scalar = en & (net_vector == 8'hA5);
assign net_vector = (en) ? 8'hFF : 8'h00;

wire [9:0] combined_bus;
assign combined_bus = {net_scalar, en, net_vector}; 

wire [7:0] sign_extended_byte;
assign sign_extended_byte = {{4{net_vector[7]}}, net_vector[3:0]};
```

## 4. Procedural Logic Blocks

### A. Combinational Procedural Blocks
#### Formal Syntax Template
```verilog
always @(*) begin
    // Blocking Assignments
    variable = expression;
end
```
#### Component Breakdown
* **`always @(*)`**: Triggers on any event change among the expression's read inputs.
* **`=`**: The **Blocking Assignment** operator. Expressions execute sequentially, blocking down-stream code execution until the current slot evaluates.

### B. Sequential Procedural Blocks
#### Formal Syntax Template
```verilog
always @(posedge clk or negedge rst_n) begin
    // Non-Blocking Assignments
    variable <= expression;
end
```
#### Component Breakdown
* **`posedge / negedge`**: Filters evaluation triggers to occur *only* on the active rising or falling voltage transition edge of the target signal.
* **`<=`**: The **Non-Blocking Assignment** operator. Values are queued concurrently and pass to the target variables at the completion of the clock cycle simulation time step, preventing race conditions.

#### Isolated Code Example (Procedural Blocks)
```verilog
always @(*) begin
    reg_scalar  = 1'b0; // Default fallback to prevent latching
    signed_reg  = 16'sh0000;
    if (en) begin
        reg_scalar = 1'b1;
        signed_reg = $signed(net_vector); 
    end
end

always @(posedge clk or negedge rst_n) begin
    if (!rst_n) begin
        data_out <= 8'h00; 
        valid    <= 1'b0;
    end else if (en) begin
        data_out <= net_vector;
        valid    <= reg_scalar;
    end
end
```

## 5. Conditional Decision Blocks

### A. Case Statement Matrix
#### Formal Syntax Template
```verilog
case (evaluation_expression)
    MATCH_VECTOR_1: begin procedural_statements; end
    MATCH_VECTOR_2: begin procedural_statements; end
    default:        begin procedural_statements; end
endcase
```
#### Component Breakdown
* **`case` / `endcase`**: Enclosing markers for structural branching evaluation.
* **`default`**: A mandatory baseline fallback state that captures all unlisted combinations (including `X` and `Z` states) to prevent unwanted hardware memory latches during synthesis.

#### Isolated Code Example (Case Statements)
```verilog
always @(*) begin
    case (net_vector[1:0])
        2'b00:   reg_vector = 32'd100;     
        2'b01:   reg_vector = 32'hAFFFFFFF;
        2'b10:   reg_vector = 32'o755;     
        2'b11:   reg_vector = 32'b1010;    
        default: reg_vector = 32'h00000000;
    endcase
end
```

## 6. Structural Compile-Time Hardware Loops

### A. Generate For-Loops
#### Formal Syntax Template
```verilog
genvar loop_variable;
generate
    for (loop_variable = START; loop_variable < END; loop_variable = loop_variable + STEP) begin : block_name
        // Structural concurrent statements (e.g., assign, module instantiations)
    end
endgenerate
```
#### Component Breakdown
* **`genvar`**: A specialized variable type allocated strictly to track compile-time iteration steps.
* **`generate / endgenerate`**: Directives informing the compiler to expand the inner loop structure during build synthesis into parallel, unrolled physical logic gates.
* **`: block_name`**: A mandatory unique labeling token appended to the loop body block to create safe scoped paths for structural signals inside the expansion.

#### Isolated Code Example (Generate Loops)
```verilog
wire [7:0] internal_inverted_bus;
genvar k; 

generate
for (k = 0; k < 8; k = k + 1) begin : bitwise_inverter_block
assign internal_inverted_bus[k] = ~net_vector[k];
end
endgenerate
```
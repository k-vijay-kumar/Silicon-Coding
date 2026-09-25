# Verilog Simulation Scheduling Regions

## 1. The Stratified Event Queue Structure

### A. The Four Core Ordered Regions
#### Formal Flow Layout
```text
             [ SIMULATION TIME STEP TRIGGER ]
                            │
                            ▼
               ┌──────────────────────────┐
               │     1. ACTIVE REGION     │ ◄── Blocking Assignments (=)
               └────────────┬─────────────┘     Continuous Assignments (assign)
                            │
                            ▼
               ┌──────────────────────────┐
               │    2. INACTIVE REGION    │ ◄── #0 Delay Assignments
               └────────────┬─────────────┘
                            │
                            ▼
               ┌──────────────────────────┐
               │      3. NBA REGION       │ ◄── Non-Blocking Updates (<=)
               └────────────┬─────────────┘
                            │
                            ▼
               ┌──────────────────────────┐
               │    4. POSTPONED REGION   │ ◄── $strobe / $monitor (Read-Only)
               └──────────────────────────┘
```
#### Component Breakdown
* **Stratified Event Queue**: The internal mechanism of a Verilog simulator that categorizes execution threads into specific priority regions within the exact same time step to prevent execution race conditions.
* **Deterministic Execution**: Order enforced across different regions (e.g., Region 1 always finishes before Region 3 starts).
* **Non-Deterministic Execution**: Order of independent operations evaluated within the *same* region (e.g., two parallel active assignments may execute in any random order chosen by the simulator engine).

## 2. Region Breakdown & Event Types

### A. Active Region Events
#### Formal Syntax Template
```verilog
variable = expression;              // Procedural Blocking
assign wire_variable = expression;  // Continuous Assignment
$display("Immediate Output");       // Active Print Tasks
```
#### Component Breakdown
* **`=`**: The Blocking assignment operator. The right-hand side (RHS) is evaluated, and the left-hand side (LHS) is updated immediately before moving to the next line of code.
* **`assign`**: Evaluated continuously inside this region whenever its dependent right-hand side signals toggle.

### B. Inactive Region Events
#### Formal Syntax Template
```verilog
#0 variable = expression;
```
#### Component Breakdown
* **`#0`**: A specific delay modifier that forces the simulator to pull this process out of the current Active region queue and postpone it to the Inactive region queue. It executes only when the Active queue is completely empty.

### C. Non-Blocking Assignment (NBA) Region Events
#### Formal Syntax Template
```verilog
variable <= expression;
```
#### Component Breakdown
* **`<=` (RHS Phase)**: The Right-Hand Side expression is evaluated immediately in the **Active Region**.
* **`<=` (LHS Phase)**: The Left-Hand Side target variable update is suspended and placed into the **NBA Region** queue. It physically updates only after the Active and Inactive regions have cleared out.
* *Loopback Behavior:* If the update in the NBA region causes an event change that affects a combinational block, the simulator routes execution back to the **Active Region** within the same time step until all signals stabilize.

### D. Postponed Region Events
#### Formal Syntax Template
```verilog
$strobe("Stable State: %h", variable);
$monitor("Persistent Monitor: %b", variable);
```
#### Component Breakdown
* **`$strobe` / `$monitor`**: System tasks executed in the absolute final zone of the current time step. 
* **Read-Only Snapshot**: No variable value modifications are permitted in this region. This acts as a safe, settled capture window to log data without inducing simulation races.

## 3. Hardware Boundaries & Synthesis Mismatch

### A. Scope of Scheduling Regions
#### Formal Behavior Rule
* **Simulation-Only Construct**: Scheduling regions exist strictly within the host CPU software simulator software layer. They have zero physical footprint or structural presence inside the physical FPGA silicon fabric.

### B. Hardware Physical Mapping Translation
#### Mapping Table Overview

| Simulator Software Region | Physical FPGA Hardware Mechanism |
| :--- | :--- |
| **Active Region** | **Combinational Propagation:** Continuous electrical flow through logic gates (AND, OR, LUTs) and copper wire traces. |
| **NBA Region** | **Clock-to-Q Delay:** The sub-nanosecond physical gate propagation delay required for a D Flip-Flop to toggle its output pin state following a clock edge. |
| **Postponed Region** | **Setup/Hold Window:** The stable voltage window directly preceding the subsequent clock edge where signal lines have completely stabilized. |

### C. The Simulation-Synthesis Mismatch Hazard
#### Architectural Impact Rule
* Violating assignment blueprints (e.g., executing a blocking `=` inside a clocked sequential block) forces the simulator to drop structural updates directly inside the **Active Region**, skipping the structural **NBA** loop step entirely. 
* While the software simulator will pass code checks on a PC, physical FPGA silicon ignores software queues and acts purely via physical register delays. This yields broken, unaligned data on the physical hardware—a critical bug profile known as a **Simulation-Synthesis Mismatch**.

## Isolated Code Example (Scheduling & Race Verification)

```verilog
`timescale 1ns / 1ps

module tb_scheduling_demo;
    reg clk;
    reg a, b;

    // --- Active Region Initialization ---
    initial begin
        clk = 1'b0;      // Executed instantly in the Active Region
        a = 1'b1;        // Executed instantly in the Active Region
    end

    // --- NBA Region Interaction ---
    always @(posedge clk) begin
        b <= a;          // 1. RHS (a) is read instantly in the ACTIVE region.
                         // 2. LHS (b) update is scheduled and executed in the NBA REGION.
    end

    // --- Evaluation Analysis ---
    always @(posedge clk) begin
        // DANGEROUS RACE: Reads variable 'b' before the NBA update resolves
        $display("Time %t | $display (Active Region) -> b = %b", $time, b); 
        
        // SAFE: Execution is delayed until the Postponed Region after NBA updates settle
        $strobe("Time %t | $strobe  (Postponed Region) -> b = %b", $time, b);  
    end

    // Basic driver to trigger clock edge at 10ns
    initial begin
        #10;
        clk = 1'b1;
        #5;
        $finish;
    end
endmodule
```

### Expected Console Output Breakdown
```text
Time 10000 | \$display (Active Region) -> b = x
Time 10000 | \$strobe  (Postponed Region) -> b = 1
```

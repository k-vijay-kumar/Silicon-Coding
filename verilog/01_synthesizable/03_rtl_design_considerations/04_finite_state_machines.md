# Finite-State Machines

An FSM stores a state and computes its next state from the current state and inputs. A common Verilog pattern separates the combinational next-state logic from the clocked state register.

```verilog
module controller (
    input  wire clk,
    input  wire rst_n,
    input  wire start,
    input  wire done,
    output reg  busy
);
    localparam [1:0] IDLE = 2'b00,
                     ACTIVE = 2'b01;

    reg [1:0] state, next_state;

    always @(*) begin
        next_state = state;
        busy = 1'b0;
        case (state)
            IDLE:   if (start) next_state = ACTIVE;
            ACTIVE: begin
                busy = 1'b1;
                if (done) next_state = IDLE;
            end
            default: next_state = IDLE;
        endcase
    end

    always @(posedge clk or negedge rst_n) begin
        if (!rst_n)
            state <= IDLE;
        else
            state <= next_state;
    end
endmodule
```

`busy` is a Moore-style output because it depends only on the current state. Provide defaults in combinational logic and a recovery branch for unused encodings. Synthesis tools may recode the states; inspect reports when encoding matters.
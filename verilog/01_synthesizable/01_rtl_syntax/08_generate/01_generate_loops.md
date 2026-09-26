# Generate Loops

A generate loop expands repeated structure during elaboration; it does not run as a hardware-time loop.

```verilog
genvar bit_index;
generate
    for (bit_index = 0; bit_index < 8; bit_index = bit_index + 1) begin : invert_bit
        assign inverted[bit_index] = ~data[bit_index];
    end
endgenerate
```

The loop bounds are elaboration-time constants. Named blocks create predictable hierarchy.
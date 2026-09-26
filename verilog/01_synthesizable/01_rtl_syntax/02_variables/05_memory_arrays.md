# Memory Arrays

An unpacked array of packed words models a collection of values and may infer memory, registers, or other logic depending on its use and target.

```verilog
reg [7:0] samples [0:15];
```

This declares 16 words, each 8 bits wide. Inference depends on read/write style and FPGA or ASIC synthesis support.
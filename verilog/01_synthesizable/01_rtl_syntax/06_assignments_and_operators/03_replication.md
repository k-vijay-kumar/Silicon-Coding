# Replication

Replication repeats a bit pattern a fixed number of times.

```verilog
wire [7:0] sign_mask;
assign sign_mask = {8{sign_bit}};
```

The replication count must be known at elaboration time. Replication is often used with concatenation for extension or masks.
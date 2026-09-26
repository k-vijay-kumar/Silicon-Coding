# Continuous Assignments

`assign` continuously drives a net from an expression.

```verilog
wire active;
assign active = enable & ready;
```

Use continuous assignments for combinational relationships between nets. Procedural assignments belong inside an `always` block.
# Named Port Connections

Named connections bind a child module's ports to signals in the parent by port name.

```verilog
adder u_adder (
    .left  (operand_a),
    .right (operand_b),
    .sum   (result)
);
```

They remain clear if the child port declaration order changes. Verify each connected name and width against the child module.
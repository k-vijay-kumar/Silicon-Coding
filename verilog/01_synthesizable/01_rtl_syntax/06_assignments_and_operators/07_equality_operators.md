# Equality Operators

`==` and `!=` perform logical equality comparisons and can produce `x` if unknown bits prevent a definite result. `===` and `!==` compare all four-state values, including `x` and `z`, and always produce `0` or `1`.

```verilog
if (actual !== expected)
    $display("Mismatch: actual=%b expected=%b", actual, expected);
```

Case equality is useful in testbench checks when unknown values should count as a mismatch. Synthesizable support and hardware meaning vary by construct and tool; do not use it as a way to build physical X-detection logic.
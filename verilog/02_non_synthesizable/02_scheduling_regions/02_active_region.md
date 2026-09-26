# Active Region

Active-region work includes procedural statements triggered at the current time, such as blocking assignments and `$display` calls.

```verilog
value = next_value;
$display("value=%b", value);
```

Independent processes in the same region may run in either order. Do not rely on an ordering that the language does not guarantee.
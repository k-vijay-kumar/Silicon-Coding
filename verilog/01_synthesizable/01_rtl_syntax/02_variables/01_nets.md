# Nets

A `wire` is a net that carries a value from its drivers. It does not retain a value by itself.

```verilog
wire ready;
assign ready = valid & enabled;
```

An undriven four-state `wire` resolves to `z` in simulation. Physical behavior of an undriven FPGA pin or internal connection depends on the device and implementation; do not rely on it.
# Tri-State I/O

A tri-state output drives a value when enabled and releases the pin otherwise.

```verilog
assign io_pin = drive_enable ? data_out : 1'bz;
```

FPGA internal logic generally represents selection with muxes; tri-state buffers are typically supported only at device I/O pins. Check the target's I/O resources and synthesis reports.
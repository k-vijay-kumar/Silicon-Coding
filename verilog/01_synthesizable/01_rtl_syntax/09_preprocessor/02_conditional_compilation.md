# Conditional Compilation

Preprocessor directives include or exclude source text before compilation.

```verilog
`ifdef TARGET_BOARD
    // Board-specific implementation
`else
    // Alternative implementation
`endif
```

Unlike a procedural `if`, this does not describe a runtime mux. Keep macro definitions in the build configuration or a shared header.
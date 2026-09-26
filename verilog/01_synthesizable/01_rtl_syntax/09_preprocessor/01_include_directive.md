# Include Directive

The preprocessor inserts the named file at the include location before compilation.

```verilog
`include "design_config.vh"
```

Header files commonly hold shared macros and declarations. Keep module implementations in source files unless the project has a specific reason otherwise.
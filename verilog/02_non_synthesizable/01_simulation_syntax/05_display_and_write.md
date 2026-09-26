# Display and Write

`$display` and `$write` print formatted output when the task executes.

```verilog
$display("data=%h", data); // Adds a newline
$write("waiting...");     // Does not add a newline
```

Use format specifiers such as `%b`, `%d`, `%h`, and `%t` to control value formatting.
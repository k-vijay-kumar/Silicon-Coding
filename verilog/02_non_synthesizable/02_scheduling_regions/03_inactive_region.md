# Inactive Region

A procedural `#0` delay schedules the process to resume in the Inactive region of the current time slot.

```verilog
#0 value = next_value;
```

It runs after the current Active events drain and before NBA updates. `#0` is not a general race fix; prefer clear synchronization and assignment practices.
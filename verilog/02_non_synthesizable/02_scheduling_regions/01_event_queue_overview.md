# Event Queue Overview

Verilog simulators divide work at a simulation time into ordered event regions. The commonly taught sequence includes Active, Inactive, NBA, and Postponed regions; the full SystemVerilog scheduler has additional regions.

```text
Active -> Inactive -> NBA -> (reevaluate events as needed) -> Postponed
```

The regions are simulation scheduling rules, not separate physical hardware blocks. Ordering within one region can still expose races.
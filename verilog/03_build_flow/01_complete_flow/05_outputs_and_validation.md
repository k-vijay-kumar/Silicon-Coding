# Outputs and Validation

The three flows produce different artifacts and answer different questions.

| Flow | Typical outputs | What they help verify |
| --- | --- | --- |
| FPGA implementation | Bitstream and implementation reports | Whether the design maps to the selected FPGA and meets implementation constraints |
| ASIC implementation | Physical layout database and sign-off reports | Whether the design meets technology-specific physical, timing, and power requirements |
| RTL simulation | Pass/fail results, logs, waveforms, and coverage | Whether tested behavioral scenarios produce expected results |

Passing simulation does not guarantee that hardware meets timing or physical constraints. Successful synthesis does not prove functional correctness. Use verification and implementation checks for their separate purposes.
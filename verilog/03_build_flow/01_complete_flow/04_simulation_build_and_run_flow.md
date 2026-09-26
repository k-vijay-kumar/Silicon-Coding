# Simulation Build and Run Flow

Simulation combines the design under test with verification code. The design may be synthesizable RTL; the testbench supplies stimulus and checks and is not part of the hardware implementation.

```text
Synthesizable RTL + testbench + models + file list
    -> preprocess and compile
    -> elaborate simulation top
    -> run event-driven simulation
    -> check results and inspect logs, waves, and coverage
```

1. **Choose sources:** Include the RTL design, testbench, required packages or models, and memory or vector files. Exclude duplicate module definitions and unrelated hardware top levels.
2. **Configure compilation:** Supply source lists, include directories, macro definitions, language version, and simulator libraries.
3. **Preprocess and compile:** Expand macros and includes, parse the sources, and compile the design and testbench into simulator-specific objects or an executable model.
4. **Elaborate:** Select the testbench top, resolve instances and parameters, expand generate constructs, and bind ports and models.
5. **Run:** The simulator executes testbench code and evaluates RTL using Verilog event scheduling. Simulation delays advance simulation time; they do not implement physical timing.
6. **Check and review:** Use assertions, scoreboards, and explicit checks. Inspect pass/fail summaries, logs, waveforms, and coverage; rerun tests after fixes.

A gate-level simulation is an optional later step. It uses a synthesized netlist and may use SDF timing annotation with a testbench. It remains a simulation and does not replace physical timing sign-off.

## Example Command with Icarus Verilog

Given a design file `rtl/mux2.v` and a testbench file `tb/tb_mux2.v` whose top module is `tb_mux2`:

```sh
mkdir -p build
iverilog -g2005 -s tb_mux2 -o build/tb_mux2.vvp rtl/mux2.v tb/tb_mux2.v
vvp build/tb_mux2.vvp
```

The `-g2005` flag selects Verilog-2005 syntax. Use the language generation and file list that match your project and simulator.
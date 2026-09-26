# Silicon-Coding

This repository is a beginner-friendly collection of Verilog and digital hardware design notes.<br>
Each topic has a short, focused page, linked from this README.

## Folder Structure

```text
Silicon-Coding/
├── LICENSE
├── README.md
└── verilog/
	├── 01_synthesizable/
	│   ├── 01_rtl_syntax/
	│   ├── 02_coding_styles/
	│   └── 03_rtl_design_considerations/
	├── 02_non_synthesizable/
	│   ├── 01_simulation_syntax/
	│   └── 02_scheduling_regions/
	└── 03_build_flow/
		├── 01_complete_flow/
		└── 02_fpga_asic_mapping/
```

## Purpose

This repository helps build a strong foundation in Verilog design and verification,<br>
especially for students and beginners learning synthesizable RTL and simulation behavior.

## Verilog Learning Path

### Coding Styles

- [Overview](verilog/01_synthesizable/02_coding_styles/01_overview.md)
- [Structural](verilog/01_synthesizable/02_coding_styles/02_structural.md)
- [Dataflow](verilog/01_synthesizable/02_coding_styles/03_dataflow.md)
- [Behavioral](verilog/01_synthesizable/02_coding_styles/04_behavioral.md)

### RTL Syntax

- [Module structure](verilog/01_synthesizable/01_rtl_syntax/01_modules/01_module_structure.md)
- [Ports](verilog/01_synthesizable/01_rtl_syntax/01_modules/02_ports.md)
- [Named port connections](verilog/01_synthesizable/01_rtl_syntax/01_modules/03_named_port_connections.md)
- [Nets](verilog/01_synthesizable/01_rtl_syntax/02_variables/01_nets.md)
- [Variables](verilog/01_synthesizable/01_rtl_syntax/02_variables/02_variables.md)
- [Vectors](verilog/01_synthesizable/01_rtl_syntax/02_variables/03_vectors.md)
- [Signed values](verilog/01_synthesizable/01_rtl_syntax/02_variables/04_signed_values.md)
- [Memory arrays](verilog/01_synthesizable/01_rtl_syntax/02_variables/05_memory_arrays.md)
- [Four-state values](verilog/01_synthesizable/01_rtl_syntax/02_variables/06_four_state_values.md)
- [Parameters](verilog/01_synthesizable/01_rtl_syntax/03_constants/01_parameters.md)
- [Synthesizable functions](verilog/01_synthesizable/01_rtl_syntax/04_functions/01_synthesizable_functions.md)
- [Conditional operator](verilog/01_synthesizable/01_rtl_syntax/05_conditionals/01_conditional_operator.md)
- [Case statements](verilog/01_synthesizable/01_rtl_syntax/05_conditionals/02_case_statements.md)
- [If and else](verilog/01_synthesizable/01_rtl_syntax/05_conditionals/03_if_else.md)
- [Continuous assignments](verilog/01_synthesizable/01_rtl_syntax/06_assignments_and_operators/01_continuous_assignments.md)
- [Concatenation](verilog/01_synthesizable/01_rtl_syntax/06_assignments_and_operators/02_concatenation.md)
- [Replication](verilog/01_synthesizable/01_rtl_syntax/06_assignments_and_operators/03_replication.md)
- [Signed casts](verilog/01_synthesizable/01_rtl_syntax/06_assignments_and_operators/04_signed_casts.md)
- [Fixed part-selects](verilog/01_synthesizable/01_rtl_syntax/06_assignments_and_operators/05_fixed_part_selects.md)
- [Indexed part-selects](verilog/01_synthesizable/01_rtl_syntax/06_assignments_and_operators/06_indexed_part_selects.md)
- [Equality operators](verilog/01_synthesizable/01_rtl_syntax/06_assignments_and_operators/07_equality_operators.md)
- [Combinational blocks](verilog/01_synthesizable/01_rtl_syntax/07_procedural_blocks/01_combinational_blocks.md)
- [Sequential blocks](verilog/01_synthesizable/01_rtl_syntax/07_procedural_blocks/02_sequential_blocks.md)
- [Generate loops](verilog/01_synthesizable/01_rtl_syntax/08_generate/01_generate_loops.md)
- [Include directive](verilog/01_synthesizable/01_rtl_syntax/09_preprocessor/01_include_directive.md)
- [Conditional compilation](verilog/01_synthesizable/01_rtl_syntax/09_preprocessor/02_conditional_compilation.md)

### RTL Design Considerations

- [Tri-state I/O](verilog/01_synthesizable/03_rtl_design_considerations/01_tristate_io.md)
- [Case attributes](verilog/01_synthesizable/03_rtl_design_considerations/02_case_attributes.md)
- [Arithmetic sizing](verilog/01_synthesizable/03_rtl_design_considerations/03_arithmetic_sizing.md)
- [Finite-state machines](verilog/01_synthesizable/03_rtl_design_considerations/04_finite_state_machines.md)
- [Clock enables and resets](verilog/01_synthesizable/03_rtl_design_considerations/05_clock_enables_and_resets.md)

### Build Flow

- [Complete flow overview](verilog/03_build_flow/01_complete_flow/01_overview.md)
- [FPGA hardware flow](verilog/03_build_flow/01_complete_flow/02_fpga_hardware_flow.md)
- [ASIC hardware flow](verilog/03_build_flow/01_complete_flow/03_asic_hardware_flow.md)
- [Simulation build and run flow](verilog/03_build_flow/01_complete_flow/04_simulation_build_and_run_flow.md)
- [Outputs and validation](verilog/03_build_flow/01_complete_flow/05_outputs_and_validation.md)
- [RTL-to-hardware mapping: combinational logic](verilog/03_build_flow/02_fpga_asic_mapping/01_combinational_logic.md)
- [RTL-to-hardware mapping: routing](verilog/03_build_flow/02_fpga_asic_mapping/02_routing.md)
- [RTL-to-hardware mapping: sequential storage](verilog/03_build_flow/02_fpga_asic_mapping/03_sequential_storage.md)
- [RTL-to-hardware mapping: multiplexers](verilog/03_build_flow/02_fpga_asic_mapping/04_multiplexers.md)
- [RTL-to-hardware mapping: resets](verilog/03_build_flow/02_fpga_asic_mapping/05_resets.md)
- [RTL-to-hardware mapping: FPGA and ASIC trade-offs](verilog/03_build_flow/02_fpga_asic_mapping/06_fpga_asic_tradeoffs.md)

### Simulation Syntax

- [Timescale](verilog/02_non_synthesizable/01_simulation_syntax/01_timescale.md)
- [Initial blocks](verilog/02_non_synthesizable/01_simulation_syntax/02_initial_blocks.md)
- [Clock generation](verilog/02_non_synthesizable/01_simulation_syntax/03_clock_generation.md)
- [Delays](verilog/02_non_synthesizable/01_simulation_syntax/04_delays.md)
- [Display and write](verilog/02_non_synthesizable/01_simulation_syntax/05_display_and_write.md)
- [Monitor and strobe](verilog/02_non_synthesizable/01_simulation_syntax/06_monitor_and_strobe.md)
- [Finish](verilog/02_non_synthesizable/01_simulation_syntax/07_finish.md)
- [Self-checking testbench](verilog/02_non_synthesizable/01_simulation_syntax/08_testbench_example.md)

### Scheduling Regions

- [Event queue overview](verilog/02_non_synthesizable/02_scheduling_regions/01_event_queue_overview.md)
- [Active region](verilog/02_non_synthesizable/02_scheduling_regions/02_active_region.md)
- [Inactive region](verilog/02_non_synthesizable/02_scheduling_regions/03_inactive_region.md)
- [NBA region](verilog/02_non_synthesizable/02_scheduling_regions/04_nba_region.md)
- [Postponed region](verilog/02_non_synthesizable/02_scheduling_regions/05_postponed_region.md)
- [Race example](verilog/02_non_synthesizable/02_scheduling_regions/06_race_example.md)
- [Simulation and hardware](verilog/02_non_synthesizable/02_scheduling_regions/07_simulation_and_hardware.md)

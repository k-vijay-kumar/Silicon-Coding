# Simulation and Hardware

Scheduling regions describe simulator ordering. They do not map one-to-one to FPGA or ASIC structures.

RTL still describes hardware behavior: a clocked process can infer state, while simulation scheduling determines when the simulator evaluates and updates that state. Blocking assignments in clocked logic may create simulation-order races across processes; use nonblocking assignments for conventional sequential RTL and follow the project's coding rules.
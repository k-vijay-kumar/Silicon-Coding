# ASIC Hardware Flow

```text
Synthesizable RTL + libraries + constraints
    -> elaborate and synthesize
    -> map to standard cells
    -> DFT and floorplan
    -> place and build clock tree
    -> route and extract parasitics
    -> timing, power, and physical sign-off
    -> stream out layout for fabrication
```

1. **Select the target:** Provide standard-cell libraries, process technology data, and timing, power, and area constraints.
2. **Elaborate and synthesize:** Resolve RTL hierarchy and parameters, optimize the design, and map it to target library cells.
3. **Prepare implementation:** Insert test structures such as scan chains when required, define the floorplan, and plan power delivery.
4. **Place cells:** Assign standard cells to physical locations and optimize paths and congestion.
5. **Build the clock tree:** Distribute clocks while managing skew and transition limits.
6. **Route and extract:** Connect cells with metal and estimate or extract interconnect parasitics.
7. **Sign off:** Check timing, power, signal integrity, and physical design rules; iterate when checks fail.
8. **Deliver layout:** Stream out the physical database, commonly GDSII or OASIS, for manufacturing handoff.

Formal equivalence, DFT, power integrity, and other sign-off checks vary by technology and organization, and may be repeated at several stages.
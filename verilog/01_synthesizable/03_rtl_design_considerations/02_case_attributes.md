# Case Attributes

Some synthesis tools support attributes such as `parallel_case` and `full_case` to state assumptions about case branches.

```verilog
(* parallel_case *) case (state)
    // branches
endcase
```

These are tool-specific hints, not substitutes for correct RTL. `full_case` can make simulation and synthesized behavior disagree when states are omitted. Prefer complete branches and an explicit `default`; check your tool documentation before using attributes.
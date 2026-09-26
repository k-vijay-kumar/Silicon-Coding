# Postponed Region

`$strobe` and `$monitor` report values at the end of the current time step, after updates for that step have settled.

```verilog
$strobe("q=%b", q);
```

This is useful for observing the post-NBA value. The postponed region is read-only; it is not a hardware timing window.
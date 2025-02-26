# `Scoreboard`

The `Scoreboard` "module" is implemented in the top-level `RocketCore` module.
"module" is in quotes because the scoreboard is ***not*** a separate module, it is inlined into the host module directly.
It is intended to allow multiple concurrent instructions to access the register file and detect **possible** collisions (hazards).
Below is a small example excerpt of the definition and a use of the `Scoreboard` module.

```scala
class Scoreboard(n: Int, zero: Boolean = false) {
  private val _r = RegInit(0.U(n.W))
}
val sboard = new Scoreboard(32)
```

A `Scoreboard` is a bit-set register that identifies which registers will be ***written*** by instructions in the pipeline.
The scoreboard entry is set when the instruction's destination register is determined and is cleared when the instruction completes its writeback to the register file.

<div class="note">
The reason the two uses of the <code>Scoreboard</code> in the <code>RocketCore</code> module use <code>32</code> is because there are 32 registers in RISC-V (both integer and floating-point).

The optional parameter <code>zero</code> forcibly clears out the zero-th bit of the bit-set.
This is done for the integer register file, because the register <code>x0</code> (the zeroth-indexed register) is always 0, so it can <strong>never</strong> conflict as a write destination.
</div>

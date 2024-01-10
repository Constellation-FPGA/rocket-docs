# `IBuf` (Instruction Buffer)

<div class="warning">
Contains <code>PC</code> and exports <code>PC</code>!
</div>

Has a unique definition of `Instruction` that uses `ExpandedInstruction` from RVC along with some extra front-end exception information.
NOTE: The `ExpandedInstruction` is usually inlined into the `Instruction` bundle.

## `ic` Instruction Cache?
Signals prefixed with `ic` (suchs as `icData` and `icMask`) are values that come from and are determined by the instruction cache?

The current instruction is found by performing bit-wise operations on `icData`, `icMask`, and `buf.data`.

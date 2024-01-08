# `IBuf` (Instruction Buffer)

<div class="warning">
Contains <code>PC</code> and exports <code>PC</code>!
</div>

Has a unique definition of `Instruction` that uses `ExpandedInstruction` from RVC along with some extra front-end exception information.
NOTE: The `ExpandedInstruction` is usually inlined into the `Instruction` bundle.

# Instruction Decoding & Control Signals
Rocket does not have a dedicated or separate control unit to handle the pipeline.
Instead, the top-level pipeline passes control signals along/down its pipeline to keep instructions executing properly.

## `IntCtrlSigs`

## `DecodeConstants`
Must have the following fields defined:
  * Valid?
  * Floating Point Valid?
  * RoCC Instruction?
  * Branch Instruction?
  * `jal` Instruction?
  * `jalr` Instruction?
  * Read Enable Source Register 2 (`renx2`)?
  * Read Enable Source Register 1 (`renx1`)?
  * salu2
  * salu1
  * Immediate?
  * DW??
  * ALU function to perform
  * Memory Valid?
  * Memory Command?
    What kind of memory operate is this?
    Read (`M_XRD`) or Write (`M_XWR`)?
  * Read Enable Floating Point Source Register 1 (`renf1`)?
  * Read Enable Floating Point Source Register 2 (`renf2`)?
  * Read Enable Floating Point Source Register 3 (`renf3`)?
  * wfd?
  * mul?
  * div?
  * wxd??
  * CSR?
  * fence.i?
  * fence?
  * amo?
  * dp?

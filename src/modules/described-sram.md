# `DescribedSRAM`
The `DescribedSRAM` utility module *is* an SRAM module (it uses the `SyncReadMem` chisel3 module), but has additional information for Diplomacy and writing its contents out to a file after elaboration.

It takes in a `name`, a `desc`ription, the `size` of the SRAM for the depth, and Chisel type `T` which is a subtype of `Data` (namely `T <: Data`).
The `name` and `desc` fields are used to write out SRAM information out to a file.

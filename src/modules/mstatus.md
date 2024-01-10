# MStatus (Machine Status)

The `MStatus` class implements the MStatus register from the RISC-V privileged specification.
This implementation also adds extensions for performance counters and debugging support.

```chisel
mpp in MStatus
status = MStatus in CSRFileIO
val io = CSRFileIO in CSRFile
val csr = CSRFile in RocketCore
```

## Default Values
Because Rocket-chip is written in Chisel, all hardware **must** have known logical values at all time (unknown `X`, high-impedance `Z`, high-value `H`, low-value `L`, etc.) are not allowed.
This means that fields marked as `UInt` will default to `0.U`, and fields marked as `Bool` will default to `false.B`.

This means that `MPP` will be set to `0b00` initially, making your currently-executing machine mode look like it just came from user-mode.
This is probably not the case if your simulation has *just* started.

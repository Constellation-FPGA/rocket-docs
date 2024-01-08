# MStatus (Machine Status)

The `MStatus` class implements the MStatus register from the RISC-V privileged specification.
This implementation also adds extensions for performance counters and debugging support.

```chisel
mpp in MStatus
status = MStatus in CSRFileIO
val io = CSRFileIO in CSRFile
val csr = CSRFile in RocketCore
```

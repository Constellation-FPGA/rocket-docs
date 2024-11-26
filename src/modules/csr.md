# `CSR`s (Control & Status Registers)

## `MStatus` (Machine Status)
The `MStatus` class implements the MStatus register from the RISC-V privileged specification.
This implementation also adds extensions for performance counters and debugging support.

```chisel
mpp in MStatus
status = MStatus in CSRFileIO
val io = CSRFileIO in CSRFile
val csr = CSRFile in RocketCore
```

### Default Values
Because Rocket-chip is written in Chisel, all hardware **must** have known logical values at all times (unknown `X`, high-impedance `Z`, high-value `H`, low-value `L`, etc.) are not allowed.
This means that fields marked as `UInt` will default to `0.U`, and fields marked as `Bool` will default to `false.B`.

This means that `MPP` will be set to `0b00` initially, making your currently-executing machine mode look like it just came *from* user-mode.
This is probably not the case if your simulation has *just* started.

## `CSRFileIO`
This is the IO bundle that the `CSRFile` uses.

Notable fields include:
  * `eret`: An `Output` boolean, which is made `true.B` when an `mret` or `sret` instruction is executed.
  * `evec`: An `Output` `vaddrBitsExtended`-width virtual address.
    This is the address that `PC` should be set to when an `mret` or `sret` happens.
  * `exception`: An `Input` boolean, stating that an exception has happened.
  * `cause`: An `Input` `xLen` word, which is given to either `mcause` or `scause`.
  * `interrupt`: An `Input` boolean, stating that an interrupt has happened.
  * `interrupt_cause`: An `Input` `xLen` word, stating which interrupt happened and is given to either `mcause` or `scause`.
  * `pc`: The value of `PC` at the time of changing the CSRs.
    This input is unused when manually reading/writing CSRs.
  * `tval`: Any extra information that should be passed into either `mtval` or `stval` to provide additional information to the handler.
    For example, a failing `ld` instruction would have the address that failed to load in `tval`, and the virtual address of the `ld` instruction itself would be in `pc`.
  * `status`: The state of the [`MStatus`](#mstatus-machine-status) CSRs.
  * `hstatus`: The state of the `HStatus` CSRs.
  * `gstatus`: The state of the [`MStatus`](#mstatus-machine-status) CSRs.

## `CSRFile`
Rocket's `CSRFile` is where the main logic of handling CSRs and changing privileges is implemented.
This module is particularly large, so only select portions of it are highlighted here.

### `xCAUSE` Registers
The `mcause` and `scause` registers are defined in `CSRFile` and are added to the read-mapping in the file as well.
These registers are set to a value ***only when a trap occurs***.
They are ***never reset*** to a particular value.
It is safe to act on the cause in these registers only **immediately after** entering a trap handler.

### Supported & Delegable Traps
There is a set of supported traps (both interrupts and exceptions) in the module, and defines *which* traps are supported and which are delegable.
Rocket may not support certain traps, which is marked in the `supported_interrupts` and `supported_exceptions` values.
Some RISC-V specification revisions define that some traps cannot be delegated to lower privilege modes; which *are allowed* are defined as `delegable_interrupts` and `delegable_exceptions`.

### System Instructions
One of the more important parts of this module is that it decodes a passed instruction and decides if it is one of:
  * `call`: `ecall`
  * `break`: `ebreak`
  * `insn_ret`: `mret`/`sret`
  * `cease`/`halt`
  * `wfi`

This is decoded the same way that Rocket decodes instructions generally, using the `DecodeLogic` class.
The designer maps the instruction's Chisel symbol to a list of "signals", which map to one of the CSR-changing possibilities.
A snippet of Rocket's `CSR.scala` is included below to illustrate how this mapping is written.
```scala
val decode_table = Seq(ECALL->       List(Y,N,N,N,N,N,N,N,N),
                       EBREAK->      List(N,Y,N,N,N,N,N,N,N),
                       MRET->        List(N,N,Y,N,N,N,N,N,N))

val insn_call :: insn_break :: insn_ret :: insn_cease :: insn_wfi :: _ :: _ :: _ :: _ :: Nil = {
  val insn = ECALL.value.U | (io.rw.addr << 20)
  DecodeLogic(insn, decode_table(0)._2.map(x=>X), decode_table).map(system_insn && _.asBool)
}
```

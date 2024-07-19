# Trap-handling Subsystem

In RISC-V, there are two kinds of traps:
  1. [Exceptions](#exceptions)
  2. [Interrupts](#interrupts)

This document is intended to describe Rocket-Chip, not how traps work on RISC-V, so the following sections do not go into much detail.

## Exceptions
An exception is caused by something exceptional.
`ecall`s and illegal instructions are two examples of exceptions.
There are others, like a page fault (when virtual memory is available and enabled) or a memory-access fault (when PMP is set up).

There are precise and imprecise exceptions.
  * Precise exceptions interrupt the processor's instruction execution immediately and allow you to return to the ***exact*** point where the exception occurred.
    Illegal instructions, `ecall`s, and page faults (to name a few) are precise exceptions.
  * Imprecise exceptions may appear several clock cycles later and do not allow you to replay the instruction.
    Floating-point exceptions are a common example of imprecise exceptions, alerting the user that a floating-point calculation did something unexpected.

## Interrupts
An interrupt is typically caused by something external to the hart, such as a timer, a peripheral (like a network card), or another hart interrupting this one (an Inter-Processor Interrupt, IPI).
These are always imprecise in that they do not know the exact instruction they were caused by, but they allow a processor to restart an instruction that was interrupted.

## Handling Traps
Rocket-Chip handles precise exceptions in the [writeback](../rocket-core/writeback.md) stage!
After a precise exception is detected, the processor flushes out the entire pipeline before jumping to the handler installed in `mtvec` or `stvec`.

<div class="note">
Please see the <a href="https://github.com/riscv/riscv-isa-manual/releases">RISC-V privileged specification</a> to see a listing of all CSRs.
</div>

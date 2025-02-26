# Hazards, Exceptions, Stalling, and Killing
A processor will naturally experience occasions where the code that is written is not possible to execute.
One common occurrence is that two instructions depend on one another, for example, Read-After-Write (RAW) dependences are common, since we have a fixed number of registers to place all of our data in.
The processor could attempt to do something illegal or impossible, like executing an illegal instruction.

From a pipeline perspective, hazards and exceptions behave the same way.
Hazards and exceptions need to stall the pipeline to make sure an older instruction (one further in the pipeline) reaches a point where the processor can begin executing again.
However, exceptions take this one step further and require that the processor **kill** instructions so that their effects **do not** occur.

<div class="note">
Since Rocket is an non-superscalar in-order core, it <strong>does not</strong> have a separate rename or commit stage, nor does it have a reorder buffer.
So the core must make sure its pipeline remains in good order while it is handling hazards and exceptions.
</div>

## Hazards
A hazard occurs when two (or more) instructions in the pipeline depend on one another in a way that the hardware cannot gracefully resolve.
To handle this, an instruction stalls the pipeline until it is finished doing its critical task.

## Exceptions
An exception occurs when an exceptional event occurs (go figure).
A common example of this is a page fault, but testing with illegal instructions is convenient.

This section is concerned with how the **main processor pipeline in `RocketCore`** handles a trap.
Please see the [Trap-handling Subsystem](../subsystems/trap-handling.md) for more information about how traps are handled as a whole subsystem (across all the different submodules).

## Stalling
Rocket can choose what pipeline stage to start stalling at while it waits for long-latency operations to complete.
Some of these long-latency operations include:
  * Floating point computations (which may be dynamic-delay too)
  * Memory requests

## Killing
Further, Rocket needs the ability to **kill** instructions in its pipeline.
Killing an instruction is *different* than stalling, because killing an instruction marks that pipeline register's contents as dead and they should be discarded.
Stalling just stalls the pipeline for an unknown amount of time.

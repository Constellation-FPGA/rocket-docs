# `ShiftQueue`
The `ShiftQueue` utility module has the same interface as a regular `Queue` (which is from Chisel's standard library), but uses a shift register as its internal implementation.
This implementation is faster for dequeuing content than the regular `Queue`, but it is less energy-efficient when there are multiple items in the queue.

The `ShiftQueue` is mostly used by [Diplomacy](../diplomacy.md) and the [Frontend](../subsystem/frontend.md).
It is used for these because the shift queue usually has zero or one entries, making it more efficient than regular queues.

# `HellaCache`

`HellaCache` is Rocket's implementation of caches, mostly L1 caches.

## Exceptions
The module exports 4 kinds of exceptions in its `HellaCacheExceptions`.

  1. `ma`: Misaligned Address.
     The address you are loading from/storing to is misaligned with the width of the load/store the instruction specified.
  2. `pf`: Page Fault.
  3. `gf`: Guest Fault (only applicable when the core has the H-extension for hypervisor mode).
     The guest virtual machine experienced a page fault.
  4. `ae`: Access Exception.
     These are caused by physical memory accesses and running afoul of PMA/PMP.

Obviously, each of these can have one of two exception types based on the instruction that was run: loads and stores.
These are defined, not as an enumeration, but as the `AlignmentExceptions` bundle.
It has two Boolean wires:
  1. `ld`: Raised to `true.B` if a load operation caused a fault
  2. `st`: Raised to `true.B` if a store operation caused a fault

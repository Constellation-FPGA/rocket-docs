# Subsystems
Each of the following sections describes a subsystem of the core.
The descriptions are done in isolation from other subsystems of the core.
For discussion and description on how multiple subsystems interact, please see the a relevant section in the [top-level design](./rocket-core.md).

For example, the L1 cache subsystem does not discuss how the address to look up in the cache is generated.
It only discusses how a cache request is responded to, what happens when there is a cache hit/miss, what happens when the cache is evicted, and what happens when refilling the instruction cache.

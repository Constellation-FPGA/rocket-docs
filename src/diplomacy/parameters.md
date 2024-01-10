# Diplomacy Parameters (`Parameters`)

Diplomacy parameters are elaboration-time parameters that must be arbitrated.
Rocket-chip uses this to let multiple Rocket-cores be instantiated by a single top-level module where each Rocket-core has a different set of elaboration-time parameters.
These are different than TileLink parameters, because TileLink is involved with uncore communication (core to cache, core to memory, core to core (Fact check)).
Diplomacy parameters are carried through a `Parameters` object, which is typically passed implicitly.
This lets components of the system separate from the one that originally set a parameter to modify the parameter if necessary.

The table below is an incomplete list of all parameters Diplomacy can arbitrate and share.

| Name              | Description                             | Common Value |
|-------------------|-----------------------------------------|--------------|
| `CacheBlockBytes` | Number of bytes in a single cache block | Unknown      |

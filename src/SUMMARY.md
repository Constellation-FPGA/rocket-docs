# Summary

[Introduction](./intro.md)

- [Elaboration-Time Parameters](./elaboration-time/parameters.md)
- [Design Constants](./elaboration-time/design-constants.md)
- [Diplomacy Parameters](./diplomacy/parameters.md)
    - [Finding Final SoC Parameters](./diplomacy/final-soc-parameters.md)
- [Individual Modules](./modules.md)
    - [`IBuf` (Instruction Buffer)](./modules/ibuf.md)
    - [`BTB` (Branch Target Buffer)](./modules/btb.md)
    - [`BHT` (Branch History Table)](./modules/bht.md)
    - [`MStatus` (Machine Status)](./modules/mstatus.md)
- [Top-Level Rocket-Core](./rocket-core.md)
    - [Fetch](./rocket-core/fetch.md)
    - [Decode (`id`)](./rocket-core/decode.md)
    - [Execute (`exe`)](./rocket-core/execute.md)
    - [Memory (`mem`)](./rocket-core/memory.md)
    - [Writeback (`wb`)](./rocket-core/writeback.md)

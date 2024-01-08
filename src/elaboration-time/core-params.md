# `CoreParams`
The core parameters (`CoreParams`) is a Scala trait that every Rocket core must implement to be used as a member of the Rocket-chip tile.
Many of the fields are fairly self-explanatory, so they will be skipped for now (e.g. `useSupervisor` controls whether the supervisor privilege mode is supported).

* `instBits`: The number of bits an instruction will be. If the core supports the compressed instruction extension (C), this will be 16, otherwise it will be 32.
* `instBytes`: `instBits` divided by 8.
* `fetchBytes`: The number of bytes to fetch as instructions to fill the instruction buffer.
   This is defined as `fetchWidth * instBytes`

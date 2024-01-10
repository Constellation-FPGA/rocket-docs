# L1 Cache Subsystem

  * `cacheDataBits`: Set by [TileLink](../tile-link.md), the number of bits for a single entry in the cache system.
    ***VERIFY ME!***
  * `cacheDataBytes`: `cacheDataBits` divided by 8.
  * `cacheBlockBytes`: Set by the abstract [`BaseTile`](../tilelink.md) class.
    Taken from the `CacheBlockBytes` [nondiplomatic parameter](../diplomacy/nondiplomatic-parameters.md).
  * `cacheDataBeats`: The number of "beats" required to fill a cache block?
    \\((\mathtt{cacheBlockBytes} * 8) / \mathtt{cacheDataBits}\\).
    By default, this is 128?
    ***FIGURE ME OUT!***
  * `refillCycles`: The number of cycles between the start of a refill request and it being completed?
    Defined to be the same as `cacheDataBeats`.

The caches are built using Diplomatic `DescribedSRAM` modules.
These SRAM modules behave as you would expect, but are also configured using [Diplomacy](../diplomacy.md).
By default, they have \\(4 * 128 = 512\\) bytes per SRAM, set up into

Somehow the L1 caches (at least the instruction ones) get refilled after some time.
I think I figured this out, but this may require further investigation.

# Elaboration-Time Parameters

Elaboration-time parameters are variables that must be provided at elaboration-/compile-time.
They must be passed from the upper/outer instantiating unit (These can simply be passed through too.).
You should never edit these directly, unless you konw what you are doing.
In most cases, these are already set by the Rocket-core itself.
* `iLen`: Instruction length in bits.
* `fetchWidth`: The number of instructions that are fetched per fetch operation.
  A fetch operation will fetch a `coreParams.fetchBits` number of bits at a time.
  `fetchWidth` tells you how many instructions are fetched at a time.
  This is `2` when compressed instructions (RVC) are enabled and `1` otherwise
* `decodeWidth`: The number of `iLen` instructions to handle at once.
* `retireWidth`: The number of `iLen` instructions to retire at once.
   Required to match `decodeWidth`.
* `coreInstBits`: Gotten from the core’s [Core Parameters](./core-params.md).
* `coreInstBytes`: `coreInstBits` divided by 8

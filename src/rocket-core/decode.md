# Decode (`id`)

Gets the IBuf Instruction for this cycle from the IBuf, producing 3 signals:
* `id_expanded_inst`: Gotten by mapping the `DecoupledIO<Instruction>` accessor `_.bits.inst` over a vector of `retireWidth`.
  This is the fully expanded instruction, in the case of compressed instructions.
  In the case of an uncompressed instruction, this is the exact same as the actual instruction.
* `id_raw_inst`: Gotten by mapping the `DecoupledIO<Instruction>` accessor `_.bits.raw` over a vector of `retireWidth`.
  The raw bits underlying this instruction.
* `id_inst`: The bits of an instruction, translated to an actual `Instruction` object.

# `Frontend` and `FrontendModule`
`Frontend` and `FrontendModule` are lazy modules, which requires two classes to be created.
  1. `Frontend` extends `LazyModule`, which makes it the outer wrapping class.
      It instantiates the `FrontendModule` lazily using the `lazy` keyword.
  2. `FrontendModule` extends `LazyModuleImp`, providing an implementation for the lazy `Frontend` module.

The `Frontend` module does relatively little work (just connecting some signals to/from the lazy module), so we only discuss the `FrontendModule` implementation.

## `FrontendReq`

## `FrontendResp`

## `FrontendIO`
Combines many signals together for communicating between the main core and the frontend instruction fetcher/buffer.
These signals include:
  * [`FrontendReq`](#frontendreq)
  * [`FrontendResp`](#frontendresp)
  * [`BTBUpdate`](./btb.md)
  * [`BHTUpdate`](./bht.md)
  * [`RASUpdate`](./ras.md)

## `FrontendModule`
Has a TLB, using the TLB parameters provided by the configuration system.

<div class="warning">
The <code>FrontendModule</code> requires that your core and ICache parameters satisfy <code>fetchWidth * coreInstBytes == fetchBytes</code>.
</div>

There are three stages of fetching through the frontend:
  1. `s0_`
  2. `s1_`
  3. `s2_`

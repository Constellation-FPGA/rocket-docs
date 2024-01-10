# `ICache` and `ICacheModule`
`ICache` and `ICacheModule` are lazy modules, which requires two classes to be created.
  1. `ICache` extends `LazyModule`, making it the outer wrapping class.
      It instantiates the `ICacheModule` lazily using the `lazy` keyword.
  2. `ICacheModule` extends `LazyModuleImp`, providing an implementation for the lazy `ICache` module.

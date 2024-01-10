# Nondiplomatic Parameters
Some parameters are passed through the `Parameters` object (like normal Diplomacy parameters), but are **not** computed with diplomacy negotiation.
This makes them safe to use while diplomacy *is* running the negotiation.
Most of these are parameters are ones that the designer provides at design configuration-time and control the core's internals, rather than its interface.
One example of these is the `usingVM` parameter, which is passed by the designer and does not affect tile communications or Diplomacy.

| Name              | Description                                 | Default Value | Set Where?                                                                         |
|-------------------|---------------------------------------------|---------------|------------------------------------------------------------------------------------|
| `cacheBlockBytes` | The number of bytes per block in the cache. | 64            | Done by `WithCacheBlockBytes` mixin.<br>Actual setting-place is currently unknown. |

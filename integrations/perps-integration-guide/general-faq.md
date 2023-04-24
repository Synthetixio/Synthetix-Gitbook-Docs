# General FAQ

### General questions about PerpsV2 contracts

> The way we currently define and interact with a futures market is via the IFuturesMarket.sol interface. We find the market address via marketForKey mapping, which will not break with perpsV2, correct?

For PerpsV2 you need to use a compiled interface or ABI (We can provide this. Compiling everything that is routed/proxied, i.e. `Market`, `MarketViews`, `DelayedOrders` and `OffchainOrders`).

> Keys will just change from sETH to snxETH or how will that be determined (just wanting to make sure I am clear on this before going forward)?

The synths won't change in PerpsV2, that will happen in PerpsV3. New perp markets will have a new name e.g. ETH would be pETH-perps.

> Previously, `IFuturesMarket.sol` contained both functions to interact with the market (i.e. deposit margin etc.) and also related view functions (i.e. what is the baseAsset()). This is no longer the case with PerpsV2. Why was this decision made?

To break the behavior in different sub-contracts (routed calls). Again, we will provide an interface containing all or something like that as a helper).

> `modifyPositionWithTracking()` now requires a `priceImpactDelta` parameter, why was this added? How would you recommend we set this for users? Pre-defined value or let them decide similar to how it is done when executing swaps on AMM's?

See price impact section below for more details. We recommend setting a reasonable default for users.

> Can you briefly walk through the mechanics of how that works just so I can confirm my mental model is accurate? For example, the address the `FuturesMarketManager` will return for a PerpsV2 market key will be a proxy address. And these addresses will never change but allow the implementation to later be changed?

Basically yes, the proxy will be their point of contact with the PerpsV2 and won't (or shouldn't) change in the future. If it changes it means the proxy is broken.

---
description: This is the migration guide from FuturesV1 to V2
---

# FuturesV1 -> PerpsV2 (Mintaka)

## Preamble

Synthetix FuturesV1 (or Futures as it was also called) from March 2022 is coming to an end (December 2022) and replaced with the long anticipated Perps V2. This document aims to provide a guide on differences between the two versions and how protocols and dApps can migrate their clients to use Perps V2.&#x20;

## Contracts

All existing FuturesV2 haven't changed (except the `FuturesMarketManager`). All new additions reside in `PerpsV2` contracts. You can find them in the same location as all other Synthetix contracts [here](https://github.com/Synthetixio/synthetix/tree/futuresV2/contracts). Take a look at the [Perps Integration Guide](../) for more details on the structure.

## Open/Close a Position

FuturesV1 had two methods of opening a new position: atomically and next-price. Atomic orders remain the same however next-price has been renamed to delayed orders. For the full details refer to the PRs available below:

{% embed url="https://github.com/Synthetixio/synthetix/pull/1899" %}
New delayed orders
{% endembed %}

PerpsV2 also introduces a new method of opening orders via off-chain delayed orders. Please refer to the complete [perps integration guide](../) for details.

## Funding Rates/Velocity

Funding has changed. In FuturesV1, they were instantaneous but in PerpsV2, funding rate floats and drifts in one direction or the other based on skew. Lots of internal implications but minimal external visible changes for frontends. You can read through how it all works here:

{% embed url="https://sips.synthetix.io/sips/sip-279/" %}
Official SIP-279
{% endembed %}

{% embed url="https://github.com/davidvuong/perpsv2-funding" %}
Python sample implementation
{% endembed %}

_For more details on funding and velocity, please refer to the full integration guide._

{% hint style="info" %}
FuturesV1 had funding rate signs inverted. This is no longer the chance in PerpsV2 and the `.neg` is not necessary. Additionally, due to the floating funding rate, you can calculate the hourly funding rate by just `.div(24)`.
{% endhint %}

## Price Impact & Protection

Orders in PerpsV2 incur price impact. This was previously not the case in Perps v1beta. In short, if the position’s size increases/expands the market skew, they are charged a premium in the form of a higher fill price but if the skew is decreases/contracts, a discount is applied. This happens automatically when a trade is made and it affects both spot and delayed orders.

We provide a `fillPrice` function to see the impact of size before a trade is executed:

```solidity
function fillPrice(int size) external view returns (uint price, bool invalid);
```

It may be beneficial to display the fill price as a result of size impact somewhere in the UI so traders know how their position size will impact their trade.

In short, it’s effectively just:

```
fill_price = (
  (price * (1 + skew / skew_scale)) + (price * (1 + (skew + pos_size) / skew_scale))
) / 2
```

This is documented in [SIP-279](https://sips.synthetix.io/sips/sip-279/). You can read the full details in the perps integration guide.

## Trade Simulations

`postTradeDetails` still remains but added is a `tradePrice` argument to specify an allowing a simulation to occur with an arbitrary price.

```solidity
function postTradeDetails(
  int sizeDelta,
  uint tradePrice,
  address sender
)
  external
  view
  returns (
    uint margin,
    int size,
    uint price,
    uint liqPrice,
    uint fee,
    IPerpsV2MarketBaseTypes.Status status
  );
```

## Miscellaneous

### Cross-side Maker/Taker Fees

Traders are charged `makerFee` if the size of their order reduces the market skew and a `takerFee` if the order increases the skew. However, in certain situations, an order can decrease and increase the skew. In these scenarios, the proportion of size that decreases the skew should be charged a `makerFee` and the remaining, a `takerFee`.

This is a bug in Perps v1beta that has now been fixed to be such that if the position flips the skew then maker/taker fees are charged proportionately. For example:

You can use the same `orderFees` view to grab the fees associated with an order. There should be no integration impact, just something to be aware of.

```solidity
function orderFee(int sizeDelta) external view returns (uint fee, bool invalid);
```

{% embed url="https://github.com/Synthetixio/synthetix/pull/1906" %}
PR for cross-side maker/taker fees for details
{% endembed %}

### Native vs. USD Denomination

Internally within market contracts, parameters for OI caps and `skewScale` are denominated in USD. For example:

```json
{
  "maxMarketValueUSD": 4000000,
  "skewScaleUSD": 300000000
}
```

The above signals that the max OI cap for either side is 4M USD and the `skewScale` to convert market skew into a fractional is 300M USD. This is no longer the case. Instead, we use the market asset as the denominator. So, if this market was the ETH then:

```json
{
  "maxMarketValue": 20000,
  "skewScale": 1000000
}
```

So if the price of ETH was $1200 then 20,000 `maxMarketValue` would be 24M OI cap.

Externally, this may/may not impact integration depending on what data you want to display on the UI. Something to be aware of as traders may hit OI caps for e.g. and wonder why.

### Tracking Codes

They remain unchanged. Tracking codes sent in FuturesV1 will still be emitted in events in PerpsV2. Please continue to use the same tracking code unless otherwise specified.

### Market Keys

We’ve changed our `marketKey` for PerpsV2 markets:

```solidity
// Previous (FuturesV1)
sBTC
sETH
sXXX

// Now (PerpsV2)
sBTCPERP
sETHPERP
sXXXPERP
```

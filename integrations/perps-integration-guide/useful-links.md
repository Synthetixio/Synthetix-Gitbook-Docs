---
description: Links for integrators and developers
---

# Useful Links

### Also see&#x20;

{% content-ref url="../../synthetix-ecosystem/community-infrastructure.md" %}
[community-infrastructure.md](../../synthetix-ecosystem/community-infrastructure.md)
{% endcontent-ref %}

### PerpsV2MarketSettings

Markets on PerpsV2 are highly configurable. `PerpsV2MarketSettings` is another top-level contract used for the storage and retrieval of market specific (and system wide) parameters, segregated by `marketKey`.

{% hint style="info" %}
It's always a good idea to query for parameter values rather than hardcoding it yourself. For example, fetching `maxMarketValue` then having your dapp automatically adapt to an increase of OI cap allows your integration to automatically benefit without needing to constantly monitor and update based on upstream changes.
{% endhint %}

Parameters range from small to impactful and can only be updated through passed [SCCPs](../../dao/how-to-write-sip-sccps.md). Below are some commonly queried parameters:

| Parameter                      | Description                                                            |
| ------------------------------ | ---------------------------------------------------------------------- |
| `makerFeeDelayedOffchainOrder` | Fee charged when order contracting skew                                |
| `takerFeeDelayedOffchainOrder` | Fee charged when expands skew                                          |
| `maxLeverage`                  | Largest allowable size on an open position                             |
| `maxMarketValue`               | Market OI cap on either short/long                                     |
| `minKeeperFee`                 | Minimum fee in sUSD paid to keeper for liquidating or executing orders |

For a complete list, refer to the Dune Dashboards below:

{% embed url="https://dune.com/meb/snx-settings" %}
PerpsV2MarketSettings Dune Analytics
{% endembed %}

{% embed url="https://dune.com/synthetix_community/perps-impact" %}
Table view of Perps V2 settings and calculations
{% endembed %}



### Trade, position and candle data

{% embed url="https://thegraph.com/hosted-service/subgraph/synthetix-perps/perps" %}
Subgraph for analyzing trades, wallets and markets
{% endembed %}

### Detailed Perps dashboards

{% embed url="https://dune.com/synthquest/synthetix-perps-v2" %}
Community dashboard for common metrics
{% endembed %}

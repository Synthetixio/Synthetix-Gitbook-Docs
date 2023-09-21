# Tracking Codes

## What is a Tracking Code?

Synthetix generates revenue via fees collected through the use of different [synthetic assets](../../synthetix-protocol/synthetic-assets/) (e.g. atomic swaps & perps). One such method are maker/taker fees charged on entry/exit of perp positions. Protocols and dapps that wish to partner and/or integrate with Synthetix, can receive a portion of fees relative to volumes generated.

A `trackingCode` is used to associate and attribute volume generated through atomic and delayed orders.

## Obtaining a Tracking Code

Tracking codes are ad-hoc and differ on a case by case basis. They are used to attribute volume. If you would like to receive a `trackingCode`, please reach out in [#dev-portal](https://discord.com/channels/413890591840272394/459603818246701056) channel on [Synthetix Discord](https://discord.gg/synthetix).

## Volume Attribution

To attribute volume to a tracking code, we provide an amended `withTracking` method for each market modification call. This allows you to specify a `trackingCode` as the last argument. If a position is successfully opened a  `PerpsTracking` event is emitted and used for fee revenue attribution.

```solidity
function modifyPositionWithTracking(
    int sizeDelta,
    uint priceImpactDelta,
    bytes32 trackingCode
) external;

function submitOffchainDelayedOrderWithTracking(
    int sizeDelta,
    uint priceImpactDelta,
    bytes32 trackingCode
) external;
```

# PerpsV2 Mintaka -> Almach

## Preamble

The Almach release marks the final set of significant improvements made against PerpsV2 whilst on the v2x system (barring any bugs or major issues). Unfortunately a small portion of improvements are backwards incompatible and has implications for those building keepers for liquidations, subgraphs for frontends, and contract interfaces for integrators.

This guide aims to provide details of each improvement and remedies for migration where exists.

Pull Request: [https://github.com/Synthetixio/synthetix/pull/1994](https://github.com/Synthetixio/synthetix/pull/1994)

## Improvements & Remedies

### New Liquidation Mechanism

You can read the full details described in [SIP-2005](https://sips.synthetix.io/sips/sip-2005/). This change has implications for existing liquidation keepers.

* `canLiquidate` no longer returns `true` when a liquidation can be liquidated but rather `true` when an account can be flagged for liquidation
* `liquidatePosition` can only liquidate a flagged position. Both the flagger and and liquidator are rewarded with fees upon liquidation. To flag a position, invoke `flagPosition(address account)`
* Once a position is flagged, no modifications can be made until they are liquidated.
* A `PositionFlagged(uint id, address account, address flagger, uint timestamp);` event is emitted when a position is flagged
* Two additional statuses pertaining to liquidations have been added to the `Status` enum: `PositionFlagged` and `PositionNotFlagged`

### Order Submission

You can find more details in [SIP-2004](https://sips.synthetix.io/sips/sip-2004/). These changes have implications for frontends that interact with the PerpsV2 contracts.

* `priceImpactDelta` provided during order submission (open and close) for both off-chain orders, delayed orders, and atomic orders have been replaced with `desiredFillPrice`. You can and should still allow for user configurable slippage as input. However, to derive a `desiredFillPrice`, you can:
  * `desiredFillPrice = side == 'short' ? fillPrice * (1 - priceImpactDelta) : fillPrice * (1 + priceImpactDelta)`
* A `close` convenience function has been introduced for off-chain and delayed orders:
  * `submitCloseOffchainDelayedOrderWithTracking`
  * `submitCloseDelayedOrderWithTracking`
  * This behaves the same as `submit{Offchain}DelayedOrder` but without the need to specify a `sizeDelta`
* Off-chain and delayed orders no longer charge a commitment fee on submission. We also don't allow order cancellations until the orders become stale (i.e. past the window of settlement)
* A subtle change has been made to all delayed order argument parameters for consistency
  * `submitDelayedOrder(int sizeDelta, uint desiredTimeDelta, desiredFillPrice)`
  * &#x20;`submitDelayedOrderWithTracking(int sizeDelta, uint desiredTimeDelta, desiredFillPrice, bytes32 trackingCode)`
  * `desiredTimeDelta` always comes before `desiredFillPrice`. Previously it was inconsistent between methods
* Orders that reduce a position, so long as the resulting position is not liquidatable will always be allowed and no longer will revert

### Misc.

* `InvalidOrderPrice` removed from `Status` enum
* `InvalidOrderType` added to `Status` enum
* The `PositionModified` event has been extended to include an additional `skew` property

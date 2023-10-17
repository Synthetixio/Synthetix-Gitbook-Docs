# Liquidations

#### Liquidations & Synthetix Staking

When a staker's Collateralization Ratio (C-Ratio) falls below the liquidation ratio, they are subject to liquidation, a risk management mechanism crucial for maintaining the protocol's stability. If the staker's C-Ratio doesn't improve within a certain period, protocol users will take action to rectify the situation by liquidating a portion of their staked SNX.

#### The Process

Upon falling below the required C-Ratio (see [current-protocol-parameters.md](../current-protocol-parameters.md "mention")), stakers enter a period during which they must rectify their C-Ratio. Failure leads to one of the following scenarios, each with distinct implications and penalties:

1. **Forced Liquidation:**
   * If a staker does nothing after being flagged, the protocol enforces liquidation. A penalty applies not to their total staked SNX but to the amount that is liquidated to bring their C-Ratio back to the target.
   * This penalty, often around 60%, is redistributed within the protocol, incentivizing active participation and penalizing negligence.
2. **Self-Liquidation:**
   * Stakers proactive in managing their stakes may opt for self-liquidation, incurring a smaller penalty, typically around 50% on the portion of SNX being liquidated.
   * This approach offers a less punitive measure for those seeking to exit their positions or reduce their exposure deliberately.
3. **Rebalancing to Avoid Liquidation:**
   * Stakers who adjust their C-Ratio promptly, either by burning sUSD or by additional staking to elevate their C-Ratio above the protocol's target, will avoid any liquidation process.
   * It demonstrates responsible staking behavior, contributing positively to network stability.
4. **Option for Self-Liquidation at Any Time:**
   * The protocol may offer mechanisms for stakers to initiate self-liquidation even before reaching critical thresholds, providing greater control over their staking positions and potential outcomes.

#### Why Are Liquidations Vital to the Protocol?

Liquidations serve multiple essential functions:

* They enforce discipline among stakers, ensuring that everyone within the network maintains adequate collateral levels.
* Active network participants can help stabilize the overall network C-Ratio by initiating liquidation processes for at-risk stakers.
* They help address the issue of 'zombie' wallets, which, due to lost keys or abandonment, no longer contribute actively to network health.

#### Example of a Liquidation

Consider a staker, Bob, who begins with a healthy position but experiences market volatility that jeopardizes his C-Ratio:

Bob stakes 1000 SNX and mints 1000 sUSD. With SNX at $2, his collateral is worth $2000, and his C-Ratio is 200%. If the SNX price drops to $1.50, his collateral value falls to $1500, pushing his C-Ratio down to 150% and triggering the liquidation process.

If Bob's position is forcibly liquidated (scenario 1), the protocol will determine how much SNX needs to be sold to restore Bob's C-Ratio to the 400% target. The penalty applies to this portion, not the entirety of Bob's staked SNX. For instance, if 250 SNX needs to be liquidated, a 60% penalty means losing 150 SNX, with the remaining 100 SNX used to repurchase sUSD and burn it to restore the C-Ratio.

If Bob opts for self-liquidation (scenario 2), he might face a 50% penalty on the liquidated SNX, reducing his loss slightly in the process of C-Ratio restoration.

Alternatively, if Bob manages to rebalance his stake (scenario 3), by adding more SNX or burning some sUSD, he could maintain or even improve his C-Ratio, thus avoiding any penalties.



Note: Please refer to [current-protocol-parameters.md](../current-protocol-parameters.md "mention") for the most updated variables

# Liquidations

## Liquidations & Synthetix Staking

When a staker's C-Ratio falls below the liquidation ratio, they become eligible for liquidation. Their SNX collateral can then be liquidated after a set amount of time. This process is similar to how a DeFi protocol like AAVE liquidates a borrower if their collateral dips below the required liquidation ratio.

Once a staker's C-Ratio drops below the liquidation ratio (find the current ratio at [current-protocol-parameters.md](../current-protocol-parameters.md "mention")), they will be flagged and have 12 hours to raise their C-Ratio. In this situation, one of the following scenarios will occur:

1. Your C-Ratio falls below the liquidation ratio, you are flagged but do not self-liquidate.
   * You will be liquidated, incurring a forced liquidation penalty on your staked SNX. Your SNX will be used to pay off your debt, leaving you with the remainder. The penalty SNX will be distributed to other stakers.
2. Your C-Ratio falls below the liquidation ratio, you are flagged, and you self-liquidate. Your liquidated SNX will be used to pay off your debt, leaving you with the remainder.
   * You will be liquidated, incurring a self-liquidation penalty on your staked SNX. The penalty SNX will be distributed to other stakers.
3. Your C-Ratio is above the target C-Ratio after being flagged because you burned sUSD or minted new debt.
   * Nothing will happen; you will not be liquidated.
4. Alternatively, you can utilize the self-liquidation mechanism at any point below the target ratio.

### Why are Liquidations Vital to the Protocol?

* Liquidations create a stronger incentive for stakers to maintain a healthy C-Ratio. If they fail to do so, they will be liquidated with a penalty.
* This process encourages a healthier network C-Ratio, as other network participants can actively improve the network C-Ratio by liquidating stakers below the liquidation ratio.
* Liquidations provide a solution for staking wallets that have been abandoned or whose private keys have been lost, as they will no longer negatively impact the network C-Ratio.

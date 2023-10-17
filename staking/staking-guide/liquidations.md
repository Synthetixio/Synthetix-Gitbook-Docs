# Liquidations

### Liquidations & Synthetix Staking

When a staker's Collateralization Ratio falls below the liquidation ratio, they become eligible for liquidation. Their SNX collateral can then be liquidated after a set amount of time. This process is similar to how a DeFi protocol like AAVE liquidates a borrower if their collateral dips below the required liquidation ratio.

Once a staker's C-Ratio drops below the liquidation ratio (find the current ratio at [Current Protocol Parameters](../current-protocol-parameters.md)), they will be flagged and have 6 hours to raise their C-Ratio. In this situation, one of the following scenarios will occur:

1. Your C-Ratio falls below the liquidation ratio; you are flagged but do not self-liquidate.
   * You will be liquidated, incurring a forced liquidation penalty of 60% on your staked SNX. Your SNX will be used to pay off your debt, leaving you with the remainder. The penalty SNX will be distributed to other stakers.
2. Your C-Ratio falls below the liquidation ratio, you are flagged, and you self-liquidate. Your liquidated SNX will be used to pay off your debt, leaving you with the remainder.
   * You will be liquidated, incurring a self-liquidation penalty of 50% on your staked SNX. The penalty SNX will be distributed to other stakers.
3. Your C-Ratio is above the target C-Ratio of 400% after being flagged because you burned sUSD or minted new debt.
   * Nothing will happen; you will not be liquidated.
4. Alternatively, you can utilize the self-liquidation mechanism at any point below the target ratio.

#### Why are Liquidations Vital to the Protocol?

* Liquidations create a stronger incentive for stakers to maintain a healthy C-Ratio. If they fail to do so, they will be liquidated with a penalty.
* This process encourages a healthier network C-Ratio, as other network participants can actively improve the network C-Ratio by liquidating stakers below the liquidation ratio.
* Liquidations provide a solution for staking wallets that have been abandoned or whose private keys have been lost, as they will no longer negatively impact the network C-Ratio.

#### Example of a Liquidation

Let's consider a staker named Bob.&#x20;

Bob has staked 1000 SNX  and minted 1000 sUSD, which gives him a C-Ratio of 200% (1000 SNX \* $2 SNX price = $2000 in SNX / 1000 sUSD = 200%). The liquidation ratio is 160%, and the target C-Ratio is 400%. Refer to [current-protocol-parameters.md](../current-protocol-parameters.md "mention") for most updated variables.

If the price of SNX falls to $1.50, Bob's C-Ratio will drop to 150% (1000 SNX \* $1.50 SNX price = $1500 in SNX / 1000 sUSD = 150%), which is below the liquidation ratio. Bob is now flagged for liquidation and has 6 hours to raise his C-Ratio.

* If Bob does nothing (or raises his C-Ratio below the target) and the 6 hours pass, the system will liquidate his position. He will incur a 60% penalty on his staked SNX, meaning 600 SNX will be taken from his stake and distributed to other stakers. The remaining 400 SNX will be used to pay off his debt, and any leftover SNX will be returned to him.
* If Bob chooses to self-liquidate, he will incur a 50% penalty on his staked SNX, meaning 500 SNX will be taken from his stake and distributed to other stakers. The remaining 500SNX will be used to pay off his debt, and any leftover SNX will be returned to him.
* If Bob manages to increase his C-Ratio above the target C-Ratio of 400% within the 6 hours by burning sUSD or minting new debt, he will avoid liquidation.

This mechanism ensures that stakers are incentivized to maintain a healthy C-Ratio, contributing to the overall health and stability of the Synthetix network.

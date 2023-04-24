# Collateralization Ratio

### Quick Summary

* The Collateralization Ratio (C-Ratio) is a dynamic variable that changes based on the staked SNX value and active debt.
* Active debt is influenced by trader performance, net of fees. If traders are profitable, active debt increases, but if they aren't, active debt decreases. However, Synthetic Assets such as Synthetix Perps have innovative risk management tools in place to ensure that they remain delta neutral. To learn more, visit [perpetual-futures.md](../../synthetix-protocol/synthetic-assets/perpetual-futures.md "mention").
* The Target C-Ratio, set by governance, determines staker rewards; stakers at or below the Target C-Ratio during the weekly staking snapshot (Wednesday) receive the maximum staking rewards.
* Target C-Ratio is critical for incentivizing participation by stakers and ensuring proper collateralization of the Synthetix protocol.

### Deeper Explanation of Collateralization Ratio

An account's **collateralization ratio** (or **c-ratio** for short) represents the ratio between its active debt and available SNX being staked, expressed as a percentage.

Active debt refers to the dynamic proportion of the Synthetix global debt pool that a staker is responsible for creating.

> **Practical Example:**
>
> * If you are responsible for 10% of the debt pool and the overall debt pool is 100,000, your current active debt is 10,000.
> * If traders are profitable and the debt pool increases to 200,000, your active debt becomes 20,000.
> * If traders are not profitable and the debt pool decreases to 50,000, your active debt becomes 5,000.
>
> **C-Ratio Calculation:** C-Ratio % = (total SNX value USD / active debt value USD) \* 100

Since both SNX value and active debt are constantly fluctuating, your c-ratio changes accordingly.

The **Target c-ratio** is a static, system-wide ratio applicable to all stakers equally. It determines the over-collateralization required for collateral in the system. This ratio is set through governance, and its current value can be found on the [current-protocol-parameters.md](../current-protocol-parameters.md "mention")page.&#x20;

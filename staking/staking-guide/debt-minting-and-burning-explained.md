# Understanding Debt, Minting, and Burning

#### Overview of Debt Dynamics in Synthetix

* **Active Debt**: This is your share of the global debt pool in the Synthetix system. The composition and value of this pool fluctuate, impacting your active debt proportionally. You can view the current debt pool composition at [Debt Pool Overview](https://staking.synthetix.eth.limo/debt/overview).
* **Issued Debt**: When you stake SNX and mint sUSD, the initial value of this sUSD is your issued debt.

#### Minting: Creating Synths

* **Process**: Minting is done by staking SNX as collateral to generate sUSD (synths), which in turn increases your active debt.
* **Purpose**: This process allows you to participate in the Synthetix ecosystem by providing liquidity and earning potential rewards.

#### Burning: Reducing Debt

* **Process**: Burning is the act of destroying sUSD, thereby reducing both your active debt and the overall debt in the system.
* **Impact on C-Ratio**: Burning sUSD improves your Collateralization Ratio (C-Ratio), enabling you to claim rewards and transfer SNX.

#### Practical Application of Minting and Burning

* **C-Ratio Management**: If your C-Ratio falls below the target, you need to burn sUSD to raise it and become eligible for claiming rewards. Conversely, having a C-Ratio above the target means your SNX collateral is not being utilized fully, suggesting the potential to stake more SNX (and mint more sUSD).

#### Active Debt: A Critical Component

* **Dynamic Nature**: Active debt is dynamic, adjusting with the global debt pool's fluctuations due to trading activities within the Synthetix network.
* **Trading Impact**: Profitable trading increases the global debt pool and your active debt; less profitable trading reduces both.
* **Staker Responsibility**: As a staker, you're responsible for eventually repaying this active debt to unlock your SNX collateral.
* **Hedging Strategies**: It's advisable to adopt debt hedging strategies that mirror the overall debt pool. dHEDGE offers an automatic debt hedging solution on Optimism, which you can read about [here](https://blog.synthetix.io/dhedge-debt-mirror-index-token-2/).

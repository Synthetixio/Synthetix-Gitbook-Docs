# Understanding the Collateralization Ratio

**Overview**

* **Collateralization Ratio (C-Ratio)**: This dynamic measure reflects the ratio between the value of staked SNX and active debt within the Synthetix network. It's critical for ensuring the protocol's collateralization and stability.
* **Active Debt Dynamics**: Your active debt is your share of the Synthetix global debt pool, which fluctuates based on the overall system trading performance, net of fees. If traders are profitable, active debt increases, and if they are not, it decreases.&#x20;
  * The concept of active debt in the system is simplified for clarity. In reality, synthetic assets like Synthetix Perpetual Futures feature robust risk management protocols to ensure delta neutrality for liquidity providers. This framework is designed so that for every dollar gained by one trader, there's an equivalent loss by another. Liquidity providers take on temporary market imbalances until another trader is incentivized to take the position.
* **Target C-Ratio**: This is a system-wide static ratio set by governance, essential for determining the over-collateralization needed in the system. Stakers who meet this Target C-Ratio during the weekly snapshot (Wednesday) are eligible for maximum rewards. The current Target C-Ratio value is available on the [Current Protocol Parameters](https://chat.openai.com/o/CgKKbcaDraUAYIovoOdl/s/DwqzB5BTWasJXBHd4rXZ/\~/changes/228/staking/current-protocol-parameters) page.

#### In-Depth Understanding

**Calculating C-Ratio**:

* The C-Ratio is calculated as follows: C-Ratio % = (total SNX value USD / active debt value USD) \* 100
* As the value of SNX and the active debt vary, so does your C-Ratio.

**Practical Example**:

* Imagine you are responsible for 10% of the total debt pool. If the overall debt is 100,000, your active debt is 10,000. This value will increase or decrease based on the trading performance within the network.

**Importance of Maintaining the Target C-Ratio**:

* Achieving or exceeding the Target C-Ratio is crucial for maximizing staking rewards and contributing to the overall health and security of the Synthetix network.

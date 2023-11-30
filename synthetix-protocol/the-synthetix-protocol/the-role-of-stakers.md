---
description: Explaining the importance of stakers within Synthetix
---

# The Role of Stakers

On Synthetix, all liquidity for Synthetix products is created by staking. Staking is an integral part of of the system and provides deep liquidity by locking collateral and maintaining a target c-ratio, which powers all of the products within the Synthetix protocol.

When you stake SNX and mint sUSD, you take on debt reflecting the amount of sUSD that must be burned to unstake your SNX. This debt, which also represents a proportion of all the debt on Synthetix, is denominated in sUSD and increases and decreases in accordance with the supply of Synths and their exchange rates. For example, if half of Synthetix's Synths were synthetic ether (sETH) and the price of ether doubled, then the total debt and each staker's debt would rise by one quarter.

Synthetix staking is vastly different from other DeFi protocols because it allows anyone to earn rewards by contributing collateral to the Synthetix protocol. Staked SNX enables the many benefits for protocols built on Synthetix, such as deep liquidity, low slippage, and highly competitive trading fees.

### Benefits of Staking

Stakers earn weekly rewards for collateralizing the network. These rewards are paid in two ways. One is from trading fees, which are charged to traders. The other is inflationary rewards, which are newly minted SNX tokens held in escrow for a year. Escrow-locked SNX tokens can be staked during this escrow and provide further rewards to stakers.

### Risks of Staking

The rewards stakers earn are not risk-free. The staker is providing collateral for traders to trade against. If traders are profitable, net of fees, stakers profits may decrease.

Additionally, smart contract risk, oracle risks, and other risks are also present when providing collateral and using Synthetix. Please operate at your own risk and do your own research.

### **How SNX and other collateral types back Synthetix Products**

All synths are backed by a mixture of SNX, ETH, LUSD, and other collateral types.

Synths are minted when SNX holders stake their SNX as collateral using the Synthetix staking application, a decentralized application for interacting with Synthetix staking contracts. The system is currently backed by a target collateralization ratio (see [current-protocol-parameters.md](../../staking/current-protocol-parameters.md "mention")), as this is a constantly updated variable through community governance. SNX incurs debt when Synths are minted, and to exit the system (i.e. unlock their SNX), they must pay back this debt by burning Synths.

ETH, LUSD, and additional collateral types (depending on governance inclusion) also back the system as forms of collateral. This means that users can either borrow against these assets, or lock them in a wrapping contract to generate sUSD, sETH, or other synths.

### **Why Stakers Stake**

SNX holders are incentivized to stake their SNX in many ways. Firstly, there are exchange rewards. These are generated whenever someone makes an exchange within the Synthetix system. Each trade generates an exchange fee that is sent to a fee pool, available for stakers to claim their proportion each week. This fee is set by governance, and will be displayed by the SNX integrator before the trade. The other incentive for stakers is SNX staking rewards, which comes from the protocols inflationary monetary policy. These SNX tokens are distributed to SNX stakers weekly on a pro-rata basis provided their collateralization ratio does not fall below the target threshold.

To learn more about staking, please visit the Synthetix Staking guide.

{% content-ref url="broken-reference/" %}
[broken-reference](broken-reference/)
{% endcontent-ref %}

### **Minting, burning, and the C-Ratio**

The mechanisms above ensure SNX stakers are incentivized to maintain their Collateralisation Ratio (C-Ratio) at the target rate. This ensures the Synthetix protocol is backed by sufficient collateral to absorb large price shocks. If the value of SNX or Synths fluctuates, each staker’s C Ratio will fluctuate. If it falls below the target c-ratio (with a small buffer to allow for minor fluctuations), they will be unable to claim fees until they restore their ratio.

They adjust their ratio by either minting Synths if their ratio is above the target c-ratio or burning Synths if their ratio is below the target c-ratio.

### **Stakers, debt, and pooled counterparties**

SNX stakers incur a ‘debt’ when they mint Synths. This debt can increase or decrease independent of their original minted value, based on the exchange rates and supply of Synths within the network.

For example, if 100% of the Synths in the system were synthetic Bitcoin (sBTC), which halved in price, the debt in the system would halve, and each staker’s debt would also halve. This means in another scenario, where only half the Synths across the system were sBTC, and BTC rises 50%, the system’s total debt—and each staker’s debt—would increase by 50%.

In this way, stakers act as a pooled counterparty to all Synthetix Network exchanges; stakers take on the risk of the overall debt in the system. They have the option of hedging this risk by taking positions external to the system. By incurring this risk and enabling trading on Synthetix stakers earn a right to fees generated by the system.

### **Liquidation Risk**

Once a stakers c-ratio goes below the liquidation ratio, they are eligible to be flagged for liquidation. They will then have a set amount of time to raise their c-ratio back to the target c-ratio. If they do not raise their c-ratio, they will be force liquidated with a penalty. If they do raise their c-ratio above the target, their liquidation flag will be removed.

Stakers who experience a liquidation will incur a penalty from SNX liquidated. When a liquidation occurs, SNX in escrow and sUSD debt is distributed to healthy stakers to ensure the system's longterm health.

Users who flag SNX and liquidate accounts for liquidation are rewarded. These rewards incentivize users to run bots that automatically flag stakers for liquidation.

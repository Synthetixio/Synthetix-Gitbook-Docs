---
description: Synthetic perpetual futures
---

# Perpetual Futures

Synthetix Perps is a decentralized perpetual futures exchange with deep liquidity and low fees.&#x20;

Users can trade perps and gain exposure to a range of assets without holding the actual asset. The margin for each position is denominated in sUSD, which can be minted and burned as needed, allowing users to avoid exposure to volatility in the value of their margin and simplifying PnL and liquidation calculations.&#x20;

As the counterparty to all orders, the SNX debt pool takes on the risk of any skew in the market. A perpetual-style funding rate is paid from the heavier to the lighter side of the market to encourage a neutral balance. Perps enable a much expanded and capital-efficient trading experience by enabling leveraged long and short exposure.

### Features

**Off-Chain Oracles**

<figure><img src="https://blog.synthetix.io/content/images/2022/12/Off-chain-Oracle-3_compressed-2.gif" alt=""><figcaption></figcaption></figure>

New off-chain oracles provided by Pyth Network allow perps fees to be reduced to 5-10bps—on par with centralized perps platforms. These oracles, pioneered by SNX, greatly improve the trader experience & minimize the risk of frontrunning attacks. They work as follows: off-chain oracles save prices off-chain and are provided to traders by keepers when a trade is initiated, with an 8-sec delay due to block times. The on-chain validation process includes staleness checks, key-threshold confirm, and a final check against on-chain oracles.

#### Delta Neutral for LP’s & Arbitrage opportunities for traders <a href="#delta-neutral-for-lp-e2-80-99s-arbitrage-opportunities-for-traders" id="delta-neutral-for-lp-e2-80-99s-arbitrage-opportunities-for-traders"></a>

Perps V2 is a novel exchange engine that efficiently matches buyers and sellers, with SNX stakers serving as a temporary counterparty as needed. Perp LP's (stakers) will only take on asset risk temporarily, while incentives reward traders for bringing markets to neutral.

But that's not all – SNX has also made significant strides to minimize the risk that perps LP's (stakers) take on through innovative risk management features. That's why dynamic funding rates and a price impact function have been introduced.

The **price impact function** incentivizes arbitrage traders with a price discount given to traders who return markets to neutral.&#x20;

* Example: The ETH Perp market currently has $100,000 in LONG positions and $20,000 in SHORT positions. Traders who go short would receive a discount for helping to bring the markets back to neutral. However, those who go long would pay a premium.

**Dynamic funding rates** allow funding rates to drift upwards in the presence of continued imbalance, incentivizing arbitrage traders to step in.

* The ETH Perp market currently has $100,000 in LONG positions and $20,000 in SHORT positions.&#x20;
  * If no one enters this market, funding rates will continue to tick upward.&#x20;
  * If traders bring the skew to neutral (100,000 LONG and 100,000 SHORT), funding rates will stay the same.&#x20;
  * If traders flip the skew to SHORT (50,000 LONG and 100,000 SHORT), funding rates will decrease.

Both functions will introduce arbitrage opportunities for traders to keep markets neutral over the long term. This innovative path to risk management will help increase scalability and capital efficiency while supporting a wider range of markets.

## Integration

Are you a developer and want to integrate with our perpetual future contracts? Check out our perps integration guide.

{% content-ref url="../../integrations/perps-integration-guide/" %}
[perps-integration-guide](../../integrations/perps-integration-guide/)
{% endcontent-ref %}

# Synthetix Token (SNX)

The Synthetix Network token (SNX) incentivizes coordination and growth within the Synthetix Network. It has two primary functions: (a) **Staking** and (b) **Governance**.

### Staking

SNX Stakers earn weekly rewards for collateralizing the network. These rewards are paid in two ways. One is from **trading fees**, which are charged to traders. The other is **inflationary rewards**, which are newly minted SNX tokens held in escrow for a year. Escrow-locked SNX tokens can be staked during this escrow and provide further rewards to stakers.

{% content-ref url="broken-reference" %}
[Broken link](broken-reference)
{% endcontent-ref %}

### Inflation Rewards

Synthetix distributes weekly inflation rewards based on [SIP-202: Target Staking Ratio](https://sips.synthetix.io/sips/sip-202/) guidelines and variables set in [SCCP-211](https://sips.synthetix.io/sccp/sccp-211/).

The goal is to achieve a target staking ratio by adjusting the inflation rate weekly. The staking ratio is defined as the percentage of SNX collateral in staked addresses versus the total SNX collateral.

The inflation rate changes per the following rules:

* Staking ratio >70%: Inflation decreases by 5%.
* Staking ratio 60-70%: Inflation decreases by 2.5%.
* Staking ratio <60%: Inflation increases by 5%.

For up-to-date inflation data, see the [Synthetix Inflation Stats](https://flipsidecrypto.xyz/synthquest/q/inflation-table-YVromr).

Please note that these ratios can change based on SCCPs approved by the Spartan Council.

### Governance

Synthetix Stakers are assigned a percentage of debt ownership proportion to their amount of SNX staked. Then their voting weight is quadratically weighted for all but the Treasury Council. Voting is done through the fully on-chain Synthetix Governance Module.

{% content-ref url="../../dao/governance-framework/" %}
[governance-framework](../../dao/governance-framework/)
{% endcontent-ref %}

# Oracles

### What are oracles?

Synthetix utilizes the decentralized **Chainlink** [oracle network](https://chain.link/education/blockchain-oracles) & **Pyth** [oracle network](https://pyth.network/price-feeds?asset-type=crypto\&status=online), which provides up-to-date token prices data to smart contracts on Ethereum and Optimism Mainnet.

{% hint style="success" %}
<mark style="color:blue;">**Responsibilities of an oracle**</mark>

* Updates, stores, and distributes up-to-date token prices relevant to the system.
* Disables exchange functionality if prices are not fresh.
* Provides functionality to perform exchange rate conversions between synth flavors.
{% endhint %}

### How does Synthetix utilize oracles?

The Synthetix protocol utilizes its respective `ExchangeRates` contract to retrieve frequently stored price updates.

### Synthetix Oracle Contracts

At Synthetix, the on-chain manifestation of the oracle is the [`ExchangeRates`](https://docs.synthetix.io/contracts/source/contracts/ExchangeRates/) contract, which stores prices that are frequently updated by the oracle. The primary user of these prices is the [`Synthetix`](https://docs.synthetix.io/contracts/source/contracts/Synthetix/) contract, which needs them to calculate debt allocations when issuing and burning synths, and to determine the correct quantity of synths when performing an exchange of one flavour for another.

It is also used by some other contracts, such as the [`Depot`](https://docs.synthetix.io/contracts/source/contracts/Depot/) and [`PurgeableSynth`](https://docs.synthetix.io/contracts/source/contracts/PurgeableSynth/) contracts.

### Constituent Contracts

| Contract        | Description                                                                                                                                                                                                                                                                                                         |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Oracle`        | The oracle is responsible for collecting and updating all token prices known to the Synthetix system. Although it is not a contract, it controls a known Ethereum address from which price updates are sent to the [`ExchangeRates`](https://docs.synthetix.io/contracts/source/contracts/ExchangeRates/) contract. |
| `ExchangeRates` | The Synthetix exchange rates contract which receives token prices from the oracle, and supplies them to all contracts that need it.                                                                                                                                                                                 |
|                 |                                                                                                                                                                                                                                                                                                                     |

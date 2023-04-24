# Lyra - Options

Lyra is an options automated market maker (AMM) that allows traders to buy and sell options on cryptocurrencies against a pool of liquidity. The Lyra protocol has two key user groups, liquidity providers and options traders.

Liquidity providers (LPs) deposit sUSD (a stablecoin) into one of the asset-specific Lyra Market Maker Vaults (MMVs). This liquidity is used to make two-sided (buy and sell) options markets for the asset that the vault specifies (e.g. ETH Market Maker Vault LPs quote options on ETH). LPs deposit liquidity to the vault to earn the fees paid when options are traded.

Traders use Lyra to trade options. They can either buy options from or sell options to the MMV. Traders pay fees (in the form of the market-making spread) to LPs, as compensation for their liquidity.

Lyra uses the Synthetix Protocol in [three different ways](https://docs.lyra.finance/overview/how-does-lyra-work/synthetix):

* As a settlement currency (sUSD)
* As collateral for calls
* For delta hedging

Learn more about Lyra by visiting the [Lyra docs](https://docs.lyra.finance/developers/contracts) or the [Lyra dapp](https://app.lyra.finance/#/portfolio).

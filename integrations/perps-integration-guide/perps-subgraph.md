# Perps Subgraph

There are subgraphs that provides all the necessary information for a perp trading front end. Available networks are Optimism:

{% embed url="https://thegraph.com/hosted-service/subgraph/synthetix-perps/perps" %}
Optimism Mainnet subgraph for production
{% endembed %}

### Entities

In the list below you find all entities that the subgraph has to offer.

* Frontends: gives you information about integrators, which market they traded on and their names.
* FuturesPositionLiquidated: gets created every time there is a liquidation. You get information about size and fee, but also about the trader and the position.
* PositionFlagged: gets created when a position is close to liquidation.
* Trader: is an accumulative entity that keeps track of a trader's stats, pnl, liquidations etc.
* FuturesTrade: this entity gets created every time there is an interaction with the position. When it gets opened, modified, closed or liquidated. This entity is helpful when you would like to know how much volume a market did in one day, or if you are interested in the history of a position.
* Synthetix: this entity is like the trader entity, although only one ever will exists. It keeps track of total volume that has flown through the system, how much fees got generated etc.
* FuturesPosition: as the name suggests, this entity gives you all the information about a position.
* FuturesOrder: this entity is almost like the futures trade entity but serve the purpose of keeping track of position that are submitted through a different way. There are:  `DelayedOrder`, `DelayedOffchainOrder` and `NextPriceOrder`. Once a futures order gets executed, it creates a futures trade entity and a futures position.
* FundingRateUpdate: every time there is a funding rate update on a market, a new entity of this type will get created and helps to compute the pnl for the futures position and trade entity. Also, it allows the consumer to see the historic movement of the funding rate.&#x20;
* FuturesMarginTransfer: when a trader deposits or withdraw margin from a market, this entity will get created.
* FuturesMarket: lists all available market that got emitted from the FuturesMarketManager contract.

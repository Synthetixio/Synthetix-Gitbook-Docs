# Technical Integration

## Preamble

This guide is for new integrators starting from scratch. If you have an existing v1 integration and want to migrate to V2 then refer please to [futuresv1-greater-than-perpsv2-mintaka.md](migration-guides/futuresv1-greater-than-perpsv2-mintaka.md "mention").

## Contracts

All `PerpsV2` contracts are routed proxies. That is, for the most part, there's a single entry point to perform most of your integration needs. You can see all available `PerpsV2` contracts on GitHub by filtering by `PerpsV2` prefix or infix on `.sol` file names (see [GitHub](https://github.com/Synthetixio/synthetix/tree/develop/contracts)). Here is a quick snapshot:

```
> tree contracts | grep 'PerpsV2*'
├── MixinPerpsV2MarketSettings.sol
├── PerpsV2ExchangeRate.sol
├── PerpsV2Market.sol
├── PerpsV2MarketBase.sol
├── PerpsV2MarketData.sol
├── PerpsV2MarketDelayedExecution.sol
├── PerpsV2MarketDelayedIntent.sol
├── PerpsV2MarketLiquidate.sol
├── PerpsV2MarketProxyable.sol
├── PerpsV2MarketSettings.sol
├── PerpsV2MarketState.sol
├── PerpsV2MarketStateLegacyR1.sol
├── PerpsV2MarketViews.sol
├── ProxyPerpsV2.sol
│   ├── IPerpsV2ExchangeRate.sol
│   ├── IPerpsV2Market.sol
│   ├── IPerpsV2MarketBaseTypes.sol
│   ├── IPerpsV2MarketBaseTypesLegacyR1.sol
│   ├── IPerpsV2MarketConsolidated.sol
│   ├── IPerpsV2MarketDelayedExecution.sol
│   ├── IPerpsV2MarketDelayedIntent.sol
│   ├── IPerpsV2MarketLiquidate.sol
│   ├── IPerpsV2MarketSettings.sol
│   ├── IPerpsV2MarketState.sol
│   ├── IPerpsV2MarketViews.sol
    ├── MockPerpsV2Market.sol
    ├── MockPerpsV2StateConsumer.sol
    ├── TestablePerpsV2Market.sol
    ├── TestablePerpsV2MarketEmpty.sol
```

There are 3 primary points of interaction: `ProxyPerpsV2`, `PerpsV2MarketSettings`, and `FuturesMarketManager` (note: does not have a `PerpsV2` prefix/suffix).

### ProxyPerpsV2

Each PerpsV2 market is deployed as a distinct instance of the `ProxyPerpsV2` contract, uniquely identified by a `marketKey`. Below are all available PerpsV2 markets:

#### Optimism

| Market Key | Address                                    |
| ---------- | ------------------------------------------ |
| sETHPERP   | 0x2B3bb4c683BFc5239B029131EEf3B1d214478d93 |

#### Optimism Goerli

| MarketKey | Address                                    |
| --------- | ------------------------------------------ |
| sETHPERP  | 0x111BAbcdd66b1B60A20152a2D3D06d36F8B5703c |
| sBTCPERP  | 0xd5844EA3701a4507C27ebc5EBA733E1Aa2915B31 |

Due to contract size limitations, we've designed `ProxyPerpsV2` to be a router of sorts. The router proxies calls downstream to a collection of registered targets, which can be described by calling `getAllTargets` on `ProxyPerpsV2`. Although an implementation detail and likely not impactful for integration, it may helpful to understand how these contracts link together.

In the past, we've found integrating with proxy contracts can sometimes be difficult to work with as definitions are scattered across an array of different targets. For simplicity, we've defined a consolidated interface for ABI generation which can be found [here](https://github.com/Synthetixio/synthetix/blob/develop/contracts/interfaces/IPerpsV2MarketConsolidated.sol).

### FuturesMarketManager

As the name would suggest, it's simply just a management contract for markets available on perps. It's a top-level contract that provides a holistic scan of all available markets, consolidated views to query data in aggregate, and acts as a registry to track new markets as they are deployed.&#x20;

Although this does not provide mutative methods to perform actions externally (as mutative operations are applied on the market level), it may be useful during debugging/integration to retrieve metadata for either display or inference or even to help avoid hardcoded values in your keepers.

### PerpsV2MarketSettings

_Checkout the_ [useful-links.md](useful-links.md "mention") _section for details._

### Contract Addresses

{% embed url="https://github.com/Synthetixio/synthetix-docs/blob/master/content/addresses.md" %}
_As of writing this, PerpsV2 is only available on Optimism._
{% endembed %}

## How to Transfer Margin

All PerpsV2 markets have isolated margin. Position A on the ETH market will not affect position B on the BTC market. This is important as it means margin must always be transferred before positions can be opened on new markets.

```solidity
interface IPerpsV2Market {
  function transferMargin(int marginDelta) external;
}
```

```typescript
const market = new Contract(address, abi, signer);

const marginDelta = BigNumber.from(100);
await market.transferMargin(marginDelta);
```

A positive `marginDelta` is considered a deposit, negative is a withdrawal and zero is a no-op. To ensure users do not receive revert errors refer to the `minInitialMargin` on the minimum required margin a position must have.

## How to Open a Position

There is only 1 recommended method to open a position: **delayed off-chain orders**.

{% hint style="warning" %}
We **STRONGLY** recommend you integrate using **delayed off-chain orders**, but will document the other order types too at the bottom of this section. In future version, its possible that the inferior order types will be removed.
{% endhint %}

#### Delayed off-chain orders (Only Use This Trading Method)

Similar to `DelayedOrders`, Delayed off-chain orders also follow a familiar interface and operate asynchronously. From an integration standpoint, this is almost exactly the same as delayed orders (with the exception of differing function names and execution).

```solidity
interface IDelayedOffchainOrders {
    function submitCloseOffchainDelayedOrderWithTracking(uint desiredFillPrice, bytes32 trackingCode) external;

    function submitOffchainDelayedOrder(int sizeDelta, uint desiredFillPrice) external;

    function submitOffchainDelayedOrderWithTracking(
        int sizeDelta,
        uint desiredFillPrice,
        bytes32 trackingCode
    ) external;

    function executeOffchainDelayedOrder(address account, bytes[] calldata priceUpdateData) external payable;

    function cancelOffchainDelayedOrder(address account) external;
}
```

Off-chain orders require off-chain prices, price feed update data needs to be submitted upon execution. Off-chain prices are queried against [Pyth](https://pyth.network/price-feeds) and passed into `executeOffchainOrder` as a `bytes[]` array. On-chain we perform a variety of checks and if all pass, the order is executed and a position is opened.

{% hint style="info" %}
If the Pyth off-chain price deviates too far from on-chain prices, the execution will revert and a position will not be opened. This deviation can also be found in `PerpsV2MarketSettings`.
{% endhint %}

{% hint style="info" %}
Executing or canceling an off-chain order using a non-off-chain method will result in revert. The inverse is also true.
{% endhint %}

{% hint style="info" %}
Orders can go stale. We consider an order stale if it hasn't been executed for a long enough period. Stale orders can no longer be executed and can only be cancelled.
{% endhint %}

{% hint style="info" %}
A keeper fee is also charged on order submission however completely refunded if the executing account is the same as the submitter.
{% endhint %}

Building a keeper that is reliable, cost efficient, and up to date to execute orders across all markets in a timely manner is hard. We provide a keeper that you can run, fork, or use as documentation to build one of your own.

{% content-ref url="perps-keeper.md" %}
[perps-keeper.md](perps-keeper.md)
{% endcontent-ref %}

It's recommended to use off-chain delayed orders as the preferred method to open positions. It has the lowest fees and provides the fastest execution, giving traders the best UX.



{% hint style="danger" %}
We **STRONGLY** recommend you DO NOT use the below order types, and instead use **Delayed off-chain orders** documented above
{% endhint %}

<details>

<summary>Delayed orders (DO NOT USE THIS TRADING METHOD)</summary>

Delayed orders are async time based orders. Rather than opening a position with a single transaction, an order is created in one transaction and then executed in a separate transaction in the future, hence async and delayed. Positions opened through async delayed orders are charged significantly less than atomic orders. The interface can be found below:

```solidity
interface IDelayedOrders {
    function submitDelayedOrder(
        int sizeDelta,
        uint priceImpactDelta,
        uint desiredTimeDelta
    ) external;
    function submitDelayedOrderWithTracking(
        int sizeDelta,
        uint priceImpactDelta,
        uint desiredTimeDelta,
        bytes32 trackingCode
    ) external;
    function cancelDelayedOrder(address account) external;
    function executeDelayedOrder(address account) external;
}
```

Order submission requires similar arguments to that of `modifyPosition` with the addition of a `desiredTimeDelta` argument. `desiredTimeDelta` specifies the amount of time (in seconds) an async order must _wait_ before it is executable. If `desiredTimeDelta == 0` then we default to the minimum required time for convenience. The specified `desiredTimeDelta` must be above the required minimum otherwise a revert will occur. The minimum can be found in `PerpsV2MarketSettings`.

Once an order has been submitted successfully, it's stored and tagged with the current block's timestamp + `desiredTimeDelta` (denoted as `intentionTime`) for execution at a later time. After `block.timestamp >= order.intentionTime` then the order is executable by either the account that submitted the order or a keeper.

* Delayed orders can be executable before the intention time. This typically occurs during high price volatile periods. If a price update occurs
* Order fees are based on order type, size, and side (long/short). You can calculate the order fee by passing a `sizeDelta` and an `orderType` (atomic, delayed, delayed off-chain) to the `orderFees` view.



</details>

<details>

<summary>Atomic orders (DO NOT USE THIS TRADING METHOD)</summary>

As the name would suggest, atomic orders allow users to open, close, or modify a position _atomically_ (i.e. within a single transaction and without the need for keepers). Historically, this was the primary method for users to open a position in V1.

However, with the introduction of hybrid oracles, it's recommended to use delayed off-chain orders (see below). Prices update more frequently and fees are drastically lower. Below is the atomic orders interface with `modifyPosition` being the operation to open atomically.

```solidity
interface IAtomicOrders {
    function modifyPosition(int sizeDelta, uint priceImpactDelta) external;
    function modifyPositionWithTracking(
        int sizeDelta,
        uint priceImpactDelta,
        bytes32 trackingCode
    ) external;
    function closePosition(uint priceImpactDelta) external;
    function closePositionWithTracking(uint priceImpactDelta, bytes32 trackingCode) external;
}
```

Similar to `transferMargin`, we use the sign to indicate whether we want to modify long (positive) or short (negative). Atomic orders have a convenience method to close out the entire position without specifying a `sizeDelta`.

Please refer to the section below for more details on `priceImpactDelta` and `trackingCode`.

_Again, it is highly recommended to **NOT** use this method to open a position. Instead, use an off-chain orders or delayed orders instead. The fees will be substantially lower with other methods._

</details>

## How to Close a Position

To close a position is the same as modifying an existing position with equal but inverted size. For example to close a 100 ETH long, you simply short -100 ETH. Once a position has been opened, regardless of how (i.e. order type), it can be closed in any method, async or otherwise. The only difference is the execution and fees charged on exit.

```typescript
const market = new Contract(address, abi, signer);
const position = await market.positions(account);

// Atomically (inferior)
await market.modifyPosition(-position.size, desiredFillPrice);

// Convenience method for atomic orders (inferior)
await market.closePosition(desiredFillPrice);

// Delayed orders (inferior)
await market.submitDelayedOrder(-position.size, desiredFillPrice);

// Delayed off-chain orders (recommended)
await market.submitOffchainDelayedOrder(-position.size, desiredFillPrice);

// Convenience method for delayed off-chain orders (also recommended)
await market.submitCloseOffchainDelayedOrderWithTracking(desiredFillPrice);
```

## What is Price Impact / Fill Price?

Price impact refers to the price change in the market that is directly caused by your trade. In perps, price impact is relative to skew. Skew is the size delta between all open long and short positions, always optimising for a perfectly balanced skew. For example, market that is 80% long and 20% short is skewed 60% long.

If the position’s size increases/expands the market skew, they are charged a premium in the form of a higher fill price but if the skew is decreases/contracts, a discount is applied. This happens automatically when a trade is made and it affects both atomic and delayed orders.

If you're building a frontend to quote trader's entry/exit price, it's important to display this fill price. We provide a `fillPrice` view to help with this:

```solidity
function fillPrice(int sizeDelta) external view returns (uint price, bool invalid);
```

This topic is extensively covered in SIP-279, example simulation code, and intrinsically within the smart contract codebase.

{% embed url="https://sips.synthetix.io/sips/sip-279/" %}
SIP-279
{% endembed %}

{% embed url="https://github.com/davidvuong/perpsv2-funding" %}
Example Python simulation
{% endembed %}

{% embed url="https://github.com/Synthetixio/synthetix/blob/v2.80.3/contracts/PerpsV2MarketBase.sol#L587-L629" %}
Inline code documentation
{% endembed %}

### Price Impact Delta (units)

`priceImpactDelta` argument passed to open/close methods are percentages between 0 and 1. For clarity below are some examples:

| Percentage | Basis Points | Decimals | 1e18               |
| ---------- | ------------ | -------- | ------------------ |
| 10%        | 1000         | 0.1      | 100000000000000000 |
| 5%         | 500          | 0.05     | 50000000000000000  |
| 1%         | 100          | 0.01     | 10000000000000000  |
| 0.5%       | 50           | 0.005    | 5000000000000000   |
| 0.1%       | 10           | 0.001    | 1000000000000000   |

The specified `priceImpactDelta` provides trade price protection, particularly for delayed orders. Price may move and many orders/trades may be executed between submission and execution. Providing an acceptable delta prevents the trade from proceeding if the price moves too much.

`priceImpactDelta` is then used to derive the trade's upper/lower acceptable price limit and reverting if above or below (depending on long or short respectively).

```
priceImpactLimit (long)  = price * (1 + priceImpactDelta)
priceImpactLimit (short) = price * (1 - priceImpactDelta)
```

## What are Funding Rates?

Funding rates on Synthetix perps is one mechanism that encourages a balanced market. A balanced market is one such that the size of longs is equal to size of shorts. A market skew is present when longs do not balance shorts or vice versa. Whenever the market is imbalanced in the sense that there is more open interest on one side, SNX holders take on market risk.

Funding rates floats. It moves up and down proportional to the skew with a funding rate velocity that dictates how quickly it can move in either direction. In practice, the effect of this is that funding rates will continuously drift higher/lower in the presence of uncorrected position imbalances, creating a natural price discovery mechanism for funding rates while simultaneously smoothing out funding rate trajectories.

We provide two methods to retrieve both the current funding rate and current funding velocity.

```solidity
/*
 * The current funding rate as determined by the market skew; this is returned as a percentage per day.
 * If this is positive, shorts pay longs, if it is negative, longs pay shorts.
 */
function currentFundingRate() external view returns (int);

/*
 * Velocity is a measure of how quickly the funding rate increases or decreases. A positive velocity means
 * funding rate is increasing positively (long skew). A negative velocity means the skew is on shorts.
 */
function currentFundingVelocity() external view returns (int);
```

Funding rates are stored in 24hr periods. To calculate the hourly funding rate:

```jsx
const fundingRate = await market.currentFundingRate().div(24);
```

## Trading Fees

Traders are charged `makerFee` if the size of their order reduces the market skew and a `takerFee` if the order increases the skew. However, in certain situations, an order can decrease and increase the skew. In these scenarios, the proportion of size that decreases the skew should be charged a `makerFee` and the remaining, a `takerFee`. Below is a concrete example:

```
price    = 100
makerFee = 0.001
takerFee = 0.003

# Increasing the skew
skew       = 10
size       = 5
skewResult = 15
fee        = 5 * price * takerFee

# Decreasing the skew
skew        = 10
size        = -3
skewResult  = 7
fee         = 3 * price * makerFee

# Increasing and decreasing the skew
skew       = 10
size       = -15
skewResult = -5
fee        = 10 * price * makerFee + 5 * price * takerFee
```

We provide an `orderFee` view to assist with fee calculation.

```solidity
function orderFee(int sizeDelta) external view returns (uint fee, bool invalid);
```

{% hint style="info" %}
Note that `orderFee` does _not_ consider the keeper fee paid out for async order executions. A static fee is paid out from a trader's available margin on successful execution. However is fully refunded if the trader is the executor.
{% endhint %}

## Trade Simulations

In certain situations, it's often useful to see the result of a trade without making it. You can simulate a trade for a particular `sender` (i.e. trader) by invoking the `postTradeDetails` view.

```solidity
function postTradeDetails(
  	int sizeDelta,
  	uint tradePrice,
  	address sender
)
  external
  view
  returns (
    uint margin,
    int size,
    uint price,
    uint liqPrice,
    uint fee,
    IPerpsV2MarketBaseTypes.Status status
  );
```

{% hint style="info" %}
Note that if `tradePrice == 0` then we use the current oracle price.
{% endhint %}

Looking to migrate an existing integration? Take a look at our [migration guides](migration-guides/).

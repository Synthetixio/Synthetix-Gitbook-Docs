# Liquidations

## Specification

Below are all relevant functions and events that pertain to perps liquidations.

```solidity
// Emitted when a position is flagged for liquidation by flagger
event PositionFlagged(uint id, address account, address flagger);

// Returns true when an account can be flagged for liquidation
function canLiquidate(address account) external view returns (bool)

// Flags a position for liquidation
function flagPosition(address account) external;

// Liquidates a flagged position
function liquidatePosition(address account) external;

// Liquidates a flagged position by an endorsed keeper
function forceLiquidatePosition(address account) external;
```

## How Do Liquidations Work?

Once a position's remaining margin is exhausted, it must be closed in a timely fashion, so that its contribution to the market skew and to the overall debt pool is accounted for as rapidly as possible, necessary for accuracy in funding rate and minting computations.

Liquidations occur in two stages: (1) flagging and (2) triggering liquidation on flagged positions. Flagging, as the name would suggest, flags the account to be liquidated, associating the flagger via `flagPosition`. After, and only after, a separate invocation to `{force}LiquidatePosition` performs the liquidation. There are two types of liquidations: **Spontaneous Liquidation** and **Forced Liquidation**.

{% hint style="info" %}
Once a position has been flagged for liquidation, no further interaction can occur until the liquidation is finalised.
{% endhint %}

{% hint style="info" %}
A position can only be flagged for liquidation _once_. Every subsequent attempts to flag will be met with reverts.
{% endhint %}

### **Spontaneous Liquidation**

A spontaneous liquidation is one whereby any account can perform the liquidation invocation. If the position is flagged, premium paid upon liquidation is below `maxLiquidationDelta`, and _instantaneous premium/discount_ is below `maxPD` then a trigger to liquidate will be successful and relevant fees will be paid to the respective keepers.

{% hint style="info" %}
Vast majority of liquidated accounts are expected to be liquidated spontaneously.
{% endhint %}

### Forced Liquidation

A forced liquidation similar to a spontaneous liquidation except that it bypasses the validation of `maxLiquidationDelta` and `maxPD.` Additionally, only an endorsed account can successfully invoke `forceLiquidatePosition`, with a revert being thrown on non-endorsed accounts.

_Refer to_ [_PerpsV2MarketSettings_](useful-links.md) _for the values of `maxLiquidationDelta` and `maxPD`._

## Endorsed Accounts

Endorsed accounts are tracked and managed on-chain via the `FuturesMarketManager` contract:

```solidity
// Events emitted when addresses are added/removed from the endorsed list
event EndorsedAddressAdded(address endorsedAddress);
event EndorsedAddressRemoved(address endorsedAddress);

// Removes one or many endorsed addresses
function removeEndorsedAddresses(address[] calldata addresses) external;

// Adds one or many endorsed addresses
function addEndorsedAddresses(address[] calldata addresses) external;

// True if the specified account is endorsed, false otherwise
function isEndorsed(address account) external view returns (bool);

// Returns all endorsed addresses
function allEndorsedAddresses() external view returns (address[] memory);
```

## Flagger / Liquidation Rewards

Rewards in the form of sUSD are paid to accounts that flag positions for liquidation. Rewards are also issued to accounts that trigger the subsequent liquidation. Flaggers are awarded the bulk of sUSD rewards, receiving an amount capped by `maxKeeperFee` but a minimum of `minKeeperFee`. As of writing this, an amount between $2 sUSD and $1000 sUSD is rewarded to the flagger.

A static sUSD amount defined by `keeperLiquidationFee` is issued to the liquidator triggering keeper. Endorsed keepers _**do not**_ receive a fee for force liquidations.

{% hint style="info" %}
sUSD rewards are _not_ issued upon flagging (i.e. at the invocation to `flagPosition`) but rather, they are issued at liquidation (i.e. invocation of `liquidatePosition`).
{% endhint %}

_Refer to_ [_PerpsV2MarketSettings_](broken-reference) _for the values of `minKeeperFee`, `maxKeeperFee`, and `KeeperLiquidationFee`._

## &#x20;Further Reading

* SIP-2005 - [https://sips.synthetix.io/sips/sip-2005/](https://sips.synthetix.io/sips/sip-2005/)

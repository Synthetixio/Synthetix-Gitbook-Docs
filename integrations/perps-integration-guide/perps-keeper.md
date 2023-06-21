# Perps Keeper

> Keepers enables smart contracts to automate key functions and event-driven tasks in a highly reliable, decentralized, and cost-efficient manner.

Synthetix perps require keepers to automate 3 core area of functionality: **delayed order executions**, **delayed off-chain order executions**, and **liquidations**. Keepers are rewarded for performing these duties in the form of sUSD. To find the exact values, refer to on-chain market parameters in `PerpsV2MarketSettings`.

## Running a Keeper

In the spirit and ethos of decentralisation, we recommend members of the community and partners to execute your own keeper. Running your own keeper improves network stability, reliability, and thus gives users an overall better experience.

Running a keeper can be tricky without understanding the minute details. To alleviate this, we provide and maintain a `perps-keeper`, which you can run, fork, or use as inspiration for your own custom keeper.

{% embed url="https://github.com/Synthetixio/perps-keepers" %}
Official Synthetix perps keeper
{% endembed %}

{% hint style="info" %}
Keepers compete with each other to process orders. The template keeper shown here is functional but inefficient and so unlikely to win any orders in this state.&#x20;

Some notes on shortcomings of the template keeper:

* How it batch execute orders (uses a custom signer pool instead of multi-call)
* It's not particularly reliable in that it just points to a single RPC but probably desirable if you're running your own node
* It's not running a local Pyth price service and calls out to another machine
* It's not using a WS connection and polls for events with `eth_getLogs` on an interval
* It's bloated and spams RPCs too heavily
{% endhint %}

{% embed url="https://github.com/Kwenta/kwenta-python-sdk/blob/main/examples/keeper/order_keeper.py" %}
Unofficial Kwenta perps keeper
{% endembed %}

&#x20;_Refer to the README for documentation, structure, and contribution_.

{% hint style="info" %}
Synthetix maintains and runs `perps-keepers` for the primary purpose of being a backstop if/when community keepers aren't timely during times of high volatility and/or new markets.
{% endhint %}

## Rewards

Keepers are rewarded for executing orders and liquidations. `minKeeperFee` specifies the minimum amount (in sUSD) a keeper will receive for performing any of the above operations. This is also a static amount (although configurable via SCCP) keepers receive for executing orders.

As for liquidations, sUSD is also rewarded upon liquidation. The amount received is proportional to size, fractionalised via `liquidationFeeRatio`. Remaining amounts post liquidation is sent to the fee pool for stakers.

{% hint style="info" %}
Stale order cancellations also reward sUSD, determined using the same `minKeeperFee` parameter.
{% endhint %}

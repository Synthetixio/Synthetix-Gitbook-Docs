---
description: For developers building on Synthetix v3 - what will you build?
---

# Build on v3

{% hint style="info" %}
v3 is still being rolled out, but now is the time to start building
{% endhint %}

<figure><img src="../.gitbook/assets/Twitter_post_-_4.png" alt=""><figcaption></figcaption></figure>

As an introduction to Synthetix v3, what its capable of and deployment progress at time of posting, see the following blog post.

{% embed url="https://mirror.xyz/cavalier.eth/w0pXCYaek7Bz_EfMmfoo6tpKhOUK-xOTcY223xl1JZE" %}
An outline of v3, its components and possibilities
{% endembed %}

## Summary

Synthetix v3 is a suite of financial primitives that enables anyone to pool collateral, build derivative markets (of any kind), and define how rewards can be distributed to stakeholders. This design allows developers to build custom market implementations for a wide range of financial instruments, such as spot tokens, perpetual futures, options, insurance, and any else, while utilizing the highest degree of decentralized technology currently available.

_**Pools**: a collection of collateral that can be connected to one or more Markets, allowing its collateral to be delegated for use by the Market(s). The Market withdraws/deposits stablecoins from/into the Pool depending on its performance,_

_**Oracle Manager**: accepts a range of onchain and offchain price oracles, which can be used by any Markets. The Oracle Manager is designed to agnostically accept a range of oracles, which currently include Chainlink and Pyth._&#x20;

_**Markets**: interact with Pools, Oracle Manager, users and the wider defi ecosystem. Markets typically perform a function, like a game, insurance market or perpetual futures market. A profitable Market would over time deposit more stable coins into the pool than it withdraws._

_**Rewards Distributor**: can be used by Pool owners to bootstrap or incentivise liquidity using additional tokens or earnings, separate to the Market’s performance depositing stablecoins._

## Markets

Here is an example implementation of a Number Guessing Game, as a Market on v3.&#x20;

{% embed url="https://github.com/Synthetixio/lottery-market" %}
Example v3 Market
{% endembed %}

_Typically, a lottery implemented using a smart contract could not provide substantial prizes or consistent odds without first accumulating an adequate prize pool from numerous players. If it were to offer consistent odds or high payouts prematurely, the lottery would risk insolvency (i.e. be unable to pay out winners). Consequently, the initial players would be uncertain about the size of the potential prize and their odds of winning, so it would be hard to attract early players to address the first issue. This scenario exemplifies the "cold start liquidity" problem, which is relevant to all types of derivatives markets._

_A lottery game implemented with Synthetix can offer liquidity providers the ability to collect fees from ticket sales in exchange for providing collateral to be used in prize payouts if necessary. In this guide, the lottery will offer tickets for 1 USD, and have a consistent jackpot of 1,000 USD. These numbers could be configured differently, or even set dynamically as a function of other factors. Let your imagination run wild._

## Pools

New Pools are created via governance, via a proposal like this:

{% embed url="https://github.com/Synthetixio/SIPs/pull/1537" %}
Proposal to create a new v3 Pool, owned by the Spartan Council
{% endembed %}

## Use cases

* Want to create a novel derivatives market? You might consider create a v3 Market, then requesting one of the existing Pools to delegate your Market some collateral.
* Want to control your own liquidity? You could propose to create a new Pool, and offer additional token incentives to stakers with the Rewards Manager.&#x20;

## Docs

{% embed url="https://snx-v3-docs.vercel.app/" %}


# Synthetix v3

{% hint style="warning" %}
Synthetix v3 is currently under development and not fully released yet, but you can read more below and see the evolving [technical integration documentation here.](https://snx-v3-docs.vercel.app/)

Synthetix v2 is the currently live version of the protocol.
{% endhint %}

## **What is Synthetix V3** <a href="#what-is-synthetix-v3" id="what-is-synthetix-v3"></a>

Synthetix V3 is a complete overhaul of the protocol from scratch. It fulfils what Synthetix set out to do long ago: a permissionless derivatives liquidity platform to power the next generation of on-chain financial products. With v3, Synthetix becomes a layer of liquidity that any derivatives markets can be built on.

Synthetix V3 benefits from years of research and development toward becoming the most robust and composable derivative liquidity protocol. It establishes a new foundation to be the most generalized and modular approach to the next generation of on-chain financial products. This diagram provides a high-level overview of the Synthetix V3 architecture:

<figure><img src="https://blog.synthetix.io/content/images/2023/03/Synthetix_V3_System_Overview.png" alt=""><figcaption></figcaption></figure>

The long-term vision of Synthetix V3 is easiest to understand through the goals of Synthetix V3

### **Long-Term Vision for Synthetix V3** <a href="#long-term-vision-for-synthetix-v3" id="long-term-vision-for-synthetix-v3"></a>

Synthetix as a liquidity layer has two key value propositions:

* **To stakers:** a range of Pools/Vaults to deposit into, that are connected to a range of derivative markets - thus choosing the level and type of market exposure and expected rewards
* **To protocols:** a range of Pools/Vaults to collateralize new derivatives market, or the tools to create a Pool and attract collateral with rewards

V3 focuses on four key areas:

1. **The Liquidity Layer for DeFi Derivatives: Fueling the Next Generation of Permissionless Derivatives**
2. **Power to Stakers with Multi-Collateral Staking**
3. **A Composable, Developer-Friendly System**
4. **The Future is Cross-Chain**

#### The Liquidity Layer of Derivatives: Fueling the Next Generation of Permissionless Defi Protocols <a href="#the-liquidity-layer-of-derivatives-fueling-the-next-generation-of-permissionless-defi-protocols" id="the-liquidity-layer-of-derivatives-fueling-the-next-generation-of-permissionless-defi-protocols"></a>

V3 brings to life Synthetix's long-term vision of becoming a permissionless liquidity provisioning platform, giving builders tools to easily create novel financial derivatives.

Launching a derivatives protocol can be challenging, typically faced with the cold-start problem of needing to attract collateral. With Synthetix, developers can create new markets and seamlessly connect to existing collateral vaults. In this way, almost any derivative protocol could be built on top of Synthetix V3, instead of from the ground up.

The creation of Pools/Vaults/Markets will initially be managed by Synthetix governance, and transition towards fully permissionless deployments over time. One could even describe Synthetix as offering liquidity-as-a-service since new protocols seeking increased liquidity for on-chain derivatives can build on Synthetix easily and efficiently.

V3 will transform Synthetix into a multi-market ecosystem, encompassing perpetual futures, spot, options, insurance, exotics, and more, all backed by multiple debt pools. Synthetix welcomes builders to leverage its protocol and bootstrap their communities for success, which is exciting for both Synthetix and the Ethereum ecosystem.

#### Power to Stakers with Multi-Collateral Staking <a href="#power-to-stakers-with-multi-collateral-staking" id="power-to-stakers-with-multi-collateral-staking"></a>

V3 creates a generalized vault system agnostic to collateral types. Each Vault supports a single collateral asset, but Vaults are combined into Pools connected to one or more Markets. All external collateral will be onboarded into the protocol through Synthetix governance.

The new Pool and Vault system has three key benefits:

1. Better risk management: Pools are connected to specific Markets, so they have specific exposure
2. Better hedging: Pools are connected to specific Markets so that they can be hedged accurately
3. Bigger collateral range: Stakers can stake whichever assets the Pools choose to accept

Stakers have an increasing range of Pools to allocate their capital to. This gives stakers more control over their credit as the V3 system provides more options for both liquidity and hedging.

#### A Simpler, Cleaner Developer Experience <a href="#a-simpler-cleaner-developer-experience" id="a-simpler-cleaner-developer-experience"></a>

V3 is fundamentally about making the Synthetix system more efficient, optimizing and cleaning up old implementations, so they are simpler, faster, and provide a better user experience.

Developers no longer need to be Synthetix experts to understand how to build on Synthetix. Instead, rich developer tooling, sandboxes, and guides make building on V3 simpler than ever. The hardest part will be deciding what market to build!

#### The Future is Cross-Chain <a href="#the-future-is-cross-chain" id="the-future-is-cross-chain"></a>

Synthetix V3 will be able to deploy onto any EVM-compatible chain to support synthetic assets on any chain.

Some of V3's most exciting features are based on cross-chain functionality- like teleporting assets from one chain to another with no additional work for protocols.

### **The Path to Synthetix V3** <a href="#the-path-to-synthetix-v3" id="the-path-to-synthetix-v3"></a>

Synthetix V3 will be released in a phased rollout over the coming months. Features will become progressively available, and users will transition from the existing v2x system. The features discussed in the next section \[Synthetix V3 Feature Deep Dive] will not be available upon initial release. The v3 system is optimized for modularity, so the scope and order of features is rapidly evolving and dependent on Synthetix Governance. It’s still important to try to understand the various streams that are being worked on within Synthetix V3.

* **Initial Release** - [Completed! Synthetix V3 core contracts are live on mainnet](https://blog.synthetix.io/synthetix-v3-is-on-mainnet/), though this only begins the path to V3. It is a ‘headless’ release without many usable features though the foundation is set. The current functionality is to borrow the new stablecoin snxUSD against snx collateral, which will be used in future integrated markets.
* **Collateral Agnostic System** - V3 creates a generalized collateral vault system that is agnostic to collateral types. Synthetix Governance will determine which assets to support as collateral in addition to the current SNX (staking) and ETH (wrappers).
* **V3 Spot Market** - The first expected market on V3 is spot markets. These markets enable the creation and trading of spot synths created entirely on Synthetix V3. Wrappers and spot markets incentives will work in conjunction to enable delta neutral markets that can support any ERC-20 wrappable synthetic asset.

Order types: Atomic Orders, Asynchronous Orders, Wrapping & Unwrapping (Wrappers) Learn more about Spot Markets in V3 by visiting the spot [readme](https://github.com/Synthetixio/synthetix-v3/tree/main/markets/spot-market?ref=blog.synthetix.io).

* **Perps V3** - Build Synthetix Perps on the infrastructure of V3.

New Features: Native cross-margin, Expanded margin collateral types, reduced gas costs based on new infrastructure, agnostic oracle integration, and more. All are highly dependent on governance, though these are all in R\&D from CCs/community.

* **Legacy market live on V3** - The ‘legacy market’ encompasses all synthetic assets and liquidity within the V2X system. Moving this to Synthetix V3 requires the introduction of a ‘Legacy Market’ within Synthetix V3 that V3 stakers can collateralize. The usage of this market is an interim solution until all synthetic assets are fully transitioned to native V3 markets. Once the legacy market is live, stakers will be able to migrate to their position to Synthetix V3.
* **Cross Chain & Synth Teleporters** - As V3 is fully EVM-compatible, it can be deployed onto any EVM-compatible chain. Liquidity can be provisioned cross-chain and synthetic assets/markets aren’t siloed to one chain.
* **Permissionless Market / Asset Creation** - The creation of Pools/Vaults/Markets will start as governance approved, and transition to permissionless.

### **Synthetix V3 Feature Deep Dive** <a href="#synthetix-v3-feature-deep-dive" id="synthetix-v3-feature-deep-dive"></a>

* **Market Creation:** The V3 system is built around markets. Markets are a generic abstraction that allows products to be built on the protocol. Markets determine the pricing logic used for associated assets.

Market Examples: Spot markets, futures markets, options, loans, etc.

* **Asset Creation:** New synthetic assets can be deployed using market pricing logic and price feeds. In V2x, these assets required approval from governance, but they will soon rely only on necessary market logic and price-feed support.

Asset Examples: Spot BTC, Spot ETH, ETH Perps, BTC Perps, ETH Options, etc.

* **Cross-Chain Synthetix:** The V3 system is compatible with any EVM-compatible chain. It has been built to be interconnected across chains with cross-chain liquidity and fee sharing, synth teleporters, and many more important changes.

Synth teleporters are more efficient than AMM-based cross-chain bridging solutions because there is no slippage from lack of liquidity on the destination chain. Synth assets are simply burned on one chain and minted on another.

* **Multi-Collateral Staking:** V3 is collateral agnostic, allowing governance to support any collateral to back synthetic assets. This will increase snxUSD liquidity and the markets supported by Synthetix. Collateral options will have adjustable variables, such as collateral requirements and rewards, which can be adjusted by governance.
* **Synthetix Loans**: Users can now provide collateral to the system to generate snxUSD without being exposed to debt pool risk, as well as without incurring any interest or issuance fees.
* **Differentiated Liquidity (Debt) Pools**: Users can choose the pools they want to provide collateral to and then decide which markets and assets within those pools they want to support, instead of delegating collateral to the entire debt pool as in V2x. This gives stakers more control over their credit and allows them to support markets that may be considered too risky by governance due to the singular debt pool for all liquidity.

Example: Risk-averse stakers can delegate their credit to a pool that only backs ETH and BTC perp markets instead of long-tail perp markets.

* **Oracle Management for Markets:** Market creators can choose from multiple oracle solutions to set up custom aggregation, giving them more control over the oracles that power their markets. The oracle manager opens up new opportunities for supporting new markets and assets.

Example: Use the lowest price for spot Bitcoin based on Chainlink, Pyth, and Uniswap's time-weighted average price (TWAP).

* **Rewards Manager:** Pool creators can attach rewards distributors to vaults, incentivizing liquidity providers of specific collateral types. Rewards can come from market fees, token distributions, or anything else.

Here are some of the in-progress SIPs to learn more about the current state of Synthetix V3 and how it will evolve:

* [SIP-300: Synthetix V3](https://sips.synthetix.io/sips/sip-300/?ref=blog.synthetix.io)
* [SIP-301: Accounts (V3)](https://sips.synthetix.io/sips/sip-301/?ref=blog.synthetix.io)
* [SIP-302: Funds (V3)](https://sips.synthetix.io/sips/sip-302/?ref=blog.synthetix.io)
* [SIP-303: Markets (V3)](https://sips.synthetix.io/sips/sip-303/?ref=blog.synthetix.io)
* [SIP-304: Liquidations (V3)](https://sips.synthetix.io/sips/sip-304/?ref=blog.synthetix.io)
* [SIP-305: Staking Incentives (V3)](https://sips.synthetix.io/sips/sip-305/?ref=blog.synthetix.io)
* [SIP-306: Collateral Migration (V3)](https://sips.synthetix.io/sips/sip-306/?ref=blog.synthetix.io)
* [SIP-307: Proxy Router Architecture (V3)](https://sips.synthetix.io/sips/sip-307/?ref=blog.synthetix.io)
* [SIP-308: Market-provided Collateral (V3)](https://sips.synthetix.io/sips/sip-308/?ref=blog.synthetix.io)
* [SIP-309: Market-locked Collateral (V3)](https://sips.synthetix.io/sips/sip-309/?ref=blog.synthetix.io)
* [SIP-310: Feature Flags (V3)](https://sips.synthetix.io/sips/sip-310/?ref=blog.synthetix.io)

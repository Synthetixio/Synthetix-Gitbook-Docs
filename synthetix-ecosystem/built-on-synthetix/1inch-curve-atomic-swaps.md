# 1inch/Curve - Atomic Swaps

## **What are Atomic Swaps?**

Atomic Swaps are a new exchange function allowing users to atomically exchange assets without fee reclamation by pricing synths via a combination of Chainlink and DEX oracles (Uniswap V3). Using both chainlink and Uniswap V3 protects stakers from frontrunning and allow traders to access low slippage and low fees from Synthetix. This functionality will only be available on Ethereum's base layer (L1), because there is no fee reclamation on Optimistic Ethereum (oracle latency is much faster).

Atomic exchanges are the reason for most of Synthetix’s mainnet volume on Curve, 1inch, and many other aggregators and integrators. It is a powerful tool that leads to significant volume without frontrunnable risk because of the unique pricing model.

## Atomic Swaps and Direct Integrations

Read more about how Atomic Swaps [utilize direct integrations](https://blog.synthetix.io/the-suhail-release-direct-integrations/) to deliver lower fees to atomic swaps traders.

---
description: How to mint testnet tokens (SNX and sUSD) with goETH
---

# Getting Goerli & Optimistic Goerli Testnet Tokens

In order to mint testnet tokens, `exchangeEtherForSNX` and `exchangeEtherForSynth` can be used under the [depot](https://goerli.etherscan.io/address/0x9B79D6dFe4650d70f35dbb80f7d1EC0Cf7f823Fd) contract.

Note that this contract returns SNX and sUSD on goerli for deposited ETH. In order to relay these tokens into optimistim, the [official optimistic bridge](https://app.optimism.io/bridge/deposit) can be used. Alternatively the [bridgeToOptimism](https://goerli.etherscan.io/address/0x1427Bc44755d9Aa317535B1feE38922760Aa4e65) contract can be interacted with directly.

Under the bridge contract the `deposit` function can be used for bridging SNX while `intiateSynthTransfer` for bridging sUSD into optimism. Bridging sUSD requires using   `0x73555344` should provided as an argument under the currencyKey field as the currencyKey.

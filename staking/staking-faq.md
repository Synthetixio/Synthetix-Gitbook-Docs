# Staking FAQ

<details>

<summary>What if I don't have any sUSD in my wallet to burn?</summary>

If you have an sUSD debt, but you have no sUSD in your wallet, then you must have done one of the following:

* Transferred it to another wallet
* Transferred it to a centralized / decentralized exchanged and sold it
* Burned sUSD in the past to raise your C-Ratio
* Exchanged it into another Synth / opened a futures position / etc.

To unlock your SNX, you must acquire the amount of sUSD under Debt in the Synthetix Staking dapp. If you transferred it to another wallet or an exchange, you will need to transfer it back into the wallet that contains your locked SNX. And if you sold the sUSD, you must buy it back.

If you are unable to acquire enough sUSD, you can also self-liquidate under the new liquidation mechanism.

You can purchase sUSD easily from [Curve](https://curve.fi/) or [Uniswap](https://uniswap.exchange/).

Once you've paid back your sUSD debt, your SNX will be unlocked and able to be transferred. Note - Your escrowed SNX will not be unlocked until it is fully vested.

</details>

<details>

<summary>I claimed by SNX staking rewards but I don't see them in my wallet</summary>

When you "claim" in the Rewards tab on Staking dAPP you are assigned your % of SNX in an escrow record in the RewardEscrow Contract. Your rewards will not show in your wallet address but they are assigned to your wallet address to be vested in 12 months from their claim date.

You will now be able to mint from those escrowed SNX as they are also used as your collateral. So mint away if you can and compound your next weeks SNX rewards.

</details>

<details>

<summary>I can't transfer my SNX, what do I do?</summary>

If you try to send more SNX than is transferrable, the transaction will fail.\
\
In the Staking dapp, if you go to the [mint page](https://staking.synthetix.eth.limo/staking/mint) it will show you how much of your SNX is transferrable and how much is in escrow.

To unlock your locked (staked) SNX, you need to 'burn' the sUSD active debt you owe. Go to the [burn section](https://staking.synthetix.eth.limo/staking/burn) of the Synthetix dapp to unlock SNX.

</details>

<details>

<summary>Where can I buy SNX?</summary>

There are several centralized and decentralized exchanges where you can buy SNX. View the centralized markets on [CoinGecko](https://www.coingecko.com/en/coins/synthetix-network-token#markets)

</details>

<details>

<summary>Why does my sUSD debt (active debt) fluctuate over time?</summary>

When you stake SNX and mint sUSD, you create a 'debt,' which is how much sUSD you need to burn to unlock your SNX again. Your debt represents a proportion of all the debt in the system. Whenever someone makes a gain through Synths, they make it against all the debt in the system.

Therefore, if the system debt increases, your debt will proportionately increase as well. When you mint sUSD, the Synthetix smart contract will work out how much debt you represented in the network at the time you joined.\
​\
For example, if you minted $1000 sUSD and the total sUSD value of all Synths in circulation is currently $1 million, your debt ratio owed to the network is 0.1%. However, as the total sUSD value of Synths increase (such as when sBTC or sETH increase in value), your debt ratio owed to the network remains constant at 0.1%.

Imagine if total sUSD value of all Synths suddenly doubles due to price increases in Synths such as sBTC or sETH, and now gets to $2 million, you will need to repay $2000 sUSD in order to unlock all your SNX. Why does this happen? This is because every staker needs to share the debt in proportion to their initial ratio so that the monetary policy balances out.

There is no free money created out of thin air. Every sUSD gain generates a corresponding debt value.

</details>

<details>

<summary>How do I increase my Colletrization Ratio (C-Ratio)?</summary>

There are three ways to increase your C-Ratio:

1. Burn some sUSD to clear some of your debt.&#x20;
2. Stake additional SNX.
3. Wait for the price of SNX to increase.

</details>

<details>

<summary>How do I transfer SNX (and other synths) between Optimism and Mainnet?</summary>

Please use the [SNX bridge](https://staking.synthetix.eth.limo/bridge), powered by Socket, to transfer SNX and other synths between Optimism and Mainnet.

</details>

<details>

<summary>Why does the number of my staked SNX fluctuate?</summary>

If you've staked your SNX, you might have noticed that the number of staked SNX in your wallet can change. This is due to fluctuations in the SNX price and account active debt.

</details>

<details>

<summary>How can I delegate claiming rewards, minting, or burning to another wallet?</summary>

Go to the [delegate section of the Synthetix staking dapp](https://staking.synthetix.io/delegate) to delegate to another wallet.

</details>

<details>

<summary>Why am I blocked from claiming rewards?</summary>

You are blocked from claiming rewards because your Collateralisation Ratio is below the target c-ratio. To increase your Collateralisation Ratio, you'll need to burn enough sUSD to get your Collateralisation Ratio above the target c-ratio.

</details>

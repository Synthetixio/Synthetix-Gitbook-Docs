# Automating Staking, Claiming, and Burning

Synthetix, in partnership with Gelato, offers automation for various staking-related tasks, such as claiming rewards, minting max (to stake additional SNX), and burning (to unstake some SNX or raise your c-ratio). This automation is facilitated by the Synthetix Delegate function, introduced with [SIP-10](https://sips.synthetix.io/sips/sip-10/) in March 2020. Gelato bots, while unable to control your entire staking account, can claim rewards, mint, and burn on your behalf using this delegate function.

#### Automated Claiming

**How it Works**:

* The bot claims your rewards if your c-ratio exceeds the target at any point during the week.
* If you manually burn sUSD to raise your c-ratio above the target, the bot will also claim your rewards.
* If your c-ratio never exceeds the target, the bot will not claim your rewards.

**Setup Guide**:

* **Deposit Funds**: Add funds to your Gelato Account for transaction fees. A recommended amount is $20-25, considering Optimism transactions cost approximately $0.50.
* **Create a Task**: Go to Gelato and click "Create Task." Use `0xaAd3a6178d741DEA76F57901FeeDaC0f7Bb280E5` as the contract address.

<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

* **Select Function**: Choose "Claim" after clicking "Select a function."
* **Enter Your Address**: Input your address in the designated field.

<figure><img src="../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

* **Set Frequency**: Select "Whenever Possible" for constant eligibility checks.
* **Name Your Task**: Provide a name and complete the task setup.
* **Delegate Claiming Rights**: Delegate only claiming rights to the Gelato contract (0xaAd3a6178d741DEA76F57901FeeDaC0f7Bb280E5) at [https://staking.synthetix.io/delegate](https://staking.synthetix.io/delegate).

#### Automated Claiming with 'Burn to Claim'

**Functionality**:

* If your c-ratio is below the target but you have sufficient sUSD to burn, Gelato will burn sUSD first and then claim your SNX rewards.

**Setup Guide**:

* Follow the same steps as above, but choose the "Burn and Claim" function instead of "Claim."
* Delegate the ability to both burn and claim to the Gelato address.

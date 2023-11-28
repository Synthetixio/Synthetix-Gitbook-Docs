# Automating Staking, Claiming, Burning, and Minting

Synthetix, in partnership with Gelato, offers automation for various staking-related tasks, such as claiming rewards, minting max (to stake additional SNX), and burning (to unstake some SNX or raise your c-ratio). This automation is facilitated by the Synthetix Delegate function, introduced with [SIP-10](https://sips.synthetix.io/sips/sip-10/) in March 2020. Gelato bots, while unable to control your entire staking account, can claim rewards, mint, and burn on your behalf using this delegate function.

### Automated Claiming

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

### Automated Claiming with 'Burn to Claim'

**Functionality**:

* If your c-ratio is below the target but you have sufficient sUSD to burn, Gelato will burn sUSD first and then claim your SNX rewards.

**Setup Guide**:

* Follow the same steps as above, but choose the "Burn and Claim" function instead of "Claim."
* Delegate the ability to both burn and claim to the Gelato address.

### **Automated Minting (thanks to Gunboats)**

SNX community member Gunboats has developed a tool in collaboration with the Gelato Network, allowing users to automate SNX minting based on their preferred settings. This automation can significantly streamline the minting process for SNX stakers.

**Step 1: Set Up Task in Gelato Network**

1. **Visit and Connect**: Go to [Gelato Network](https://app.gelato.network/). Connect your wallet to Optimism or Ethereum depending on where you stake.
2. **Create a Task**:
   * Input SNX token address based on your network:
     * Ethereum Mainnet: `0xd0dA9cBeA9C3852C5d63A95F9ABCC4f6eA0F9032`
     * Optimism: `0x8700dAec35aF8Ff88c16BdF0418774CB3D7599B4`
   * Switch to Custom ABI
   * Copy and Paste the SNX Token Contract ABI from the Mainnet [Etherscan](https://etherscan.io/address/0xd0dA9cBeA9C3852C5d63A95F9ABCC4f6eA0F9032#code) link
   * Select function: **issuemaxsynthsonbehalf**
   * Click “Resolver” and input the MaxMint Contract address:
     * Ethereum Mainnet: `0x509c4C872d2a8A82aD2C9Cbd09869697c7C6729b`
     * Optimism: `0xaD2E8F76f5f7b4378fD49fE62b8C0960511cf734`
3. Select the **Checker** function & input your staking address into input field
4. Name your task
5. Before finalizing the creation of your task, note down the msg.sender for use in the next step.

**Step 2: Delegate Minting Permission**

* **Delegate in Synthetix**: Use the [Synthetix Staking Dapp](https://staking.synthetix.io/delegate) to delegate minting permission to the msg.sender address obtained from Gelato when creating your task.

**Step 3: Configure MaxMint Contract**

* **Access MaxMint on Etherscan**: Visit the MaxMint contract page on Etherscan.
  * Ethereum Mainnet: [0x213f1d3d8cac06d39436380fdaee93007b1bd108](https://etherscan.io/address/0x213f1d3d8cac06d39436380fdaee93007b1bd108)
  * Optimism: [0xaD2E8F76f5f7b4378fD49fE62b8C0960511cf734](https://optimistic.etherscan.io/address/0xaD2E8F76f5f7b4378fD49fE62b8C0960511cf734#writeContract)
* **Set Configuration**: Connect your wallet and Call the setConfig function. Choose between C-Ratio Mode or sUSD Mode for settings (see below)

#### **Configuring Modes**

**C-Ratio Mode (Method #1)**

1. **Target C-Ratio**: Decide your target C-Ratio, e.g., 505% (5.3 in decimal).
2. **Convert to Wei**: Use 1/ Automated Target C-Ratio, then input this number into [https://eth-converter.com/](https://eth-converter.com/) as ether, then copy the Wei value and add two 0’s on the end to make sure it’s 18 digits.
   * Example: Automated Target C-Ratio of 505%
     1. 1/505 = 0.001980198019802
     2. Inputted into [https://eth-converter.com/](https://eth-converter.com/) as ether and then copied as wei = 1980198019802000
     3. Add two additional zeros 1980198019802000 + 00 = 198019801980200000
3. **Input in Etherscan**:
   * Optimism: \[1, "198019801980200000", 0] - It must use this exact template for Optimistic Etherscan.
   * Ethereum Mainnet: Input each piece separately:
     1. 1
     2. 198019801980200000
     3. 0

**sUSD Mode (Method #2)**

1. **sUSD Threshold**: Choose the dollar threshold, e.g., $500.
2. **Convert to Wei**: Multiply the amount by 1e18. For $500, it’s 500000000000000000000.
3. **Input in Etherscan**:
   * Optimism: \[2, 0, "500000000000000000000"] - It must use this exact template for Optimistic Etherscan.
   * Ethereum Mainnet: Input each piece separately:
     1. 2
     2. 0
     3. 500000000000000000000

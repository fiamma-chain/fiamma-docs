---
hidden: true
---

# How to Deposit and Withdraw on Fiamma Bridge?

Prerequisite

To begin, you'll need wallets that support EVM-compatible and BTC addresses, along with the corresponding test tokens.

* Bitcoin Signet
  * Wallet: [Unisat](https://unisat.io/) (others coming soon)
  * Faucet: [https://signetfaucet.bublina.eu.org/](https://signetfaucet.bublina.eu.org/)
* Ethereum Holesky Testnet
  * Wallet: [Metamask](https://metamask.io/) and others
  * Faucet: [https://www.holeskyfaucet.io/](https://www.holeskyfaucet.io/)



## How to Deposit

> Transfer sBTC from Signet to Holesky Testnet.

1. Connect Bitcoin Wallet - Unisat

<figure><img src="../../../../.gitbook/assets/img_v3_02gs_9236ece3-7c26-4f86-a525-085d6ce21dhu.png" alt=""><figcaption></figcaption></figure>

Please note that we only support Native Segwit and Taproot address types in alpha-testnet.&#x20;

<figure><img src="../../../../.gitbook/assets/img_v3_02gs_af43b911-befc-4d65-bcef-4367cc16f4hu.png" alt=""><figcaption></figcaption></figure>

2. Enter amount within `0.00001 ~ 0.0001sBTC`(Due to current liquidity constraints in our operator, we have implemented a temporary limit on amounts. We anticipate increasing these limits.)

<figure><img src="../../../../.gitbook/assets/img_v3_02gs_bdeda497-b65b-427f-955a-84da7905eehu.png" alt=""><figcaption></figcaption></figure>

3. Please enter the recipient's address in the designated field, ensuring it is an ERC20-compatible address from the Holesky network.

> Or just connecting with the Metamask, which will autofill the address.

<figure><img src="../../../../.gitbook/assets/image (22).png" alt=""><figcaption></figcaption></figure>

4. Confirm and hit deposit

<figure><img src="../../../../.gitbook/assets/818d9f09-8f48-4cf7-9112-71d65dfea58a.jpeg" alt=""><figcaption></figcaption></figure>



5. Sign `PEG-IN` (Deposit) Transaction and pre-sign Take Transactions, which is prepared to pay back for Operator when they finish `PEG-OUT` (withdraw) operation.

<figure><img src="../../../../.gitbook/assets/img_v3_02gs_8008e31e-44c7-430e-bfec-630e3b6746hu.jpg" alt=""><figcaption></figcaption></figure>

6. It will then proceed with processing.
7. Check your deposit (Peg-in) status by clicking the deposit transaction. &#x20;

<figure><img src="../../../../.gitbook/assets/2afc9d55-b064-4863-a096-9563fbfe869b.jpeg" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/img_v3_02gs_e88f30f7-8988-42b2-9cea-6a93904b3bhu.jpg" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/img_v3_02gs_f4026fd5-460b-4083-94b5-d3a0cb4c69hu.jpg" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/img_v3_02gs_ecb1bb1a-eb2a-4663-aa6d-97ac672050hu.jpg" alt=""><figcaption></figcaption></figure>

8.  Check your bridged BTC (mamaBTC) on Sidechain wallet.

    1. Add mamaBTC **`0x5636bB012F5176d75755691B623236971126Fdac`**  on Metamask
    2. Check the amount.

    <figure><img src="../../../../.gitbook/assets/img_v3_02gs_88b6404c-995c-4c14-a501-41f843fa38hu.jpg" alt=""><figcaption></figcaption></figure>



## How to `PEG-OUT`

1. Connect EVM-compatible wallets (e.g., Metamask)

<figure><img src="../../../../.gitbook/assets/20241124-163845.jpeg" alt=""><figcaption></figcaption></figure>

2. Select `PEG-OUT` Amount (We will bring in external liquidity provider to achieve fully flexible amount in the future.)

<figure><img src="../../../../.gitbook/assets/d0e80137-af32-4f11-9dce-33d821ea2150.jpeg" alt=""><figcaption></figcaption></figure>

3. Fill out the recipient address on Bitcoin.

<figure><img src="../../../../.gitbook/assets/20241124-164526.jpeg" alt=""><figcaption></figcaption></figure>

4. Confirm and Withdraw
   1. Withdraw

<figure><img src="../../../../.gitbook/assets/img_v3_02gs_a86402b6-c4d6-46a0-8018-575646eb96hu (1).png" alt=""><figcaption></figcaption></figure>

b. Confirm Withdraw and Sign Burn Transaction

<figure><img src="../../../../.gitbook/assets/img_v3_02gs_b3a1aa0b-667c-4a3e-98d8-ed617bc840hu.jpg" alt=""><figcaption></figcaption></figure>

5. Processing.&#x20;
6. Check your PEG-OUT (withdraw) status in history.

> This process may take 10-20 minutes to be confirmed on the Signet.

<figure><img src="../../../../.gitbook/assets/img_v3_02gs_8e546016-21aa-4cc0-9347-192f40df1fhu.jpg" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/img_v3_02gs_098c5537-2c5b-4421-92bc-cd1a57000ehu.jpg" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (25).png" alt=""><figcaption></figcaption></figure>


























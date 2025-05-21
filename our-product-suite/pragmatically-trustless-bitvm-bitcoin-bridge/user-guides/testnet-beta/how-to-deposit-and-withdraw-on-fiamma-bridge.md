# How to Deposit and Withdraw on Fiamma Bridge?

**Prerequisite**

To begin, you'll need two wallets that support EVM-compatible and BTC addresses, along with the corresponding test tokens.

* Bitcoin Signet
  * Wallet: [Unisat](https://unisat.io/), [OKX](https://web3.okx.com/), [Bitget](https://web3.bitget.com/en), [Xverse](https://www.xverse.app/)
  * Faucet: [https://signetfaucet.bublina.eu.org/](https://signetfaucet.bublina.eu.org/)
* Ethereum Holesky Testnet
  * Wallet: [Metamask](https://metamask.io/) and others
  * Faucet: [https://www.holeskyfaucet.io/](https://www.holeskyfaucet.io/)



### How to Deposit

> Transfer sBTC from Signet to another chain (e.g., Ethereum Holesky).

1. Connect Bitcoin Wallet

<figure><img src="../../../../.gitbook/assets/image (41).png" alt=""><figcaption></figcaption></figure>

Please note that we only support Native Segwit and Taproot address types in beta-testnet.&#x20;

<figure><img src="../../../../.gitbook/assets/img_v3_02gs_af43b911-befc-4d65-bcef-4367cc16f4hu.png" alt=""><figcaption></figcaption></figure>

2. Connect EVM Wallet (Optional)

<figure><img src="../../../../.gitbook/assets/image (42).png" alt=""><figcaption></figcaption></figure>

3. Enter the recipient's address in the designated field.

> If you have connected to an EVM wallet, an autofill option will appear below the text field

<figure><img src="../../../../.gitbook/assets/截屏2025-05-21 22.07.49.png" alt=""><figcaption></figcaption></figure>

4. Enter deposit amount from `0.001` to `3 sBTC`&#x20;

<figure><img src="../../../../.gitbook/assets/image (45).png" alt=""><figcaption></figcaption></figure>

5. Check the Deposit Summary pop up. Once confirmed, hit deposit to submit this transaction.

<figure><img src="../../../../.gitbook/assets/截屏2025-05-21 22.32.43.png" alt=""><figcaption></figcaption></figure>

6. Sign Deposit Transaction in your BTC wallet. You will also sign pre-sign Take Transactions simultaneously, which will be used to pay back to Operator when they finish Withdraw operation.

<figure><img src="../../../../.gitbook/assets/image (35).png" alt=""><figcaption></figcaption></figure>

7. Your deposit has been submitted. You can then see the deposit progress in the new page.

<figure><img src="../../../../.gitbook/assets/截屏2025-05-21 22.40.01.png" alt=""><figcaption></figcaption></figure>

8. To see all transaction history, click on the account icon on the top right of the screen, and select bridge in the sub-menu.

<figure><img src="../../../../.gitbook/assets/image (36).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (37).png" alt=""><figcaption></figcaption></figure>

8. Once the deposit is complete, check your bridged BTC (FiaBTC) on destination chain wallet.
   1.  Import FiaBTC token for each destination chain. Enter the token contract address for each chain:

       1. Ethereum Holesky: `0xD32B4fB574a3cCEB3576350D8A0e9011507F79d2`
       2. &#x20;Monad Testnet: `0x859fb36f3Fe7e22b37dd99b501f891377DdC9c33`
       3. Plume Testnet: `0xd922BB00C0f7F555655e7c9e38D70E5636e6C615`

       &#x20;

       <figure><img src="../../../../.gitbook/assets/image (34).png" alt=""><figcaption></figcaption></figure>
   2. Check the amount in your wallet.

<div data-full-width="false"><figure><img src="../../../../.gitbook/assets/image (38).png" alt="" width="375"><figcaption></figcaption></figure></div>



## How to Withdraw

1. Connect EVM-compatible wallets (e.g., Metamask)

<figure><img src="../../../../.gitbook/assets/image (42).png" alt=""><figcaption></figcaption></figure>

2. Fill out the recipient address on Bitcoin.

> If you have connected to a BTC wallet, an autofill option will appear below the text field

<figure><img src="../../../../.gitbook/assets/image (33).png" alt="" width="375"><figcaption></figcaption></figure>

2. Enter Withdraw amount

* The bridge supports two modes: Express mode and Custom mode.
  * Express mode: Faster but with limited amount options. Pick the closest amount you entered to withdraw.
  * Custom mode: Withdraw any amount you entered.

<figure><img src="../../../../.gitbook/assets/image (32).png" alt="" width="375"><figcaption></figcaption></figure>

3. Check the Withdraw Summary pop up. Once confirmed, hit withdraw to submit this transaction.

<figure><img src="../../../../.gitbook/assets/截屏2025-05-21 23.20.40.png" alt=""><figcaption></figcaption></figure>

4. Sign Burn Transaction in your EVM wallet.

<figure><img src="../../../../.gitbook/assets/截屏2025-05-21 23.22.31.png" alt=""><figcaption></figcaption></figure>

5. You can also check the Withdraw status under bridge history.

> This process may take 10-20 minutes to be confirmed on the Signet.

<figure><img src="../../../../.gitbook/assets/截屏2025-05-21 23.25.12.png" alt=""><figcaption></figcaption></figure>

* Click on one of the transactions to see detailed progress.

<figure><img src="../../../../.gitbook/assets/截屏2025-05-21 23.26.06.png" alt=""><figcaption></figcaption></figure>

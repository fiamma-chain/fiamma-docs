# Wallet and Tokens
## Connect Keplr Wallet
**Note**: We are in the Testnet stage, so the API may undergo incompatible changes in the future. If you encounter any issues, please join our Discord to get in touch with the [Fiamma](https://discord.gg/jTXWxKmG) Team.

Fiamma Testnet has been integrated with the Keplr wallet! To better manage your Fiamma address, you can connect your [Keplr wallet](https://www.keplr.app/) by following these steps.

### Add Fiamma Testnet Chain
Visit [keplr app](https://chains.keplr.app), search for "Fiamma Testnet" and add it to your Keplr wallet.

Add "Fiamma Testnet" Chain to Keplr:

<figure><img src="../.gitbook/assets/fia-keplr.png" alt=""><figcaption></figcaption></figure>

### Create a Wallet with Fiamma Address
Open the Keplr wallet extension, click the user avatar in the top right corner, and select "Add Wallet" on the Select Wallet page.

Add Wallet in Keplr:

<figure><img src="../.gitbook/assets/select-wallet.png" alt=""><figcaption></figcaption></figure>

On the new page, choose "Create a new wallet". If you want to import an existing wallet from fiamma-node, please refer to [Manage Keys](./manage-keys.md).


Create a new wallet:

<figure><img src="../.gitbook/assets/create-new-wallet.png" alt=""><figcaption></figcaption></figure>

Then follow the steps to sign in and set a custom name for your wallet. In the third step, select the chain for your wallet. Search for "Fiamma Testnet" and check the box to confirm.


Select "Fiamma Testnet" Chain:
<figure><img src="../.gitbook/assets/select-fiamma.png" alt=""><figcaption></figcaption></figure>

You will now see your Fiamma address in the Keplr wallet. To get testnet FIA from our faucet, please refer to Get FIA.

### Get FIA
Get your testnet FIA for development and testing

**Note**: We are in the Alpha Testnet stage, so the API may undergo incompatible changes in the future. If you encounter any issues, please join our Discord to get in touch with the Fiamma Team.

In Fiamma DA Alpha Testnet, users can receive FIA tokens through two methods: the Discord channel and the web faucet. Each method has its own limits and conditions, and these two methods are not mutually exclusive.

- **Discord Faucet**: Each address/Discord ID can receive 0.05 FIA per day, but each address can only claim once every 24 hours.

- **Web Faucet**: Each address can receive 0.1 FIA daily, but each device can only claim once every 24 hours.

**Note**: Addresses with a balance exceeding 5 FIA will not be eligible to receive additional FIA from the faucet. The provided tokens should be sufficient to cover gas fees under normal circumstances, so please use them wisely. If you need more FIA, please contact the FIA team. 

#### Web Faucet
The web faucet is available at: [faucet FIA](https://testnet-faucet.fiammachain.io).

Users can claim 0.1 FIA per day, but each device is restricted to one claim every 24 hours.

#### Discord Faucet
Join Fiamma discord server by this invitation: [Fiamma](https://discord.gg/jTXWxKmG).

To request tokens from the Fiamma DA Alpha Testnet Faucet, use the following command in the `#[testnet-faucet]` channel on Fiamma’s Discord server:

`$request <FIAMMA-ADDRESS>`

Where `<FIAMMA-ADDRESS>` is a generated address starting with Fiamma.

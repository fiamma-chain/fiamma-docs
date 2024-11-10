---
description: >-
  The token symbol for the Fiamma testnet is $FIA, and the token's denom value
  is ufia .                            1FIA = 1_000_000 ufia
---

# Get $FIA

Get your testnet token FIA for development and testing

{% hint style="info" %}
**Note**: We are in the Alpha Testnet stage, so the API may undergo incompatible changes in the future. If you encounter any issues, please join our Discord to get in touch with the Fiamma Team.
{% endhint %}

In Fiamma DA Alpha Testnet, users can receive FIA tokens through two methods: the Discord channel and the web faucet. Each method has its own limits and conditions, and these two methods are not mutually exclusive.

* **Discord Faucet**: Each address/Discord ID can receive **1 FIA** per day, but each address can only claim once every 24 hours.
* **Web Faucet**: Each address can receive **0.5 FIA** daily, but each device can only claim once every 24 hours.

{% hint style="info" %}
**Note**: The tokens of the faucet will dynamically adjust based on supply and demand conditions. The provided tokens should be sufficient to cover gas fees under normal circumstances, so please use them wisely. If you need more FIA, please contact the [Fiamma team](https://app.gitbook.com/u/6g4AtPl7qkgj2hKuTiFRQ7DXCXD2).
{% endhint %}

## Web Faucet

The web faucet is available at: [https://testnet-faucet.fiammachain.io/](https://testnet-faucet.fiammachain.io/).

Users can claim 0.03 FIA per day, but each device is restricted to one claim every 24 hours.

## Discord Faucet

Join Fiamma discord server by this invitation: [Fiamma Discord](https://discord.com/invite/jTXWxKmG).

To request tokens from the Fiamma DA Alpha Testnet Faucet, use the following command in the `#[testnet-faucet]` channel on Fiamma’s Discord server:

```
$request <FIAMMA-ADDRESS>
```

Where `<FIAMMA-ADDRESS>` is a generated address starting with Fiamma.

Additionally, you can use the `$balance <FIAMMA-ADDRESS>` command to check the balance of a specified address and the `$transaction <TX HASH>` command to check the status of a specific transaction (faucet transactions only).

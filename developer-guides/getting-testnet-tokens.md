---
description: In this tutorial you will learn how to get fiamma testnet token ufia
---

# Getting Testnet Tokens

### Create a Keyring <a href="#id-1-create-a-keyring" id="id-1-create-a-keyring"></a>

One can create a keyring through the  `fiammad keys add` command.&#x20;

```
# Replace the --keyring-backend argument with a backend of your choice
fiammad --keyring-backend test keys add my-key
```

This will output an address and a memo. Record the memo as it is the only way to recover your key if it gets lost.

### Request Funds from the Fiamma Testnet Faucet <a href="#id-2-request-funds-from-the-babylon-testnet-faucet" id="id-2-request-funds-from-the-babylon-testnet-faucet"></a>

#### Web Faucet

The web faucet is available at: [faucet FIA](https://testnet-faucet.fiammachain.io).

Users can claim 0.1 FIA per day, but each device is restricted to one claim every 24 hours.

#### Discord Faucet

Join Fiamma discord server by this invitation: [Fiamma](https://discord.gg/jTXWxKmG).

To request tokens from the Fiamma DA Alpha Testnet Faucet, use the following command in the `#[testnet-faucet]` channel on Fiamma’s Discord server:

`$request <FIAMMA-ADDRESS>`

Where `<FIAMMA-ADDRESS>` is a generated address starting with Fiamma.


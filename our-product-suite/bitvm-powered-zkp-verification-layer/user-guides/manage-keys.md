---
description: >-
  In this tutorial, you will learn how to manage your account using the fiammad
  command line tool.
---

# Manage Keys

## Add Keys <a href="#list-keys" id="list-keys"></a>

{% hint style="info" %}
Note! Once your account is created, you must keep your mnemonic phrase safe. If you lose it, you will also lose your assets.
{% endhint %}

```bash
fiammad keys add <key-name> --keyring-backend=test
```

A fiamma address will be automatically generated such as:

```json

- address: fiammaXXX
  name: test-alice
  pubkey: '{"@type":"/cosmos.crypto.secp256k1.PubKey","key":"XXX"}'
  type: local

```

## Recover keys  <a href="#list-keys" id="list-keys"></a>

```
fiammad keys add <key-name> --keyring-backend=test --recover
```

After executing the above command, you will be prompted to enter a mnemonic in the bip39 format

After bip39 mnemonic inputed, a fiamma address will be automatically generated such as:

```json
- address: fiammaXXX
  name: test-alice
  pubkey: '{"@type":"/cosmos.crypto.secp256k1.PubKey","key":"XXX"}'
  type: local
```

## List Keys <a href="#list-keys" id="list-keys"></a>

You can use the command below to view the account you just created.

```bash
fiammad keys list --keyring-backend=test
```

A fiamma address named with test-alice will be automatically show such as:

```
- address: fiammaXXX
  name: test-alice
  pubkey: '{"@type":"/cosmos.crypto.secp256k1.PubKey","key":"XXX"}'
  type: local
```

## Export Keys

You can use the command below to show the account private key.

```bash
fiammad keys export <key-name> --keyring-backend=test --unarmored-hex --unsafe
```

## Store Keys in Keplr Wallet

Fiamma Testnet has been integrated with the Keplr wallet. Please refer to [Connect Keplr Wallet](wallet-and-tokens/#connect-keplr-wallet) for more details. To better manage your Fiamma address, you can import it into your Keplr wallet by following these steps.

Visit the Keplr Chains website at [https://chains.keplr.app](https://chains.keplr.app), search for "**Fiamma Testnet**" and add it to your Keplr wallet.

Open the Keplr wallet extension and click the user avatar in the top right corner. Select "**Add Wallet**," then choose either "**Import an existing wallet**" or "**Create a new wallet**." Opt for the "24 words recovery phrase" and enter your mnemonic phrase, or opt for the "private key" and enter your unarmored hex private key.

Use Recovery Phrase or Private Key to Import Keys into Keplr Wallet:

<figure><img src="../../../.gitbook/assets/image (5) (1).png" alt=""><figcaption><p>import-private-key</p></figcaption></figure>

Set a custom name for your wallet, select "**Fiamma Testnet**" Chain and confirm. Your Fiamma address will now appear in the Keplr wallet extension, ready for receive and send transactions. For more faucet details, please refer to [Get FIA](wallet-and-tokens/#get-fia).

\\

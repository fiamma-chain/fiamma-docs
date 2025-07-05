---
description: >-
  Before becoming a validator on the fiamma network, you should register your
  validator address with the committee program, so that your validator address
  is allowed to join the network
---

# Become a Bitvm Staker

{% hint style="info" %}
On the current testnet, users who need to register as Fiamma validators must be approved before they are allowed to create one. If you wish to become a Fiamma validator, please follow [Fiamma's relevant announcements](https://x.com/Fiamma\_Chain) or contact the [Fiamma team](https://app.gitbook.com/u/6g4AtPl7qkgj2hKuTiFRQ7DXCXD2).
{% endhint %}

## Prerequisites

This guide assumes you have some familiarity with Bitcoin wallets and general Bitcoin usage. For example, know what UTXO is, Bitcoin RPC service etc, for more information, please see [bitcoin developer reference](https://developer.bitcoin.org/reference/rpc/index.html).

Ensure you have Rust installed on your system. You can [**install Rust**](https://www.rust-lang.org/learn/get-started) from the official Rust website[.](https://www.rust-lang.org/learn/get-started)

## Step 1: Installation Fiamma Committee CLI

You can refer to this [installation](../fiamma-committee-cli.md#installation) step to install the Fiamma Committee CLI.

## Step 2: Register as a Staker

You can refer to [Registration Instructions](../fiamma-committee-cli.md#register-as-a-bitvm2-staker-validator)  to register as a bitvm2 staker.

### Expected Output

If everything is correct, you will receive a registration ID:

```bash
You have submitted your registration application.
The registration number is 6, please wait patiently.
```

wait the Bitcoin transaction is confirmed, we have successfully register validator\_key as BitVM staker.

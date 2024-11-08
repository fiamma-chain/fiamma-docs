---
description: >-
  In this tutorial you will learn how to stake fiamma token and become a fiamma
  validator
---

# Become a Validator

{% hint style="info" %}
On the current testnet, users who need to register as Fiamma validators must be approved before they are allowed to create one. If you wish to become a Fiamma validator, please follow [Fiamma's relevant announcements](https://x.com/Fiamma\_Chain) or contact the [Fiamma team](https://app.gitbook.com/u/6g4AtPl7qkgj2hKuTiFRQ7DXCXD2).
{% endhint %}

## Prerequisites[​](https://docs.babylonchain.io/docs/user-guides/btc-staking-testnet/become-validator#prerequisites) <a href="#prerequisites" id="prerequisites"></a>

Having a full [node setup ](set-up-a-node.md)and synced by following this guide

You need to [register your validator ](become-a-bitvm-staker.md)address as a bitvm staker, so that you can continue with the registration process.

## 1. Create a Keyring and Get Funds <a href="#id-1-create-a-keyring-and-get-funds" id="id-1-create-a-keyring-and-get-funds"></a>

The [Getting Testnet Tokens](getting-testnet-tokens.md) page contains detailed instructions on how to create a keyring and get funds for it through a faucet.

## 2. Get Validator Pub Key <a href="#id-1-create-a-keyring-and-get-funds" id="id-1-create-a-keyring-and-get-funds"></a>

You can get the validator **pubkey** for the current node using the following command. You'll need to write it down. It will be needed next when creating the validator json file

<pre class="language-bash"><code class="lang-bash"><strong>fiammad tendermint show-validator
</strong></code></pre>

## 3. Get Node Moniker <a href="#id-1-create-a-keyring-and-get-funds" id="id-1-create-a-keyring-and-get-funds"></a>

You can get the node moniker for the current node using the following command. You'll need to write it down. It will be needed next when creating the validator json file

```bash
fiammad config get config moniker
```

## 4. Create A Validator Config File <a href="#id-1-create-a-keyring-and-get-funds" id="id-1-create-a-keyring-and-get-funds"></a>

You can modify the information of your validator as you wish, the following is just an example

You can find the **pubkey** by [Get Validator Key](become-a-validator.md#id-1-create-a-keyring-and-get-funds-1).

You can find the **moniker** by [Get Node Moniker](become-a-validator.md#id-1-create-a-keyring-and-get-funds-2)

```bash
cat << EOF > ~/.fiamma/config/validator.json
{
	"pubkey": {"@type":"/cosmos.crypto.ed25519.PubKey","key":"QiZohv1ATkoaiBvH3aKNryXIw5026xHZAWuqOuR0rWQ="},
	"amount": "1000000ufia",
	"moniker": "test-node",
	"commission-rate": "0.1",
	"commission-max-rate": "0.2",
	"commission-max-change-rate": "0.01",
	"min-self-delegation": "1"
}
EOF
```

## 5. Staking And Become A Validator <a href="#id-1-create-a-keyring-and-get-funds" id="id-1-create-a-keyring-and-get-funds"></a>

Now you can create a pledge transaction to complete the creation of the validator

```bash
fiammad tx staking create-validator ~/.fiamma/config/validator.json --from $KEYNAME --keyring-backend test --chain-id fiamma-testnet-1 --node "https://testnet-rpc.fiammachain.io/" --fees 2000ufia
```

## 6. Show Your Validator Addr <a href="#id-5-verify-your-validator" id="id-5-verify-your-validator"></a>

You can get your validator address with the following command

<pre class="language-bash"><code class="lang-bash"><strong>fiammad keys show $KEYNAME --keyring-backend test -a --bech val
</strong></code></pre>

where `$KEYNAME` is the name of the key that you used for the self-delegation (e.g. `my-key` on our example).&#x20;

## 7. Query Your Validator staking <a href="#id-5-verify-your-validator" id="id-5-verify-your-validator"></a>

Use the above command to get the validator address, then you can check if your validator is staking successfully

```bash
fiammad query staking validator $ADDR
```

If all goes well, you should see a response indicating the parameters that you specified on the create-validator transaction.

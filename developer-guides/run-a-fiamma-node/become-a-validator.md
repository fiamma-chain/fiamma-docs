---
description: >-
  In this tutorial you will learn how to stake fiamma token and become a fiamma
  validator
---

# Become a Validator

## Prerequisites[​](https://docs.babylonchain.io/docs/user-guides/btc-staking-testnet/become-validator#prerequisites) <a href="#prerequisites" id="prerequisites"></a>

Having a full [node setup ](set-up-a-node.md)and synced by following this guide

## 1. Create a Keyring and Get Funds <a href="#id-1-create-a-keyring-and-get-funds" id="id-1-create-a-keyring-and-get-funds"></a>

The [Getting Testnet Tokens](getting-testnet-tokens.md) page contains detailed instructions on how to create a keyring and get funds for it through a faucet.

## 2. Get Validator Key <a href="#id-1-create-a-keyring-and-get-funds" id="id-1-create-a-keyring-and-get-funds"></a>

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

## 6. Verify your Validator <a href="#id-5-verify-your-validator" id="id-5-verify-your-validator"></a>

To verify that you have become a validator, first find your validator address:

```bash
fiammad keys show $KEYNAME --keyring-backend test -a --bech val
```

where `$KEYNAME` is the name of the key that you used for the self-delegation (e.g. `my-key` on our example). This will return an address which you can use as the `$ADDR` variable to perform the following query:

```bash
fiammad query staking validator $ADDR
```

If all goes well, you should see a response indicating the parameters that you specified on the create-validator transaction.

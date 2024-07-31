---
description: >-
  Before becoming a validator on the fiamma network, you should register your
  validator address with the committee program, so that your validator address
  is allowed to join the network
---

# Become a Bitvm Staker

## Prerequisites

This guide assumes you have some familiarity with Bitcoin wallets and general Bitcoin usage. For example, know what UTXO is, Bitcoin RPC service etc, for more information, please see [bitcoin developer reference](https://developer.bitcoin.org/reference/rpc/index.html).

Ensure you have Rust installed on your system. You can [**install Rust**](https://www.rust-lang.org/learn/get-started) from the official Rust website[.](https://www.rust-lang.org/learn/get-started)

## Step 1: Clone the Repository

Next, clone the Fiamma committee repository:

```bash
git clone https://github.com/fiamma-chain/fiamma-committee.git
```

## Step 2: Compile the `fcli` Tool

Navigate into the cloned repository and compile the `fcli` tool:

```bash
cd fiamma-committee
cargo build --release
```

This will generate the `fcli` binary in the `target/release` directory.

## (optional) Step 3: Obtain UTXO Information

Before proceeding with the registration, you need to obtain a usable UTXO from your Bitcoin wallet. We use bitcoin-cli as example (_This could be different in other Bitcoin wallet_):

1.  **List Unspent Transactions**:

    ```bash
    bitcoin-cli listunspent
    ```

    This will list all unspent transactions. Look for a UTXO that you want to use and note the `txid` and `vout`. Make sure the UTXO has enough amount balance for stake.
2.  **Dump the Private Key**:

    ```bash
    bitcoin-cli dumpprivkey <your-bitcoin-address>
    ```

    Replace `<your-bitcoin-address>` with the address corresponding to the UTXO you selected. This command will output the private key associated with that address.

## Step 4: Register as a Staker

Use the `fcli` tool to register as a staker with the obtained UTXO information. Below is an example command:

```bash
fcli tx -n <network> register -v <validator_key> -t <txid> -o <vout> -s <private-key> -u <rpc-user> -p <rpc-password>
```

Replace `network` `<validator_key>`, `<txid>`, `<vout>`, `<private-key>`, `<rpc-user>`, and `<rpc-password>` with the appropriate values.

### Explanation of Command Parameters

* `-n`: Specifies the committee service network and Bitcoin RPC service. It can be `local` for local testing or `dev` for the testnet, or `main` for the mainnet.
* `register`: The subcommand used to register.
* `-v`: Specifies the Fiamma `validator_key`. Ensure the format is correct. Refer to [Show your  Validator Addr ](become-a-validator.md#id-5-verify-your-validator)section on obtaining the `validator_key`. The validator key should have a prefix of `fiammavaloper`.
* `-t`: Specifies the transaction ID of a UTXO in Bitcoin we did in step 3. This transaction must be associated with the private key specified by `-s`.
* `-o`: Specifies which output of the UTXO to use as we did in step 3, e.g., `0`.
* `-s`: Specifies the private key of Bitcoin account.
* `-u`: Specifies the Bitcoin RPC user.
* `-p`: Specifies the Bitcoin RPC password.

### Expected Output

If everything is correct, you will receive a registration ID:

```bash
You have submitted your registration application.
The registration number is 6, please wait patiently.
```

Now the Bitcoin transaction is staked, we have successfully register validator\_key as BitVM staker.

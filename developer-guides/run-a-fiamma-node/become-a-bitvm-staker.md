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

## &#x20;Step 1: Installation Fiamma Committee CLI

Fiamma Committee CLI is a BTC Staking Command Line Tool for BITVM2 Challenges on the Fiamma Chain.

### From GitHub Releases

1. Visit the [GitHub Releases page](https://github.com/fiamma-chain/fiamma-committee-cli/releases).
2. Download the binary file for your operating system:
   * Linux x86-64: `fcli-linux-x86-64`
   * macOS Intel: `fcli-mac-intel`
   * macOS Apple Silicon (M1/M2): `fcli-mac-arm`
   * Windows: `fcli-windows.exe`
3. Rename the downloaded file:
   * On Linux and macOS, rename to `fcli`
   * On Windows, rename to `fcli.exe`
4. Move the renamed file to a directory in your PATH.

For example, on Linux or macOS:

```bash
mv fcli-linux-x86-64 fcli # or fcli-mac-intel or fcli-mac-arm   
chmod +x fcli
sudo mv fcli /usr/local/bin/
```

On Windows, move `fcli.exe` to a directory in your PATH, such as `C:\Windows\System32\`.

### Building from Source

To build the CLI from source, ensure you have Rust and Cargo installed. Then follow these steps:

1. Clone the repository:

```
git clone https://github.com/fiamma-chain/fiamma-committee-cli.git
cd fiamma-committee-cli
```

2. Build the project:

```
cargo build --release
```

3. After building, you can find the binary in the `target/release` directory.

## Step 2: Obtain btc UTXO Information (optional)

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

## Step 3: Register as a Staker

Use the `fcli` tool to register as a staker with the obtained UTXO information. The registration process requires the use of the following 2 commands to complete.

```bash
fcli register --network testnet start --validator-key <VALIDATOR_KEY> --txid <TXID> --vout <VOUT> --private-key <PRIVATE_KEY>
```

**After the above command has finished executing, wait 5-10 minutes for the corresponding signed transactions to be generated, and then execute the following command.**

```bash
fcli register --network testnet finish --validator-key <VALIDATOR_KEY> --private-key <PRIVATE_KEY>
```

Replace `network` `<validator_key>`, `<txid>`, `<vout>`, `<private-key>`, `<rpc-user>`, and `<rpc-password>` with the appropriate values.

### Explanation of Command Parameters

* `--network`:Specifies the committee service network and Bitcoin RPC service. It can be `local` for local testing or `dev` for the testnet, or `main` for the mainnet.
* `register`: The subcommand used to register.
* `--validator_key`: Specifies the Fiamma `validator_key`. Ensure the format is correct. Refer to [Show your  Validator Addr ](become-a-validator.md#id-5-verify-your-validator)section on obtaining the `validator_key`. The validator key should have a prefix of `fiammavaloper`.
* `--txid`: Specifies the transaction ID of a UTXO in Bitcoin we did in step 3. This transaction must be associated with the private key specified by `-s`.
* `--vout`: Specifies which output of the UTXO to use as we did in step 3, e.g., `0`.
* `--private-key`: Specifies the private key of Bitcoin account.

### Expected Output

If everything is correct, you will receive a registration ID:

```bash
You have submitted your registration application.
The registration number is 6, please wait patiently.
```

Now the Bitcoin transaction is staked, we have successfully register validator\_key as BitVM staker.

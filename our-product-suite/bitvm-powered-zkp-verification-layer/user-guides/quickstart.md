---
description: >-
  This guide will help you get started with Fiamma Network for ZKP verification.
  We'll cover the complete workflow from installation to sending verification
  requests.
---

# QuickStart

## 1. Install Fiamma

You can refer to the [Installation](installation.md) section to install the fiammad binary program

## 2. Generate Fiamma Address

You can refer to the [Add Keys](manage-keys.md#list-keys) section to  generate a fiamma address&#x20;

## 3. Get Testnet Token

You can refer to the [Get $FIA](wallet-and-tokens/get-fia.md) section to  get some testnet token

## 4. Submit Proof for Verification

Before you can use fiammad cli to submit proof , you need to prepare the proof for testing, and a simple way to do this is to use the [fiamma git repository](https://github.com/fiamma-chain/fiamma/tree/main/prover\_examples) provides some test proof files.

If you have cloned the fiamma repository as instructed earlier, you can navigate to the root directory of the fiamma repository and then use the script and your previously created account to send transactions quickly.

You can also manually construct a transaction to send based on the contents of the submit\_proof.sh script, which works either way

```bash
cd fiamma/script/cli
./submit_proof.sh alice 
```

## 5. Check Verification Results

After you submit the transaction in the manner described in step 4, you can use the scripts in scirpt/cli to query and verify the results.

```bash
./query_verify_result.sh
```

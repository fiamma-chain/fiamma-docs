---
description: >-
  In this tutorial, you will learn how to use the fiammad command line tool to
  send requests related to zkpverify.
---

# CLI Tutorial
## 1. Send your proof to Fiamma network
### Groth16 proof
The Groth16 proof need the proof file, public input file and verifying key file. You may set gas and fees.

The current Fiamma network chain-id is `fiamma-testnet-1`, the proof system is `"GROTH16_BN254"` and the node is [https://testnet-rpc.fiammachain.io](https://testnet-rpc.fiammachain.io).

```
fiammad tx zkpverify submit-proof \
  --from <account_name> --chain-id <chain_id>  \
  --gas <gas> --fees <fees> \
  --node <node> \
  --keyring-backend test \
  <proof_system> \
  <proof_file> \
  <public_inpt_file> \
  <verifying_key_file>
```

**Example**
If you at the fiamma root direction, you can use the files at the direction of `prover_examples`.

Note that you must regenerate different proof files before each submition to ensure uniqueness of the proof id.

regenerate proof files:
```
// Assuming you are currently in the root directory at fiamma
cd prover_examples/gnark_groth16
make generate-proof
cd -
```

submit proof:
```
fiammad tx zkpverify submit-proof \
  --from alice --chain-id fiamma-testnet-1  \
  --gas 20000000 --fees 2000ufia \
  --node https://testnet-rpc.fiammachain.io \
  --keyring-backend test \
  "GROTH16_BN254" \
  ./prover_examples/gnark_groth16/example/proof \
  ./prover_examples/gnark_groth16/example/public_input \
  ./prover_examples/gnark_groth16/example/vk
```
### Plonk proof
The fiammd command for submit plonk proof is essentially similar to the one above for submit groth16 proof. The differences are proof system with `"PlonkBn254"` or `"PlonkBls12_381"` and the proof files at `gnark_plonk` direction.

**Example**
First regenerate different proof files:
```
cd prover_examples/gnark_plonk
make generate-proof
cd -
```

Then send Plonk proof:

Proof system use `"PlonkBn254"`.
```
fiammad tx zkpverify submit-proof \
  --from alice --chain-id fiamma-testnet-1  \
  --gas 20000000 --fees 2000ufia \
  --node https://testnet-rpc.fiammachain.io \
  --keyring-backend test \
  "PlonkBn254" \
  ./prover_examples/gnark_plonk/example/proof \
  ./prover_examples/gnark_plonk/example/public_input \
  ./prover_examples/gnark_plonk/example/vk
```
Or proof system use `"PlonkBls12_381"`.
```
fiammad tx zkpverify submit-proof \
  --from alice --chain-id fiamma-testnet-1  \
  --gas 20000000 --fees 2000ufia \
  --node https://testnet-rpc.fiammachain.io \
  --keyring-backend test \
  "PlonkBls12_381" \
  ./prover_examples/gnark_plonk/example/proof \
  ./prover_examples/gnark_plonk/example/public_input \
  ./prover_examples/gnark_plonk/example/vk
```

### BitVM proof
The fiammd command for submit BitVM proof is essentially similar to the one above for submit groth16 proof. The differences are  proof system with `"GROTH16_BN254_BITVM"` and the proof files at bitvm direction.

**Example**
Proof system use "GROTH16_BN254_BITVM".

Send BitVM proof:

```
fiammad tx zkpverify submit-proof \
  --from alice --chain-id fiamma-testnet-1  \
  --gas 20000000 --fees 2000ufia \
  --node https://testnet-rpc.fiammachain.io \
  --keyring-backend test \
  "GROTH16_BN254_BITVM" \
  ./prover_examples/bitvm/proof.bitvm \
  ./prover_examples/bitvm/public_input.bitvm \
  ./prover_examples/bitvm/vk.bitvm
```
## 2. Submit community verification to Fiamma network
The community verification need an proof id and verification result.

The proof id can be calculated from `sha256sum` of proof inputs using shell. It Concatenate the proof system, proof, public input,and vk.
```
# : ${PROOF_SYSTEM:="GROTH16_BN254"}
# NEW_PROOF_SYSTEM=$(echo -n $PROOF_SYSTEM | xxd -p)
# NEW_PROOF=$(cat $PROOF_FILE)
# NEW_PUBLIC_INPUT=$(cat $PUBLIC_INPUT_FILE)
# NEW_VK=$(cat $VK_FILE)
# allDataHex="${NEW_PROOF_SYSTEM}${NEW_PROOF}${NEW_PUBLIC_INPUT}${NEW_VK}"
# proof_id=$(echo -n "$allDataHex" | xxd -r -p | sha256sum | awk '{print $1}')
```

The optional proof systems include: `"PlonkBn254"`, `"PlonkBls12_381"`, `"GROTH16_BN254"`, `"GROTH16_BN254_BITVM"` and `"SP1"`. These proof input files are located in the file directories of the respective proving systems.

submit community verification:
```
fiammad tx zkpverify submit-community-verification \
  --from <account_name> --chain-id <chain_id>  \
  --gas <gas> --fees <fees> \
  --node <node> \
  --keyring-backend test \
  <proof_id> \
  <result>
```
**Example**
You may use the above shell to calculate a proof id, and use fiammad command to sumbit community verification with a verification result.
```
fiammad tx zkpverify submit-community-verification \
  --from alice --chain-id fiamma-testnet-1  \
  --gas 20000000 --fees 2000ufia \
  --node https://testnet-rpc.fiammachain.io \
  --keyring-backend test \
  8c467c816348fa2c44686624b558b71fb139cc30b6b2642298d6696f91adc189 \
  true
```
In addition, we provide shell scripts to make it easier to send these commands. The three parameters accepted by the script are account, proof id and result with bool value.
```
// Assuming you are currently in the root directory at fiamma
./scripts/cli/submit_community_verification_groth16_bn254.sh alice 8c467c816348fa2c44686624b558b71fb139cc30b6b2642298d6696f91adc189 true
```
## 3. Get proof data by proof id from Fiamma network
You can query proof data stored in the fiamma network by proof id.
```
fiammad query zkpverify get-proof-data \
  --chain-id <chain_id>  \
  --node <node> \
  --keyring-backend test \
  <proof_id>
```
**Example**
```
fiammad query zkpverify get-proof-data \
  --chain-id fiamma-testnet-1  \
  --node https://testnet-rpc.fiammachain.io \
  --keyring-backend test \
  8c467c816348fa2c44686624b558b71fb139cc30b6b2642298d6696f91adc189
```
## 4. Get bitvm witness by proof id from Fiamma network
You can query bitVM witness stored in the fiamma network by proof id.

```
fiammad query zkpverify get-bitvm-witness \
  --chain-id <chain_id>  \
  --node <node> \
  --keyring-backend test \
  <proof_id>
```

**Example**
```
fiammad query zkpverify get-bitvm-witness \
  --chain-id fiamma-testnet-1  \
  --node https://testnet-rpc.fiammachain.io \
  --keyring-backend test \
  4792ef5c0e3fafbae94dcbb068dc4c5bf8718584c2266895547c75653bb60c30
```
## 5. Get verify result from Fiamma network
You can query proof verify status stored in the fiamma network by proof id.
```
fiammad query zkpverify get-verify-result \
  --chain-id <chain_id>  \
  --node <node> \
  --keyring-backend test \
  <proof_id>
```

**Example**
```
fiammad query zkpverify get-verify-result \
  --chain-id fiamma-testnet-1  \
  --node https://testnet-rpc.fiammachain.io \
  --keyring-backend test \
  8c467c816348fa2c44686624b558b71fb139cc30b6b2642298d6696f91adc189
```
## 6. Get pending proofs from Fiamma network
You can queries a list of pending proof verification items in teh fiamma network.
```
fiammad query zkpverify pending-proof \
  --chain-id <chain_id>  \
  --node <node> \
  --keyring-backend test
```

**Example**
```
fiammad query zkpverify pending-proof \
  --chain-id fiamma-testnet-1  \
  --node https://testnet-rpc.fiammachain.io \
  --keyring-backend test
```
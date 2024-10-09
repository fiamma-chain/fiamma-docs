---
description: >-
  To make it easier to send zkpverify requests to the fiamma network, fiamma
  supports multi-language sdk, which can be easily used by developers.
---

# Fiamma ZKPVerify SDK

## Fiamma-sdk-rs

The [fiamma-sdk-rs](https://github.com/fiamma-chain/fiamma-sdk-rs.git) is the Rust SDK for the Fiamma chain, providing a range of APIs for interacting with the Fiamma blockchain. This SDK is primarily designed to simplify the process of blockchain development in Rust, covering fundamental on-chain operations and related functionalities.

### Main Features

#### **For eco-project parties**

* [Submit a proof to the blockchain.](fiamma-zkpverify-sdk.md#id-1.-submit\_proof)
* [Query transaction status and results.](fiamma-zkpverify-sdk.md#id-2.-get\_tx)
* Query a proof verify result and status.

#### **Other features**

* Create and remove validators on the Fiamma blockchain.
* Query the challenge data related to a specific BitVM proof or transaction
* Query the basic account functionality.
* etc...

### API Methods List

#### 1. submit\_proof

**Description**: Submits a proof to the Fiamma blockchain.

{% hint style="info" %}
When a project submits a proof to the Fiamma network, the Fiamma network verifies the proof's correctness and provides immediate verification results. This stage is known as "soft finality." If the project requires "hard finality" confirmation of the status, it must wait for a period of time, the duration of which depends on the number of validation nodes operated by community users within the network.
{% endhint %}

**Parameters**:

* **creator**: The Account identifiers.
* **proof\_system**: The name of the proof system used.
* **proof**: The serialized proof data in bytes.
* **public\_input**: The public input associated with the proof, serialized as bytes.
* **vk**: The verification key for the proof, also serialized as bytes.
* **namespace**: The namespace under which the proof is being submitted.

```rust
pub struct MsgSubmitProof {
    pub creator: AccountId,
    pub proof_system: String,
    pub proof: Vec<u8>,
    pub public_input: Vec<u8>,
    pub vk: Vec<u8>,
    pub namespace: String,
}
```

**Example Usage**:

```rust
const SENDER_PRIVATE_KEY: &str =
"59514b4e9c63b91cc9d3b6b882f1c5ee7449890c7c1116782670c71c96957897";
const NODE: &str = "http://54.65.137.66:9090";
const BITVM_PROOF_SYSTEM: &str = "GROTH16_BN254_BITVM";
const NAMESPACE: &str = "ZULU";
let wallet = Wallet::new(SENDER_PRIVATE_KEY);
let gas_limit = 80_000_000_u64;
let fee = 2000_u128;
let tx_client = TxClient::new(SENDER_PRIVATE_KEY, NODE, fee, gas_limit);
let submit_proof_msg = msg_submit_proof(wallet.account_id.clone());
let resp = tx_client.submit_proof(submit_proof_msg).await.unwrap();

fn msg_submit_proof(account_id: AccountId) -> MsgSubmitProof {
    // Note that proof_artifacts construct proof, public_input and vk
    let (proof, public_input, vk) = proof_artifacts();

    MsgSubmitProof {
        creator: account_id,
        proof_system: BITVM_PROOF_SYSTEM.to_string(),
        proof,
        public_input,
        vk,
        namespace: NAMESPACE.to_string(),
    }
}
```

#### 2. get\_tx

**Description**: Queries the status of a specific transaction. after submitting the proof, this method can be used to check whether the transaction was successfully submitted to the blockchain network.

**Parameters**:

* **tx\_hash**: The hash of the transaction to query.

**Example Usage**:

```rust
const SENDER_PRIVATE_KEY: &str =
"59514b4e9c63b91cc9d3b6b882f1c5ee7449890c7c1116782670c71c96957897";
const NODE: &str = "http://54.65.137.66:9090";
let gas_limit = 80_000_000_u64;
let fee = 2000_u128;
let tx_id = "FECF6B15F33A220A4ACAB850BD968BB8C6C16DD610C5294B19C2C91511E7EE44";
let query_client = TxClient::new(SENDER_PRIVATE_KEY, NODE, fee, gas_limit);
let tx = query_client.get_tx(tx_id).await;
```

####

#### 4. create\_staker

**Description**: Adds a new validator to the Fiamma network.

**Parameters**:

* **creator**: The Account identifiers.
* **staker\_address**: The address of the validator.

```rust
pub struct MsgCreateStaker {
    pub creator: AccountId,
    pub staker_address: String,
}
```

**Example Usage**:

```rust
const SENDER_PRIVATE_KEY: &str =
"59514b4e9c63b91cc9d3b6b882f1c5ee7449890c7c1116782670c71c96957897";
const NODE: &str = "http://54.65.137.66:9090";
let wallet = Wallet::new(SENDER_PRIVATE_KEY);
let gas_limit = 80_000_000_u64;
let fee = 2000_u128;
let tx_client = TxClient::new(SENDER_PRIVATE_KEY, NODE, fee, gas_limit);
let msg = MsgCreateStaker {
    creator: wallet.account_id.clone(),
    staker_address: "fiammavaloper124lzt3g4axrqf8p58f6hs9uzdk056y3cey2m5r".to_string(),
};
let resp = tx_client.create_staker(msg).await;
```

#### 5. remove\_staker

**Description**: Deletes an existing validator from the Fiamma network.

**Parameters**:

* **creator**: The Account identifiers.
* **staker\_address**: The address of the validator.

```rust
pub struct MsgRemoveStaker {
    pub creator: AccountId,
    pub staker_address: String,
}
```

**Example Usage**:

```rust
const SENDER_PRIVATE_KEY: &str =
"59514b4e9c63b91cc9d3b6b882f1c5ee7449890c7c1116782670c71c96957897";
const NODE: &str = "http://54.65.137.66:9090";
let wallet = Wallet::new(SENDER_PRIVATE_KEY);
let gas_limit = 80_000_000_u64;
let fee = 2000_u128;
let tx_client = TxClient::new(SENDER_PRIVATE_KEY, NODE, fee, gas_limit);
let msg = MsgRemoveStaker {
    creator: wallet.account_id.clone(),
    staker_address: "fiammavaloper124lzt3g4axrqf8p58f6hs9uzdk056y3cey2m5r".to_string(),
};
let resp = tx_client.remove_staker(msg).await;
```

#### 6. get\_account\_info

**Description**: contains all the necessary fields for basic account functionality. **Parameters**: An instance of the `Wallet` struct created with the `PRIVATE_KEY`. This wallet will manage the user's account and facilitate interactions with the Fiamma blockchain.

**Example Usage**:

```rust
const SENDER_PRIVATE_KEY: &str =
"59514b4e9c63b91cc9d3b6b882f1c5ee7449890c7c1116782670c71c96957897";
const NODE: &str = "http://54.65.137.66:9090";
let wallet = Wallet::new(PRIVATE_KEY);
let account_info = wallet.get_account_info(NODE.to_string()).await;
```

#### 7. get\_proof\_data

**Description**: Retrieves the necessary proof data from the Fiamma blockchain.

**Parameters**:

* **proof\_id**: A unique identifier for the proof you want to retrieve.

**Response**: The `ProofData` struct corresponds to the `MsgSubmitProof` structure in that both are designed to encapsulate information relevant to the submission and verification of proofs within the Fiamma blockchain context.

```rust
pub struct ProofData {
    #[prost(enumeration = "ProofSystem", tag = "1")]
    pub proof_system: i32,
    #[prost(bytes = "vec", tag = "2")]
    pub proof: ::prost::alloc::vec::Vec<u8>,
    #[prost(bytes = "vec", tag = "3")]
    pub public_input: ::prost::alloc::vec::Vec<u8>,
    #[prost(bytes = "vec", tag = "4")]
    pub vk: ::prost::alloc::vec::Vec<u8>,
    #[prost(string, tag = "5")]
    pub namespace: ::prost::alloc::string::String,
}
```

**Example Usage**:

```rust
const NODE: &str = "http://54.65.137.66:9090";
let proof_id = "1776686b821785672155f4f34a0cf0d088e721e3ec5ff32709a7cec1b5a3b669";
let query_client = QueryClient::new(NODE);
let proof_data = query_client.get_proof_data(proof_id).await;
```

#### 8. get\_bitvm\_challenge\_data

**Description**: Retrieves the challenge data related to a specific BitVM proof or transaction.

**Parameters**:

* **proof\_id**: A unique identifier for the proof you want to retrieve.

**Response**:

* **verify\_result** (`bool`): Indicates whether the verification of the challenge was successful.
* **witness** (`Vec<u8>`): Contains the witness data needed for the proof validation process.
* **vk** (`Vec<u8>`): Represents the verification key used in the proof system.
* **public\_input** (`Vec<u8>`): Holds the public input data required for the challenge.
* **proposer** (`String`): Specifies the account or entity that proposed the challenge.

```rust
pub struct BitVmChallengeData {
    #[prost(bool, tag = "1")]
    pub verify_result: bool,
    #[prost(bytes = "vec", tag = "2")]
    pub witness: ::prost::alloc::vec::Vec<u8>,
    #[prost(bytes = "vec", tag = "3")]
    pub vk: ::prost::alloc::vec::Vec<u8>,
    #[prost(bytes = "vec", tag = "4")]
    pub public_input: ::prost::alloc::vec::Vec<u8>,
    #[prost(string, tag = "5")]
    pub proposer: ::prost::alloc::string::String,
}
```

**Example Usage**:

```rust
const NODE: &str = "http://54.65.137.66:9090";
let proof_id = "1776686b821785672155f4f34a0cf0d088e721e3ec5ff32709a7cec1b5a3b669";
let query_client = QueryClient::new(NODE);
let bitvm_challenge_data = query_client.get_bitvm_challenge_data(proof_id).await;
```

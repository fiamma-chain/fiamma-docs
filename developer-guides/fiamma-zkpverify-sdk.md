---
description: >-
  To make it easier to send zkpverify requests to the fiamma network, fiamma
  supports multi-language sdk, which can be easily used by developers.
---

# Fiamma ZKPVerify SDK

## Fiamma-sdk-rs

The [fiamma-sdk-rs](https://github.com/fiamma-chain/fiamma-sdk-rs.git) is the Rust SDK for the Fiamma chain, providing a range of APIs for interacting with the Fiamma blockchain. This SDK is primarily designed to simplify the process of blockchain development in Rust, covering fundamental on-chain operations and related functionalities.

### Main Features

#### For eco-project parties

* [Submit a proof to the blockchain.](fiamma-zkpverify-sdk.md#id-1.-submit\_proof)
* [Query transaction status and results.](fiamma-zkpverify-sdk.md#id-2.-get\_tx)
* [Query a proof verify result and status.](fiamma-zkpverify-sdk.md#id-3.-get\_verify\_result)

#### Other features

* Create and remove validators on the Fiamma blockchain.
* Query the challenge data related to a specific BitVM proof or transaction.
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
* **data\_location**:  proof data storage location, the default is fiamma, you can specify the DA storage later.

```rust
pub struct MsgSubmitProof {
    pub creator: AccountId,
    pub proof_system: String,
    pub proof: Vec<u8>,
    pub public_input: Vec<u8>,
    pub vk: Vec<u8>,
    pub namespace: String,
    pub data_location: String,
} 
```

**Example Usage**:

```rust
const SENDER_PRIVATE_KEY: &str =
"59514b4e9c63b91cc9d3b6b882f1c5ee7449890c7c1116782670c71c96957897";
const NODE: &str = "http://127.0.0.1:9090";
const BITVM_PROOF_SYSTEM: &str = "GROTH16_BN254_BITVM";
const NAMESPACE: &str = "test-namespace";
const DATA_LOCATION: &str = "FIAMMA";
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
        data_location: DATA_LOCATION.to_string(),
    
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
const NODE: &str = "http://127.0.0.1:9090";
let gas_limit = 80_000_000_u64;
let fee = 2000_u128;
let tx_id = "FECF6B15F33A220A4ACAB850BD968BB8C6C16DD610C5294B19C2C91511E7EE44";
let query_client = TxClient::new(SENDER_PRIVATE_KEY, NODE, fee, gas_limit);
let tx = query_client.get_tx(tx_id).await;
```

#### 3. get\_verify\_result

**Description**: Retrieves the verification result of a previously submitted ZKP. The result indicates whether the proof has passed the verification checks.

**Parameters**:

* **proof\_id**: A unique identifier for the proof you want to retrieve.

**Response**:

* **proof\_id** (`String`): Unique identifier of the proof.
* **proof\_system** (`i32`): Enum representing the proof system used.
* **data\_commitment** (`String`): Commitment to the data that was verified.
* **data\_location** (`i32`): Enum representing where the data is located.
* **result** (`bool`): Verification result (true if successful).
* **status** (`i32`): Enum representing the current status of verification.
* **community\_verification\_count** (`u64`): Number of community verifications performed.
* **namespace** (`String`): The namespace under which this proof belongs.

```rust
pub struct VerifyResult {
    #[prost(string, tag = "1")]
    pub proof_id: ::prost::alloc::string::String,
    #[prost(enumeration = "ProofSystem", tag = "2")]
    pub proof_system: i32,
    #[prost(bool, tag = "3")]
    pub result: bool,
    #[prost(enumeration = "VerificationStatus", tag = "4")]
    pub status: i32,
    #[prost(uint64, tag = "5")]
    pub community_verification_count: u64,
    #[prost(string, tag = "6")]
    pub namespace: ::prost::alloc::string::String,
}
```

**Example Usage**:

```rust
const NODE: &str = "http://127.0.0.1:9090";
let proof_id = "8a17276c37500fe1f0b277f21205592eac037b60f8a7021713ed2b99fe4f78f2";
let query_client = QueryClient::new(NODE);
let get_verify_result = query_client.get_verify_result(proof_id).await;
```

#### 4. get\_verify\_result\_by\_namespace

**Description**: Retrieves the verification results for a specific namespace. This method is useful for querying the verification status of proofs submitted under a certain namespace, making it possible to verify the results of multiple proofs associated with the same logical group or entity.

**Parameters**:

* **namespace** (`String`): The namespace for which the verification results are requested which typically represents a logical grouping of proofs.

**Response**:

* **Vec**: A vector of VerifyResult objects, each representing the verification details of a proof under the given namespace.

**Example Usage**:

```rust
const NODE: &str = "http://127.0.0.1:9090";
const NAMESPACE: &str = "test-namespace";
let query_client = QueryClient::new(NODE);
let get_verify_results = query_client.get_verify_result_by_namespace(NAMESPACE).await;
```

#### 5. submit\_community\_verification

**Description**: allows a community member to submit their verification result for a specific proof in the Fiamma network.

**Parameters**:

* **creator**: The Account identifiers.
* **proof\_id**: Unique identifier of the proof.
* **verify\_result**: A boolean value representing the community member’s assessment of the proof.

```rust
pub struct MsgSubmitCommunityVerification {
    pub creator: AccountId,
    pub proof_id: String,
    pub verify_result: bool,
}
```

**Example Usage**:

```rust
const SENDER_PRIVATE_KEY: &str =
"59514b4e9c63b91cc9d3b6b882f1c5ee7449890c7c1116782670c71c96957897";
const NODE: &str = "http://127.0.0.1:9090";
const BITVM_PROOF_SYSTEM: &str = "GROTH16_BN254_BITVM";
const NAMESPACE: &str = "test-namespace";
let proof_id = "8a17276c37500fe1f0b277f21205592eac037b60f8a7021713ed2b99fe4f78f2";
let wallet = Wallet::new(SENDER_PRIVATE_KEY);
let gas_limit = 80_000_000_u64;
let fee = 2000_u128;
let tx_client = TxClient::new(SENDER_PRIVATE_KEY, NODE, fee, gas_limit);
let submit_community_verification_msg = MsgSubmitCommunityVerification {
    creator: wallet.account_id.clone(),
    proof_id: proof_id.to_string(),
    verify_result: true,
};
let resp = tx_client
    .submit_community_verification(submit_community_verification_msg)
    .await
    .unwrap();
```

#### 6. create\_staker

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
const NODE: &str = "http://127.0.0.1:9090";
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

#### 7. remove\_staker

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
const NODE: &str = "http://127.0.0.1:9090";
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

#### 8. get\_account\_info

**Description**: contains all the necessary fields for basic account functionality. **Parameters**: An instance of the `Wallet` struct created with the `PRIVATE_KEY`. This wallet will manage the user's account and facilitate interactions with the Fiamma blockchain.

**Example Usage**:

```rust
const SENDER_PRIVATE_KEY: &str =
"59514b4e9c63b91cc9d3b6b882f1c5ee7449890c7c1116782670c71c96957897";
const NODE: &str = "http://127.0.0.1:9090";
let wallet = Wallet::new(PRIVATE_KEY);
let account_info = wallet.get_account_info(NODE.to_string()).await;
```

#### 9. get\_proof\_data

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
    #[prost(enumeration = "DataLocation", tag = "5")]
    pub data_location: i32,
    #[prost(string, tag = "6")]
    pub namespace: ::prost::alloc::string::String,
}

```

**Example Usage**:

```rust
const NODE: &str = "http://127.0.0.1:9090";
let proof_id = "1776686b821785672155f4f34a0cf0d088e721e3ec5ff32709a7cec1b5a3b669";
let query_client = QueryClient::new(NODE);
let proof_data = query_client.get_proof_data(proof_id).await;
```

#### 10. get\_bitvm\_challenge\_data

**Description**: Retrieves the challenge data related to a specific BitVM proof or transaction.

**Parameters**:

* **proof\_id**: A unique identifier for the proof you want to retrieve.

**Response**:

* **witness** (`Vec<u8>`): Contains the witness data needed for the proof validation process.
* **proposer** (`String`): Specifies the account or entity that proposed the challenge.

```rust
pub struct BitVmChallengeData {
    #[prost(bytes = "vec", tag = "1")]
    pub witness: ::prost::alloc::vec::Vec<u8>,
    #[prost(string, tag = "2")]
    pub proposer: ::prost::alloc::string::String,
}
```

**Example Usage**:

```rust
const NODE: &str = "http://127.0.0.1:9090";
let proof_id = "1776686b821785672155f4f34a0cf0d088e721e3ec5ff32709a7cec1b5a3b669";
let query_client = QueryClient::new(NODE);
let bitvm_challenge_data = query_client.get_bitvm_challenge_data(proof_id).await;
```

#### 11. get\_pending\_proof

**Description**: Retrieves a list of proofs that are currently awaiting verification. This is useful for community members or validators who want to access pending tasks and perform verifications.

**Response**:

* **Vec**: A vector of VerifyResult objects that are currently pending verification.

**Example Usage**:

```rust
const NODE: &str = "http://127.0.0.1:9090";
const NAMESPACE: &str = "test-namespace";
let query_client = QueryClient::new(NODE);
let get_pending_proof = query_client.get_pending_proof().await;
```

#### 12. get\_pending\_proof\_by\_namespace

**Description**: Retrieves a list of proofs that are currently awaiting verification for a specific namespace. This is useful for community members or validators who want to access pending tasks and perform verifications.

**Parameters**:

* **namespace** (`String`): The namespace for which the pending proofs are requested which typically represents a logical grouping of proofs.

**Response**:

* **Vec**: A vector of VerifyResult objects that are currently pending verification under the given namespace.

**Example Usage**:

```rust
const NODE: &str = "http://127.0.0.1:9090";
const NAMESPACE: &str = "test-namespace";
let query_client = QueryClient::new(NODE);
let get_pending_proof_by_namespace = query_client.get_pending_proof_by_namespace(NAMESPACE).await;
```

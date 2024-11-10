---
description: >-
  In this tutorial, you will learn about the Command Line Interface(CLI) introduction related
  to fiammad zkpverify and bitvmstaker.
---

# CLI Command Overview

{% hint style="info" %}
Note! that the CLI here refers to transactions and queries in the fiamma verification network and doesn't include the regular cosmos application chain.
{% endhint %}

The Fiamma Command Line Interface(CLI) provides essential commands to manage zero-knowledge proofs and staker accounts, streamlining interactions with the blockchain. Use the commands and options as described to perform operations effectively.

Use CLI tools `fiammad` you can:
- send **zkpverify transactions** with `tx zkpverify [command] [flags]` and queries with `query zkpverify [command] [flags]`.
- send **bitvmstaker transactions** with `tx bitvmstaker [command] [flags]` and queries with `query bitvmstaker [command] [flags]`.

Global Flags usually contains: `--from`, `--chain-id`, `--gas`, `--node`, `--keyring-backend`.

command currently support:

## Tx Type CLI

**Zkpverify transactions**
* [`submit-proof`](cli-command-overview.md#submit-proof)
* [`submit-community-verification`](cli-command-overview.md#submit-community-verification)

**Bitvmstaker transactions**
* [`create-staker`](cli-command-overview.md#create-staker)
* [`register-vk `](cli-command-overview.md#register-vk)
* [`remove-staker`](cli-command-overview.md#remove-staker)
* [`remove-vk`](cli-command-overview.md#remove-vk)
* [`update-committee-address`](cli-command-overview.md#update-committee-address)

### **submit-proof**&#x20;

A (zkpverify) operation for verifying a proof by namespace, proof\_system, proof, public\_input and vk.

request params:

```
{
  "namespace": "string",
  "proof_system": "string",
  "proof": "string",
  "public_input": "string",
  "vk": "string"
}
```

### **submit-community-verification**&#x20;

A community (zkpverify) operation for verifying a proof by proof\_id and verify\_result.&#x20;

request params:

```
{
  "proof_id": "string",
  "verify_result": "bool"
}
```

### **create-staker**&#x20;

A committee (bitvmstaker) operation for create a new staker account on the Fiamma blockchain by staker address.&#x20;

request params:

```
{
  "staker_address": "string"
}
```

### **remove-staker**&#x20;

A committee (bitvmstaker) operation for removing a staker account on the Fiamma blockchain by staker address. This action can be necessary for managing the network's staker list, ensuring that only valid stakers participate.&#x20;

request params:

```
{
  "staker_address": "string"
}
```

### **register-vk**&#x20;

A committee (bitvmstaker) operation for registering a new verification key (VK) for a specific proof system on the blockchain by verification key. This is essential for validating the correctness of proofs submitted to the network.&#x20;

request params:

```
{
  "vk": "string"
}
```
### **remove-vk**&#x20;

A committee (bitvmstaker) operation for removing a previously registered verification key (VK) for a specific proof system on the blockchain by verification key. This command is essential for maintaining the integrity of the verification processes by allowing the removal of outdated or incorrect VKs.&#x20;

request params:

```
{
  "vk": "string"
}
```

### **update-committee-address**&#x20;

A committee (bitvmstaker) operation for updating the address of the committee responsible for overseeing the blockchain operations or specific proof systems. This is crucial for ensuring that the governance structure is current and that the correct addresses are in use for administrative tasks.&#x20;

request params:

```
{
  "new_committee_address": "string"
}
```

## Query Type CLI

**Zkpverify queries**
* [`get-proof-data`](cli-command-overview.md#get-proof-data)
* [`get-bitvm-challenge-data`](cli-command-overview.md#get-bitvm-challenge-data)
* [`get-verify-result`](cli-command-overview.md#get-verify-result)
* [`get-verify-results-by-namespace`](cli-command-overview.md#get-verify-results-by-namespace)
* [`pending-proof`](cli-command-overview.md#pending-proof)
* [`pending-proof-by-namespace`](cli-command-overview.md#pending-proof-by-namespace) &#x20;

**Bitvmstaker queries**
* [`all-staker-info`](cli-command-overview.md#all-staker-info)
* [`committee-address`](cli-command-overview.md#committee-address)
* [`registered-vk-list`](cli-command-overview.md#registered-vk-list)&#x20;

### **get-bitvm-challenge-data**&#x20;

Query bitVM chanllenge data stored in the fiamma by proof\_id.&#x20;

request params:

```
{
  "proof_id": "string",
}
```

response:

```
{
  "bitvm_challenge_data": {
    "proposer": "string",
    "public_input": "string",
    "verify_result": "bool",
    "vk": "string",
    "witness": "string"
  }
}
```

### **get-proof-data**&#x20;

Query Proof data stored in the fiamma by proof\_id.&#x20;

request params:

```
{
  "proof_id": "string",
}
```

response:

```
{
  "proof_data": {
    "proof_system": "integer",
    "proof": "string",
    "public_input": "string",
    "vk": "string",
    "namespace": "string"
  }
}
```

### **get-verify-result**

Query Proof verify status stored in the fiamma by proof\_id.&#x20;

request params:

```
{
  "proof_id": "string",
}
```

response:

```
{
  verify_result: {
      "proof_id": "string",
      "proof_system": "string",
      "data_commitment": "string",
      "data_location": "string",
      "result": "bool",
      "status": "integer",
      "community_verification_count": "integer",
      "namespace": "string"
  }
}
```

### **get-verify-results-by-namespace**

Query Proof verify status stored in the fiamma by namespace.&#x20;

request params:

```
{
  "namespace": "string",
}
```

response:

```
{
  verify_result: [
    {
      "proof_id": "string",
      "proof_system": "string",
      "data_commitment": "string",
      "data_location": "string",
      "result": "bool",
      "status": "integer",
      "community_verification_count": "integer",
      "namespace": "string"
    },
    ...
  ]
}
 
```

### **pending-proof**&#x20;

Queries a list of pending proof verification items.&#x20;

There is no request param for this method.

response:

```
{
  "pending_proofs": [
    {
      "proof_id": "string",
      "proof_system": "string",
      "data_commitment": "string",
      "data_location": "string",
      "result": bool,
      "status": "string",
      "community_verification_count": "string",
      "namespace": "string"
    },
    ...
  ],
  "pagination": {
    "next_key": "string",
    "total": "integer"
  }
}
```

### **pending-proof-by-namespace**&#x20;

Queries a list of pending proof verification items by namespace.&#x20;

request params:

```
{
  "namespace": "string",
}
```

response:

```
{
  "pending_proofs": [
    {
      "proof_id": "string",
      "proof_system": "string",
      "data_commitment": "string",
      "data_location": "string",
      "result": bool,
      "status": "string",
      "community_verification_count": "string",
      "namespace": "string"
    },
    ...
  ],
  "pagination": {
    "next_key": "string",
    "total": "integer"
  }
}
```

### **all-staker-info**&#x20;

Queries a list of holding information about all the stakers. It may include details such as staker_index and staker_address.&#x20;

response:

```
{
  "all_staker_info": [
    {
      "staker_index": "integer",
      "staker_address": "string"
    },
    ...
  ],
  "pagination": {
    "next_key": "string",
    "total": "integer"
  }
}
```

### **committee-address**&#x20;

Queries the address associated with the committee responsible for overseeing certain operations or governance within Fiamma blockchain system.&#x20;

response:

```
{
  "committeeAddress": "string",
}
```

### **registered-vk-list**&#x20;

Queries a list of registered verification keys (VKs).&#x20;

response:

```
{
  "registered_vk_list": [
    ["string"]
    ,
    ...
  ],
  "pagination": {
    "next_key": "string",
    "total": "integer"
  }
}
```

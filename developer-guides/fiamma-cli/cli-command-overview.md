---
description: >-
  In this tutorial, you will learn about the command line introduction related
  to fiammad zkpverify.
---

# CLI Command Overview

{% hint style="info" %}
Note! that the cli here refers to transactions and queries in the fiamma verification network and doesn't include the regular cosmos application chain.
{% endhint %}

Use cli tools `fiammad` you can send transactions with `tx zkpverify [command] [flags]` and queries with `tx zkpverify query [command] [flags]`.

Global Flags usually contains: `--from`, `--chain-id`, `--gas`, `--node`, `--keyring-backend`.

command currently support:

## Tx Type CLI

* [`submit-proof`](cli-command-overview.md#submit-proof)
* [`submit-community-verification`](cli-command-overview.md#submit-community-verification)

### **submit-proof**&#x20;

A (zkpverify) operation for verifying a proof by proof\_system, proof, public\_input and vk.

request params:

```
{
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
  "verify_result": bool
}
```

## Query Type CLI

* [`get-proof-data`](cli-command-overview.md#get-proof-data)
* [`get-bitvm-witness`](cli-command-overview.md#get-bitvm-witness)
* [`get-verify-result`](cli-command-overview.md#get-verify-result)
* [`pending-proof`](cli-command-overview.md#pending-proof) &#x20;

### **get-bitvm-witness**&#x20;

Query bitVM witness stored in the fiamma by proof\_id.&#x20;

request params:

```
{
  "proof_id": "string",
}
```

response:

```
{
  "witness": "string"
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
    "proof_system": "string",
    "proof": "string",
    "public_input": "string",
    "vk": "string"
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
      "proof_id": "string",
      "proof_system": "string",
      "data_commitment": "string",
      "data_location": "string",
      "result": bool,
      "status": "string",
      "community_verification_count": "string"
    },
```

### **pending-proof**&#x20;

Queries a list of pending proof verification items.&#x20;

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
      "community_verification_count": "string"
    },
    ...
  ],
  "pagination": {
    "next_key": "string",
    "total": "string"
  }
}
```

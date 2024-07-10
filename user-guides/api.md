# API

The following API's are recommended for development purposes. For maximum control and reliability it's recommended to run your own node.

## Networks

Quickly connect your app or client to Fiamma public testnets. You can use [Networks](https://testnet-api.fiammachain.io/) to connect to the Fiamma.

## Clients

The Fiamma Network supports different clients in order to support Cosmos and Fiamma transactions and queries. You can use Swagger as a REST interface for state queries and transactions:

|                                                                                  | Description                                                                          | Default Port | Swagger                                                             |
| -------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------ | ------------ | ------------------------------------------------------------------- |
| **Cosmos REST** | Query or send Fiamma transactions using an HTTP RESTful API                           | `1317`       | [Testnet](https://testnet-api.fiammachain.io/) |                                                                    |
| **Tendermint [RPC](#tendermint-rpc)**                                            | Query transactions, blocks, consensus state, broadcast transactions, etc.            | `26657`      | [Localhost](http://127.0.0.1:26657)                 |                                                                    |
| **Command Line Interface (CLI)**                     | Query or send Fiamma transactions using your Terminal or Console.                     | N/A          |                                                                     |

### CLI
Note that the cli here refers to transactions and queries in the fiamma verification network and doesn't include the regular cosmos application chain.

Use cli tools `fiammd` you can send transactions with `tx zkpverify [command] [flags]` and queries with `tx zkpverify query [command] [flags]`. 

Global Flags usually contains: `--from`, `--chain-id`, `--gas`, `--node`, `--keyring-backend`.

command currently support: 
- `submit-proof` and `submit-community-verification` for send transaction (POST). 
- `get-proof-data`, `get-bitvm-witness` and `pending-proof` for queries (GET).

**submit-proof**
A (zkpverify) operation for verifying a proof by proof_system, proof, public_input and vk.

request params:
```
{
  "proof_system": "string",
  "proof": "string",
  "public_input": "string",
  "vk": "string"
}
```
**submit-community-verification**
A community (zkpverify) operation for verifying a proof by proof_id and verify_result.
request params:
```
{
  "proof_id": "string",
  "verify_result": bool
}
```
**get-bitvm-witness**
Query bitVM witness stored in the fiamma by proof_id.
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
**get-proof-data**
Query Proof data stored in the fiamma by proof_id.
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
**pending-proof**
Queries a list of pending proof verification items.
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
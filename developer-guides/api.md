---
description: >-
  The following API's are recommended for development purposes. For maximum
  control and reliability it's recommended to run your own node.
---

# Fiamma ZKPVerfiy APIs

## Network

Quickly connect your app or client to Fiamma public testnets. You can check the [**network**](network-information.md) page for information about the current test network

## RPC And APIs

The Fiamma RPC interface includes basic query interfaces for the Tendermint consensus, and the API includes basic interfaces related to Cosmos, as well as interfaces for the unique **zkpverify module** of the Fiamma network.

| Name                | Description                                                               | Default Port | Link                                                                       |
| ------------------- | ------------------------------------------------------------------------- | ------------ | -------------------------------------------------------------------------- |
| **Fiamma Rest API** | Query or send Fiamma transactions using an HTTP RESTful API               | `1317`       | [https://testnet-api.fiammachain.io/](https://testnet-api.fiammachain.io/) |
| **Fiamma RPC**      | Query transactions, blocks, consensus state, broadcast transactions, etc. | `26657`      | [https://testnet-rpc.fiammachain.io/](https://testnet-rpc.fiammachain.io/) |

### RPC-Msg

Fiamma's RPC message modules all start with **/fiamma.zkpverify.Msg/**,  followed by the message name. These requests are all **POST** requests

### RPC-Query&#x20;

Fiamma's RPC query modules all start with **/fiamma.zkpverify/**, followed by the query name. These requests are all **GET** requests

### Proto Buff

All messages and queries of the fiamma network are defined in proto buff files, which can be found in [**buf.build**](https://buf.build/fiamma-chain/fiamma/tree/main:fiamma/zkpverify).


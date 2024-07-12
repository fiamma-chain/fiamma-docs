---
description: >-
  The following API's are recommended for development purposes. For maximum
  control and reliability it's recommended to run your own node.
---

# Rest API And GRPC

## Network

Quickly connect your app or client to Fiamma public testnets. You can check the [**network**](network-information.md) page for information about the current test network

## GRPC, Rest, and CometBFT Endpoints

The Fiamma RPC interface includes basic query interfaces for the Tendermint consensus, and the API includes basic interfaces related to Cosmos, as well as interfaces for the unique **zkpverify module** of the Fiamma network.

| Name                | Description                                                                                                            | Link                                                                        |
| ------------------- | ---------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------- |
| **Fiamma Rest API** | Query or send Fiamma transactions using an HTTP restful API                                                            | [https://testnet-api.fiammachain.io/](https://testnet-api.fiammachain.io/)  |
| **Fiamma RPC**      | Query transactions, blocks, consensus state, broadcast transactions, etc.                                              | [https://testnet-rpc.fiammachain.io/](https://testnet-rpc.fiammachain.io/)  |
| **FIamma GRPC**     | Using a predefined proto data structure, grpc requests can be sent to the fiamma network for transactions and queries. | [https://testnet-grpc.fiammachain.io/](https://testnet-rpc.fiammachain.io/) |

## Rest API  Info

The list of all REST APIs supported by Fiamma can be obtained from the [Swagger documentation](https://testnet-api.fiammachain.io/).

### API-Msg

Fiamma's zkverify RPC message modules all start with **/fiamma.zkpverify.Msg/**,  followed by the message name. These requests are all **POST** requests

### API-Query&#x20;

Fiamma's zkpverify RPC query modules all start with **/fiamma.zkpverify/**, followed by the query name. These requests are all **GET** requests

## GRPC  Info

fiamma supports grpc requests, you can build grpc requests using any language sdk that supports grpc clients, a list of fiamma defined proto files can be found in [Proto Buff](api.md#proto-buff)

### Proto Buff

All messages and queries of the fiamma network are defined in proto buff files, which can be found in [**buf.build**](https://buf.build/fiamma-chain/fiamma/tree/main:fiamma/zkpverify).

{% hint style="info" %}
Note! All gRPC requests will correspond to a REST request.  For instance, querying pendingProof could be done via the /**fiamma.zkpverify.Query/PendingProof** gRPC endpoint, or alternatively via the gRPC-gateway  **/fiamma/zkpverify/pending\_proof** REST endpoint: both will return the same result.&#x20;
{% endhint %}

